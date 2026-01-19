# Typography Controls Memory Usage Analysis

> **Analysis Date**: 2026-01-19  
> **Status**: ✅ **RESOLVED** (v2.11.8+77) - Custom DataAdapter Implemented

This document provides a deep technical analysis of memory consumption issues related to Typography controls using Select2 for Google Fonts selection in the WordPress Customizer.

---

## Executive Summary

Both **Select2** and **Choices.js** internally **clone/copy** provided data arrays. Neither library maintains a direct reference to a shared global object. This means the current optimization of using a `choicesGlobalVar` to avoid server-side duplicate output **does not prevent JavaScript-side memory duplication**.

**Key findings:**
- Select2 creates ~200KB of internal data copies **per instance** (24 instances = ~4.8MB)
- Select2 also creates ~1000 DOM `<option>` elements **per instance** (~2.4MB additional)
- Choices.js exhibits the **same data cloning behavior** - switching libraries would NOT solve the memory issue
- ✅ **RESOLVED**: Custom `SharedFontDataAdapter` implemented (v2.11.8+77)

### Solution Implemented (v2.11.8+77)

Created `SharedFontDataAdapter` in `Customizer/Controls/Select/src/shared-font-data-adapter.ts`:
- Extends ArrayAdapter, overrides `_normalizeItem()` to avoid `$.extend()` copying
- Pre-processes data with selection state without mutating the global font array
- **Fixed bug**: Removed global array mutation in `select-control.ts`
- Expected memory reduction: ~7-8MB → ~500KB-1MB

---

## 1. Select2 Memory Behavior Analysis

### 1.1 How Select2 Handles Data Internally

**Source files analyzed:**
- [array.js](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/select2/src/js/select2/data/array.js)
- [select.js](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/select2/src/js/select2/data/select.js)

#### Data Flow

1. **Initial data storage** (array.js:7):
   ```javascript
   this._dataToConvert = options.get('data') || [];
   ```
   This stores a **reference** to the input array initially.

2. **Data conversion** (array.js:34-80):
   ```javascript
   ArrayAdapter.prototype.convertToOptions = function (data) {
     for (var d = 0; d < data.length; d++) {
       var item = this._normalizeItem(data[d]);
       // ...
       var $option = this.option(item);
       $options.push($option);
     }
     return $options;
   };
   ```

3. **Data normalization creates NEW objects** (select.js:252-282):
   ```javascript
   SelectAdapter.prototype._normalizeItem = function (item) {
     item = $.extend({}, { text: '' }, item);  // Creates a SHALLOW COPY
     // ...
     return $.extend({}, defaults, item);  // Creates ANOTHER copy
   };
   ```

4. **DOM element creation** (select.js:163-202):
   ```javascript
   SelectAdapter.prototype.option = function (data) {
     option = document.createElement('option');
     option.textContent = data.text;
     // ...
     Utils.StoreData(option, 'data', normalizedData);  // Stores data on DOM element
     return $(option);
   };
   ```

### 1.2 Memory Impact Summary

| Resource | Per Instance | × 24 Instances | Total |
|----------|-------------|----------------|-------|
| JavaScript data copy via `$.extend()` | ~200KB | 24 | **~4.8MB** |
| DOM `<option>` elements (~1000 fonts) | ~100KB | 24 | **~2.4MB** |
| Select2 internal state/callbacks | ~7KB | 24 | ~170KB |
| **Total** | | | **~7.4MB** |

### 1.3 Confirmed: Select2 Clones Data

> [!CAUTION]
> **Select2 does NOT keep a reference to the global array.**  
> Every call to `.select2({ data: choicesFromGlobalVar })` creates:
> 1. New JavaScript objects via `$.extend()` for each of the ~1000 font items
> 2. New DOM `<option>` elements for each item
> 3. jQuery data stored on each `<option>` element

---

## 2. Choices.js Memory Behavior Analysis

### 2.1 How Choices.js Handles Data Internally

**Source files analyzed:**
- [choices.ts](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/choices.js/src/scripts/choices.ts)
- [choice-input.ts](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/choices.js/src/scripts/lib/choice-input.ts)
- [store.ts](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/choices.js/src/scripts/store/store.ts)

#### Data Flow

1. **`setChoices()` method** (choices.ts:726-766):
   ```typescript
   choicesArrayOrFetcher.forEach((groupOrChoice) => {
     if ('choices' in groupOrChoice) {
       this._addGroup(mapInputToChoice<InputGroup>(group, true));
     } else {
       const choiceFull = mapInputToChoice<InputChoice>(choice, false);
       this._addChoice(choiceFull);
     }
   });
   ```

2. **`mapInputToChoice()` creates NEW objects** (choice-input.ts:70-85):
   ```typescript
   const result: ChoiceFull = {
     id: 0,
     group: null,
     score: 0,
     rank: 0,
     value: choice.value,
     label: choice.label || choice.value,
     active: coerceBool(choice.active),
     selected: coerceBool(choice.selected, false),
     disabled: coerceBool(choice.disabled, false),
     // ... more properties
   };
   return result;
   ```

