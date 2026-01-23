# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Create a Custom Select2 DataAdapter to eliminate data duplication for Google Fonts dropdowns.

**Status**: Session v2.11.8+77 - Custom Select2 DataAdapter for Typography Controls.

---

## Task Details

### Background

The WordPress Customizer has 24 Select2 instances for Google Fonts (font-family and variant fields in typography controls). Currently, Select2 **copies the entire ~200KB font data array** for each instance via `$.extend()` in its `_normalizeItem()` function. This results in **~7-8MB of memory consumption** just for Google Fonts dropdowns.

### The Problem

See detailed analysis in: `ai-docs/page-builder-framework/typography-controls-memory-analysis.md`

Key finding: Select2's ArrayAdapter does NOT keep a reference to the provided data array. It iterates through and creates NEW JavaScript objects plus DOM `<option>` elements for each item, for each instance.

### Objective

Create a **Custom Select2 DataAdapter** that:
1. Reads directly from the global `wpbfGoogleFonts` array WITHOUT copying
2. Does NOT create 1000+ `<option>` DOM elements per instance
3. Shares a single data source across all 24 instances

### Expected Outcome

- Memory reduction from ~7-8MB to ~500KB-1MB for Google Fonts
- No change to user experience - dropdowns work exactly the same
- Font data is already loaded with the page - INSTANT display (no AJAX)

### Implementation Strategy

1. **Research Select2 Custom DataAdapter pattern**:
   - Study `node_modules/select2/src/js/select2/data/array.js`
   - Study `node_modules/select2/src/js/select2/data/select.js`
   - Understand how to extend/override the ArrayAdapter

2. **Create SharedFontDataAdapter**:
   - Override `query()` to filter from global array without copying
   - Override `current()` to return selected items without copying
   - Avoid calling `_normalizeItem()` or `$.extend()` on each item
   - Skip DOM `<option>` creation (use custom rendering)

3. **Integration**:
   - Modify `select-control.ts` to use the custom adapter when `choicesGlobalVar` is set
   - Ensure it works with existing typography control workflow

4. **Fix existing mutation bug** (optional but recommended):
   - In `select-control.ts` lines 131-146, the global array is mutated to set `selected: true`
   - This should be fixed to track selection state separately

### Files to Modify

- `Customizer/Controls/Select/src/select-control.ts` - Main control
- Create new file: `Customizer/Controls/Select/src/shared-font-data-adapter.ts` (or similar)

### Reference Files

- `ai-docs/page-builder-framework/typography-controls-memory-analysis.md` - Full analysis
- `ai-docs/page-builder-framework/memory-issues.md` - Memory consumption overview
- `node_modules/select2/src/js/select2/data/array.js` - Select2 ArrayAdapter source
- `node_modules/select2/src/js/select2/data/select.js` - Select2 SelectAdapter source

### Build Command

After implementation: `pnpm build-controls-bundle`

---

## Previous Session Summary (v2.11.8+76)

Session v2.11.8+76 was used for research/analysis only:
- ✅ Deep technical analysis of Select2 and Choices.js memory behavior
- ✅ Created `typography-controls-memory-analysis.md` documenting findings
- ✅ Confirmed both libraries clone data internally - switching would NOT help
- ✅ Identified Custom DataAdapter as the reliable solution (no network dependency)

---

## Recent Completed

- ✅ Typography Controls Memory Analysis (v2.11.8+76)
- ✅ Responsive Style Tag Consolidation (v2.11.8+75)
- ✅ WooCommerce Conditional Loading (v2.11.8+74)
- ✅ Typography Control Hook Fix (v2.11.8+73)
- ✅ Sortable Control Destroy Method (v2.11.8+72)
- ✅ Repeater Control Destroy Method (v2.11.8+71)
