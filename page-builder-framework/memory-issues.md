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

### 3. Typography Controls - Multiple Bindings Per Control ✅ FIXED

**Location**: `Typography/src/typography-control.ts`

Each typography control creates bindings for:
- Main setting (`page_font_family`)
- Sub-properties: `[font-family]`, `[variant]`, `[font-size]`, `[line-height]`, `[letter-spacing]`

**Pattern issues:** ✅ FIXED in v2.11.8+73
```typescript
// BEFORE: Inside composeFontProperties() - caused hook accumulation
// AFTER: Moved to setupTypographyFields() - registered once per control
window.wp.hooks.addAction(
    "wpbf.dynamicControl.initWpbfControl",
    "wpbf/typography/" + id,  // Unique namespace per control
    // ...
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

### 5. Select2 Instances for Google Fonts ✅ OPTIMIZED (v2.11.8+77)

**Location**: `Select/src/select-control.ts`, `Typography/TypographyField.php`

#### Typography Field Count

| Source | Typography Fields | Select2 Instances |
|--------|-------------------|-------------------|
| Theme (`inc/customizer/settings/typography/`) | 12 | 24 (2 per field) |
| Premium Plugin | 0 (uses individual controls) | 0 |
| **Total** | **12** | **24** |

**Theme typography fields (12 total)**:
- `title-tagline-fields.php`: 2 (logo font, tagline font)
- `text-fields.php`: 1 (body text font)
- `menu-fields.php`: 1 (menu font)
- `sub-menu-fields.php`: 1 (sub-menu font)
- `headings-fields.php`: 6 (H1-H6 fonts)
- `footer-fields.php`: 1 (footer font)

> [!NOTE]
> The premium plugin's heading typography uses individual `responsive-input-slider`, `color`, `slider`, and `select` controls instead of the `typography` control type, so it does NOT create Select2 instances for font-family selection.

#### PHP-Side Optimization (Partial)

The Google Fonts data is printed once via `TypographyStore::$control_vars_printed`:

```php
// TypographyField.php - JS object printed ONCE regardless of field count
if ( ! TypographyStore::$control_vars_printed ) {
    wp_localize_script( 'wpbf-controls-bundle', 'wpbfGoogleFonts', 
        ( new GoogleFontsUtil() )->getCollections() );
    TypographyStore::$control_vars_printed = true;
}
```

> [!WARNING]
> **Select2 DUPLICATES data internally!** When you pass `data: choicesFromGlobalVar`, Select2 does NOT keep a reference to your array. It creates its own internal JavaScript objects AND renders `<option>` DOM elements for each item.

#### JS-Side Problem: Data Duplication + Mutation Bug

```typescript
// select-control.ts - Each instance gets a reference to the SAME array
const choicesFromGlobalVar = window[choicesGlobalVar];

// ⚠️ BUG: This mutates the GLOBAL array!
choicesFromGlobalVar.forEach((choice, index) => {
    if (choice.id && values.includes(choice.id)) {
        choicesFromGlobalVar[index].selected = true;  // Pollutes global!
    }
});