3. **Store maintains copies** (store.ts:33-38):
   ```typescript
   get defaultState(): State {
     return {
       groups: [],
       items: [],
       choices: [],  // All ChoiceFull objects are stored here
     };
   }
   ```

4. **DOM element creation** (choices.ts:954-957):
   ```typescript
   if (this._isSelectElement) {
     const backingOptions = activeChoices.filter((choice) => !choice.element);
     if (backingOptions.length) {
       (this.passedElement as WrappedSelect).addOptions(backingOptions);
     }
   }
   ```

### 2.2 Choices.js Memory Comparison

| Aspect | Select2 | Choices.js |
|--------|---------|------------|
| **Data cloning** | ✅ Yes (`$.extend()`) | ✅ Yes (new objects) |
| **DOM `<option>` creation** | ✅ Yes (all items) | ✅ Yes (visible items) |
| **Internal state store** | Limited | Full Redux-like store |
| **Virtual rendering** | ❌ No | ❌ No (can limit render count) |

### 2.3 Key Insight: Same Problem

> [!IMPORTANT]
> **Choices.js has the same data duplication problem as Select2.**
> 
> Both libraries:
> - Create new JavaScript objects for each choice item
> - Do NOT keep references to shared/global data arrays
> - Create DOM elements for choices
> 
> **Switching from Select2 to Choices.js would NOT reduce memory usage.**

---

## 3. Current Implementation Analysis

### 3.1 PHP-Side Optimization (Working)

[TypographyField.php](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/Customizer/Controls/Typography/TypographyField.php) already implements a partial optimization:

```php
// Lines 109-121 - JS object printed ONCE regardless of field count
if ( ! TypographyStore::$control_vars_printed ) {
    wp_localize_script(
        'wpbf-controls-bundle', 
        'wpbfGoogleFonts', 
        ( new GoogleFontsUtil() )->getCollections()
    );
    TypographyStore::$control_vars_printed = true;
}
```

**Benefit**: Prevents ~200KB of JSON being output 24 times in the HTML response.

### 3.2 JavaScript-Side Problem (Not Fixed)

[select-control.ts](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/Customizer/Controls/Select/src/select-control.ts) has two issues:

**Issue 1: Global array mutation** (lines 131-146):
```typescript
// ⚠️ BUG: This mutates the GLOBAL array!
choicesFromGlobalVar.forEach((choice, index) => {
    if (choice.id && values.includes(choice.id)) {
        choicesFromGlobalVar[index].selected = true;  // Pollutes global!
    }
});
```

**Issue 2: Data passed to Select2** (lines 149-158):
```typescript
$selectbox?.select2({
    // Select2 will COPY this entire array internally
    data: choicesFromGlobalVar ?? params.choices,
});
```

---

## 4. Would Switching to Choices.js Help?

### 4.1 Short Answer: No

Both libraries have fundamentally the same architecture that causes data duplication:

| Factor | Select2 | Choices.js | Winner |
|--------|---------|------------|--------|
| Data cloning | ~200KB per instance | ~200KB per instance | Tie |
| DOM elements | All ~1000 items | Can limit render count | Choices.js (slight) |
| Bundle size | ~80KB | ~60KB | Choices.js |
| jQuery dependency | Required | None | Choices.js |
| Virtual scrolling | ❌ No | ❌ No | Tie |
| Memory with 24 instances | ~7-8MB | ~6-7MB (estimated) | Tie |

### 4.2 Potential Marginal Benefits of Choices.js

1. **No jQuery dependency** - Slightly smaller footprint
2. **`renderChoiceLimit` option** - Can limit initial DOM rendering
3. **AJAX/fetch support** - Built-in remote data fetching
4. **Modern TypeScript codebase** - Easier to understand/modify

### 4.3 Conclusion

> [!WARNING]
> **Switching to Choices.js is NOT a solution to the memory problem.**
> 
> The ~7-8MB memory consumption is caused by the architectural pattern of:
> 1. Loading all ~1000 fonts into memory upfront
> 2. Creating 24 separate Select2/Choices instances
> 3. Each instance cloning the full dataset
> 
> This problem exists in both libraries.

---

## 5. Recommended Architectural Approaches

> [!IMPORTANT]
> **Critical Constraint**: When the user clicks a dropdown, fonts MUST be visible immediately. No loading states, no "please wait", no empty results. Any solution that depends on network timing at the moment of user interaction is unreliable.

### 5.1 Custom DataAdapter (Recommended - Select2)

**Concept**: Create a custom Select2 DataAdapter that shares a single data source across all 24 instances without copying.

**Implementation**:
```typescript
class SharedFontDataAdapter extends $.fn.select2.amd.require('select2/data/array') {
  // Override query() to filter from shared global without copying
  // Override current() to return selected items without copying
  // Skip _normalizeItem() / $.extend() on each item
  // Track selection state externally, not on the data objects
}
```

