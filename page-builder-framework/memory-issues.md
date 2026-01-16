# Customizer Memory Consumption Analysis

## Overview

This document analyzes the browser memory consumption issues in the WordPress Customizer when using the `page-builder-framework` theme with the `wpbf-premium` plugin.

---

## Key Findings

### 1. Massive Number of Setting Bindings (~260+ in theme alone)

**Location**: `inc/customizer/js/postmessage-parts/*.ts`

Each call to `listenToCustomizerValueChange()` creates:
- A customizer setting lookup
- An initial value handler call
- A persistent `setting.bind()` callback that remains in memory

**Files with high binding counts:**
| File | Approx. Bindings |
|------|------------------|
| `woocommerce.ts` | ~35 |
| `footer-builder-rows.ts` | ~48+ (6 rows × 8 settings) |
| `mobile-header-builder-rows.ts` | ~30+ |
| `header-builder-reveal.ts` | ~25+ |
| `menu-triggers.ts` | ~40+ |

**Premium plugin** adds ~80+ more bindings from files like:
- `navigation.ts` (~30)
- `headings.ts` (~30)
- `sticky-navigation.ts` (~25)

> [!WARNING]
> All 340+ bindings are registered at customizer load, regardless of which sections the user opens.

---

### 2. Dynamic Style Element Proliferation

**Location**: `customizer-util.ts` → `writeCSS()` / `getStyleTag()`

Each setting with live preview creates a `<style data-id="...">` element in the document head. For responsive fields, this multiplies:

```
page_h1_font_size      →  Creates 3 style tags:
                          - page_h1_font_size-desktop
                          - page_h1_font_size-tablet  
                          - page_h1_font_size-mobile
```

**Estimated style elements**: 400-500+ when fully loaded.

> [!IMPORTANT]
> Style elements are never removed from the DOM during the session.

---

### 3. Typography Controls - Multiple Bindings Per Control

**Location**: `Typography/src/typography-control.ts`

Each typography control creates bindings for:
- Main setting (`page_font_family`)
- Sub-properties: `[font-family]`, `[variant]`, `[font-size]`, `[line-height]`, `[letter-spacing]`

**Pattern issues:**
```typescript
// Inside composeFontProperties()
window.wp.hooks.addAction(
    "wpbf.dynamicControl.initWpbfControl",
    // This action is added EVERY time composeFontProperties runs
    // on every font-family change!
);
```

---

### 4. Control Lifecycle and Destroy Methods

**Location**: `Customizer/Controls/*/src/*.ts`

#### Controls with Proper Destroy

Most controls **do have** `destroy()` methods through two patterns:

1. **Controls extending `wpbfDynamicControl`** (base-control.ts) inherit a basic destroy:
   - Checkbox, Radio, Editor, Dimension, Generic, Builder, etc.
   - Removes `change input paste click` event handlers

2. **Controls extending `Control` directly** with custom destroy:
   - `ColorControl` / `MulticolorControl` → Unmounts React root
   - `SliderControl` / `InputSliderControl` → Unmounts React root
   - `SelectControl` → Calls `select2("destroy")`, removes event handlers
   - `MarginPaddingControl` → Unmounts React root

#### When Destroy Is Called

Destroy is triggered via `customizer.control.bind("removed", onRemoved)` pattern:

```typescript
// Example from ColorControl.tsx
function handleOnRemoved(removedControl) {
    if (control === removedControl) {
        if (control.destroy) control.destroy();
        control.container?.remove();
        customizer.control.unbind("removed", handleOnRemoved);
    }
}
customizer.control.bind("removed", handleOnRemoved);
```

> [!WARNING]
> The "removed" event only fires when `customizer.control.remove()` is explicitly called.
> **It does NOT fire when sections collapse** - controls remain in memory.

---

### 5. Select2 Instances for Google Fonts

**Location**: `Select/src/select-control.ts`