// Select2 then COPIES this data internally
$selectbox?.select2({ data: choicesFromGlobalVar });
```

**Two problems:**
1. Each control mutates the shared global to set `selected: true`
2. Select2 creates internal copies of the ~200KB data array for EACH instance

#### Actual Memory Impact

| Resource | Size | Count | Total |
|----------|------|-------|-------|
| `wpbfGoogleFonts` global | ~200KB | 1 | ~200KB |
| Select2 internal data copy | ~200KB | 24 | **~4.8MB** |
| DOM `<option>` elements | ~100KB | 24 | **~2.4MB** |
| Select2 instance overhead | ~7KB | 24 | ~170KB |
| **Total for Google Fonts dropdowns** | | | **~7-8MB** |

> [!CAUTION]
> The 24 Google Fonts Select2 dropdowns consume approximately **7-8MB of memory** - far more than the ~400KB initially estimated. This is one of the largest memory consumers in the Customizer.

#### Possible Optimizations

1. **Use AJAX/remote data source** - Select2 can fetch data on demand instead of loading all ~1000 fonts upfront
2. **Custom DataAdapter** ✅ IMPLEMENTED (v2.11.8+77)
   - Created `SharedFontDataAdapter` that extends ArrayAdapter
   - Overrides `_normalizeItem()` to avoid `$.extend()` data copying
   - Pre-processes data with selection state without mutating global
   - **Fixed bug**: Removed global array mutation in `select-control.ts`
3. **Lazy initialization** - Only initialize Select2 when typography section expands
4. ~~**Fix the mutation bug**~~ ✅ FIXED in v2.11.8+77

**The `destroy()` method exists but is never called** when sections collapse - only on explicit control removal via `customizer.control.remove()`.

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

### 7. Controls Previously Missing Destroy Methods

**Status**: Both controls now have proper destroy methods.

#### `sortable-control.ts` ✅ FIXED (v2.11.8+72)
- Now has `destroy()` method that:
  - Destroys jQuery Sortable: `.sortable("destroy")`
  - Unbinds all container events: `.off()`
- Has `removed` event handler to trigger destroy on control removal

#### `repeater-control.ts` ✅ FIXED (v2.11.8+71)
- Now has comprehensive `destroy()` method that:
  - Destroys jQuery Sortable on repeater fields container
  - Unbinds all container event handlers
  - Disposes wp.media frame if exists
  - Destroys wpColorPicker instances
  - Cleans up row objects (unbinds container and header events)
  - Clears memoized template function and other references
- Has `removed` event handler to trigger destroy on control removal

> [!NOTE]
> Both controls now properly clean up resources when removed via `customizer.control.remove()`.
> The "removed" event still only fires on explicit removal, not section collapse.

---

## Memory Consumption Summary

| Category | Impact | Notes |
|----------|--------|-------|
| PostMessage bindings (theme) | High | ~260+ callbacks registered at load |
| PostMessage bindings (plugin) | High | ~80+ callbacks registered at load |
| **Select2 Google Fonts (24 instances)** | ✅ Optimized | Custom DataAdapter avoids `$.extend()` copying (v2.11.8+77) |
| Dynamic `<style>` elements | Medium | ~400-500, never removed |
| Typography field sub-bindings | ✅ Fixed | Hook accumulation fixed in v2.11.8+73 |
| Control dependency bindings | Medium | ~100+ additional callbacks |
| React roots (color pickers) | Medium | ~40+, have destroy but not called on section close |
| **Sortable destroy** | ✅ Fixed | v2.11.8+72 - Proper cleanup implemented |
| **Repeater destroy** | ✅ Fixed | v2.11.8+71 - Comprehensive cleanup implemented |

### Estimated Memory Costs

| Resource Type | Estimated Size | Priority to Fix |
|---------------|----------------|-----------------|
| **Select2 Google Fonts dropdowns** | ✅ Optimized | Custom DataAdapter implemented (v2.11.8+77) |
| JavaScript closures & bindings (340+) | **Megabytes** | 🔴 High (but breaks instant preview) |
| React component state & roots | **Hundreds of KB** | 🟡 Medium |
| Dynamic `<style>` elements (DOM overhead) | ~100KB | ✅ Low priority |
| CSS text in style elements | ~50KB | ✅ Low priority |

> [!NOTE]
> The Select2 Google Fonts optimization (v2.11.8+77) implemented a custom DataAdapter that avoids `$.extend()` data copying. Expected memory reduction: ~7-8MB → ~500KB-1MB. Actual savings should be verified via Chrome DevTools heap snapshot.

**Bottom line**: All controls now have proper destroy methods, but:
1. Destroy is only called on explicit control removal (rare)
2. ✅ Sortable and Repeater controls now have destroy methods (v2.11.8+71-72)

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

1. ~~**Add destroy method to `repeater-control.ts`**~~ ✅ DONE (v2.11.8+71)

2. ~~**Add destroy method to `sortable-control.ts`**~~ ✅ DONE (v2.11.8+72)

### Priority 2: Quick Wins

3. **Fix hook accumulation in `typography-control.ts`** ✅ DONE (v2.11.8+73)
   - Moved `wp.hooks.addAction()` outside of `composeFontProperties()` function
   - Hook now registered once per control, not on every font change

4. **Add WooCommerce conditional loading** ✅ DONE (v2.11.8+74)
   - Added `wpbfIsWooActive` check in `postmessage.ts`
   - Saves ~35 bindings when WooCommerce not active

5. **Consolidate responsive style tags** ✅ DONE (v2.11.8+75)
   - Added `writeResponsiveCSS()` to premium plugin utils.ts
   - Added `writeResponsiveCSSMultiSelector()` to theme customizer-util.ts
   - Updated premium plugin: `headings.ts`, `text.ts`
   - Updated theme: `logo.ts`, `tagline.ts`, `layout.ts`
   - Reduces 33 style tags to 11 (22 fewer DOM elements)

### Priority 3: Medium-Term Improvements

6. ~~**Implement lazy postMessage registration**~~ ❌ NOT DOABLE
   - ~~Create a registry of handlers per section~~
   - ~~Only `setting.bind()` when section is first expanded~~
   - ~~Store handlers as functions until needed~~
   
   > [!CAUTION]
   > **Breaks instant preview.** The preview iframe's `postMessage` handlers expect settings to be bound at load time. Lazy registration creates a timing mismatch where the preview is already listening but the parent frame's `setting.bind()` chain isn't established, causing instant preview to fail.

7. ~~**Add cleanup on section collapse**~~ ❌ NOT DOABLE (even worse than #6)
   - ~~Listen to `section.expanded.bind()` for collapse events~~
   - ~~Call control `destroy()` methods with debounce on collapse~~
   - ~~Re-embed controls on next expand~~
   
   > [!CAUTION]
   > **Even worse than #6 - completely breaks instant preview.** Destroying controls unbinds their setting callbacks. When re-embedded, the setting → preview communication chain is broken or creates duplicate/orphaned bindings. Tested and confirmed: many instant previews stop working after section collapse/expand cycles.

### Priority 4: Long-Term Architecture

8. ~~**Split postMessage handlers into dynamic imports**~~ ❌ NOT DOABLE
   - ~~Convert each postmessage-parts file to dynamic `import()`~~
   - ~~Load only when corresponding customizer section is accessed~~
   
   > [!CAUTION]
   > **Network latency breaks instant preview.** When user expands a section, dynamic imports create network delay (100-500ms+) before handlers are registered. During this window, setting changes produce no preview update. Users would need to change settings twice - once to trigger the load, once to actually see the preview. Same fundamental problem as #6, but with external network dependency making timing even less predictable.

9. ~~**Create unified style management**~~ ❌ NOT WORTH IT
   - ~~Single style element with consolidated CSS rules~~
   - ~~Batch updates on requestAnimationFrame~~
   - ~~Remove individual style tags approach~~
   
   > [!CAUTION]
   > **Low ROI - High effort, minimal memory impact.** The 400-500 style elements contribute ~150KB total (DOM overhead + CSS text), which is negligible compared to JavaScript closures and bindings (megabytes). Migrating 30+ postmessage handler files for ~150KB savings is not worthwhile. The real memory issues are the callback bindings (#6, #7), which have been proven to break instant preview and are marked NOT DOABLE.

---

## Files to Review

### Previously Critical (Now Fixed)
- `Customizer/Controls/Sortable/src/sortable-control.ts` - ✅ Has destroy (v2.11.8+72)
- `Customizer/Controls/Repeater/src/repeater-control.ts` - ✅ Has destroy (v2.11.8+71)

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