**Benefits**:
- One copy of font data in memory (~200KB total, not ~4.8MB)
- Works with existing global variable optimization
- No server-side changes needed
- No network dependency - fonts are already loaded - INSTANT display
- **Expected savings: ~7MB → ~500KB-1MB**

**Trade-offs**:
- Requires understanding Select2 DataAdapter internals
- Selection state management becomes separate from data
- May need custom rendering to avoid DOM `<option>` creation

### 5.2 Single Shared Dropdown Instance

**Concept**: Only ONE Select2 dropdown exists globally. All 24 font-family fields share this single instance.

**Implementation**:
- Create one hidden Select2 dropdown at page load
- When user clicks any font-family field → reposition and show the shared dropdown
- Dropdown is positioned next to the clicked field
- On selection, update the corresponding field's setting

**Benefits**:
- Memory: ~300KB instead of ~7MB
- No network dependency - INSTANT display

**Trade-offs**:
- Tricky positioning logic
- Complex event handling for 24 different fields
- May affect accessibility (focus management)

### 5.3 Virtualized/Windowed Rendering

**Concept**: Only render DOM elements for visible items in the dropdown (typically 10-20 items).

**Benefits**:
- DOM element count drops from ~1000 to ~20 per instance
- ~100KB DOM savings per instance

**Trade-offs**:
- Requires replacing Select2/Choices.js entirely
- Accessibility considerations for screen readers
- May not address the JavaScript data duplication issue

### 5.4 Approaches NOT Recommended

#### ❌ AJAX Lazy Loading

**Why it fails**: User opens customizer → expands section → clicks dropdown while AJAX is loading → **empty dropdown**. Network latency varies wildly (10ms to 5000ms+), making this unreliable worldwide.

#### ❌ Preload on Section Expand

**Why it fails**: Same problem as AJAX - user may click dropdown before loading completes. Not all users have fast internet.

#### ❌ Lazy Control Initialization

**Why it fails**: Breaks Customizer's postMessage preview system. Documented in [memory-issues.md](file:///c:/www/mapsteps/ai-docs/page-builder-framework/memory-issues.md).

---

## 6. Ranking of Solutions

| Priority | Approach | Effort | Memory Savings | Reliability |
|----------|----------|--------|----------------|-------------|
| 1 | **Custom DataAdapter** | Medium | ~85% (~7MB → ~1MB) | ✅ 100% |
| 2 | Single Shared Dropdown | Medium-High | ~95% | ✅ 100% |
| 3 | Virtualized rendering | High | ~30% | ✅ 100% |
| 4 | ~~AJAX lazy loading~~ | — | — | ❌ Unreliable |


---

## 7. Reasoning for AI Agent Future Reference

### Why the current optimization doesn't work

The `choicesGlobalVar` approach only prevents the PHP server from outputting the same JSON 24 times. It reduces the initial HTML payload but does nothing for client-side memory because:

1. JavaScript receives ONE copy of `wpbfGoogleFonts` (~200KB) ✅ Good
2. Each of 24 Select2 instances calls `.select2({ data: wpbfGoogleFonts })`
3. Select2's ArrayAdapter does NOT store a reference to this array
4. Instead, it iterates through and creates NEW objects via `_normalizeItem()`
5. Each normalized object is then converted to a DOM `<option>` element
6. Result: 24 × 200KB data + 24 × 100KB DOM = ~7.2MB

### Why Choices.js wouldn't help

The Choices.js architecture follows the same pattern:

1. `setChoices()` receives the data array
2. For each item, it calls `mapInputToChoice()` which creates a NEW `ChoiceFull` object
3. These objects are dispatched to the internal Redux-like store
4. When backing a `<select>` element, it also creates DOM `<option>` elements
5. Result: Same data duplication problem

### The only real solutions require architectural changes

Any solution must address the root cause: **all ~1000 fonts are loaded into memory for each instance**.

Options:
1. **Don't load all fonts** → AJAX/lazy loading
2. **Share the loaded data** → Custom data adapter
3. **Don't render all fonts** → Virtualized rendering

---

## 8. Files Referenced in This Analysis

| File | Purpose |
|------|---------|
| [select2/data/array.js](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/select2/src/js/select2/data/array.js) | Select2 array data adapter |
| [select2/data/select.js](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/select2/src/js/select2/data/select.js) | Select2 base data handling, `_normalizeItem()` |
| [choices.js/choices.ts](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/choices.js/src/scripts/choices.ts) | Main Choices.js class, `setChoices()` |
| [choices.js/choice-input.ts](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/choices.js/src/scripts/lib/choice-input.ts) | `mapInputToChoice()` function |
| [choices.js/store.ts](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/node_modules/choices.js/src/scripts/store/store.ts) | Redux-like store implementation |
| [select-control.ts](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/Customizer/Controls/Select/src/select-control.ts) | Current Select2 control implementation |
| [TypographyField.php](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/Customizer/Controls/Typography/TypographyField.php) | PHP-side font field registration |
| [memory-issues.md](file:///c:/www/mapsteps/ai-docs/page-builder-framework/memory-issues.md) | Related memory analysis document |

---

*Analysis performed: 2026-01-19*