Each typography control with Google Fonts creates a Select2 instance:
- Select2 maintains its own event listeners and DOM elements
- The `destroy()` method properly cleans up but is **never invoked**

**Data payload**:
- `wpbfGoogleFonts` global variable contains ~1000+ font families with variants
- Each variant dropdown may hold 10-20 options

---

### 6. Control Dependencies System

**Location**: `Base/src/control-dependencies.ts`

For every dependency relationship:
```typescript
function listenDependencyControl(dependencySettingId: string) {
    customizer(dependencySettingId, function (setting) {
        handleRulesCondition(...);
        setting.bind(function (newValue: string) {
            handleRulesCondition(...);  // Another binding!
        });
    });
}
```

This adds binding callbacks for **every control that has dependencies**.

---

### 7. Controls Missing Destroy Methods

**Critical Issue**: Two controls extend `Control` directly but have **no destroy method**:

#### `sortable-control.ts`
- Extends `wp.customize.Control` directly (not wpbfDynamicControl)
- Creates jQuery Sortable: `container.find("ul.sortable").sortable({...})`
- Binds click events: `.find("i.visibility").on("click", ...)`
- **Missing**: No `destroy()` to call `.sortable("destroy")` or unbind events

#### `repeater-control.ts` (~950 lines)
- Extends `wp.customize.Control` directly
- Creates multiple bindings: `container.on("click", ...)` (6+ handlers)
- Creates jQuery Sortable: `repeaterFieldsContainer.sortable({...})`
- Creates wp.media frames: `this.frame = wp.media({...})`
- Initializes color pickers: `wpColorPicker(options)`
- Creates row objects with their own event handlers
- **Missing**: No `destroy()` method at all despite heavy resource usage

> [!CAUTION]
> The Repeater control is a significant memory leak source. Each usage creates media frames, color pickers, sortable instances, and event handlers that are never cleaned up.

---

## Memory Consumption Summary

| Category | Impact | Notes |
|----------|--------|-------|
| PostMessage bindings (theme) | High | ~260+ callbacks registered at load |
| PostMessage bindings (plugin) | High | ~80+ callbacks registered at load |
| Dynamic `<style>` elements | Medium | ~400-500, never removed |
| Typography field sub-bindings | Medium | ~50+ with hook accumulation bug |
| Control dependency bindings | Medium | ~100+ additional callbacks |
| Select2 instances | Medium | ~15-20, have destroy but not called on section close |
| React roots (color pickers) | Medium | ~40+, have destroy but not called on section close |
| **Missing destroy: Sortable** | High | jQuery Sortable + events never cleaned |
| **Missing destroy: Repeater** | **Critical** | Media frames, color pickers, sortable, 6+ event handlers |
| Google Fonts data (global) | Low | ~200KB, acceptable |

**Bottom line**: Controls with proper destroy methods exist, but:
1. Destroy is only called on explicit control removal (rare)
2. Two controls (Sortable, Repeater) have no destroy at all

---

## Root Causes

1. **Eager Registration**: All postMessage handlers register at load, not on-demand
2. **No Lazy Loading**: Premium features like WooCommerce handlers load even if WooCommerce isn't active
3. **No Cleanup**: Controls don't destroy bindings when sections collapse
4. **Callback Accumulation**: Some patterns add actions repeatedly (typography hooks)
5. **Single iframe context**: Everything runs in one frame with shared memory

---

## Recommendations

### Quick Wins (Low Risk)

1. **Conditional loading of WooCommerce handlers**
   - Check if WooCommerce is active before registering ~35 bindings
   
2. **Remove redundant hook additions**
   - Fix `typography-control.ts` to not add hooks inside `composeFontProperties()`

3. **Consolidate responsive style tags**
   - Use single style tag with media queries instead of 3 separate tags

### Medium-Term Improvements

4. **Lazy postMessage registration**
   - Only bind to settings when their section is first opened
   - Store handler functions, register on section expand

5. **Implement control cleanup**
   - Call `destroy()` when sections collapse (with debounce)
   - Unbind setting callbacks for hidden controls

6. **Use WeakMap for style tag references**
   - Allow garbage collection when references are released

### Long-Term Architecture

7. **Module-based loading**
   - Split postMessage handlers into dynamic imports
   - Load only when corresponding section/feature is accessed

8. **Virtual DOM for style management**
   - Batch style updates instead of per-property updates
   - Single style element with consolidated rules

9. **Consider iframe isolation**
   - Heavy controls (builders) in separate frames
   - Communicate via postMessage

---

## Testing Recommendations

To measure improvement, profile with Chrome DevTools:

```javascript
// Run in console to count bindings
Object.keys(wp.customize.settings.settings)
    .filter(k => wp.customize(k)?._dirty !== undefined)
    .length;

// Count style elements  
document.querySelectorAll('style.wpbf-customize-live-style').length;

// Memory snapshot
performance.measureUserAgentSpecificMemory?.();
```

## Possible Tasks for AI Agent

### Priority 1: Critical Fixes

1. **Add destroy method to `repeater-control.ts`**
   - Destroy jQuery Sortable: `this.repeaterFieldsContainer?.sortable("destroy")`
   - Unbind container events: `this.container?.off()`
   - Destroy wp.media frame: `this.frame?.dispose?.()`
   - Destroy color pickers: `.wpColorPicker("destroy")`
   - Clean up row objects

2. **Add destroy method to `sortable-control.ts`**
   - Destroy jQuery Sortable: `container.find("ul.sortable").sortable("destroy")`
   - Unbind click events: `container.find("i.visibility").off("click")`

### Priority 2: Quick Wins

3. **Fix hook accumulation in `typography-control.ts`**
   - Move `wp.hooks.addAction()` outside of `composeFontProperties()` function
   - Should only register hook once, not on every font change

4. **Add WooCommerce conditional loading**
   - In `postmessage.ts`, check if WooCommerce is active before calling `woocommerceSetup()`
   - Saves ~35 bindings when WooCommerce not active

5. **Consolidate responsive style tags**
   - In `headings.ts` and similar files, use single style tag with media queries
   - Instead of 3 separate calls to `writeCSS()` per responsive field

### Priority 3: Medium-Term Improvements

6. **Implement lazy postMessage registration**
   - Create a registry of handlers per section
   - Only `setting.bind()` when section is first expanded
   - Store handlers as functions until needed

7. **Add cleanup on section collapse**
   - Listen to `section.expanded.bind()` for collapse events
   - Call control `destroy()` methods with debounce on collapse
   - Re-embed controls on next expand

### Priority 4: Long-Term Architecture

8. **Split postMessage handlers into dynamic imports**
   - Convert each postmessage-parts file to dynamic `import()`
   - Load only when corresponding customizer section is accessed

9. **Create unified style management**
   - Single style element with consolidated CSS rules
   - Batch updates on requestAnimationFrame
   - Remove individual style tags approach

---

## Files to Review

### Critical (Missing destroy methods)
- `Customizer/Controls/Sortable/src/sortable-control.ts` - **No destroy**, has jQuery Sortable
- `Customizer/Controls/Repeater/src/repeater-control.ts` - **No destroy**, major leak source

### High Priority (PostMessage handlers)
- `inc/customizer/js/postmessage.ts` - Entry point
- `inc/customizer/js/postmessage-parts/*.ts` - All handler files
- `wpbf-premium/inc/customizer/js/postmessage.ts` - Plugin handlers

### Medium Priority (Control lifecycle)
- `Customizer/Controls/Base/src/base-control.ts` - Base control lifecycle
- `Customizer/Controls/Typography/src/typography-control.ts` - Font handling with hook bug
- `Customizer/Controls/Select/src/select-control.ts` - Select2 usage

---

*Analysis Date: 2026-01-16*
