# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Consolidate responsive style tags in postmessage handlers.

**Status**: Session v2.11.8+75 - Responsive style tag consolidation.

---

## Task Details

### Background

The postmessage handlers create separate `<style>` tags for each responsive breakpoint (desktop, tablet, mobile). This results in ~400-500 style elements in the DOM. Consolidating these into single style tags with media queries would reduce DOM pollution.

### Objective

Modify `writeCSS()` usage in postmessage handlers to use single style tags with media queries instead of 3 separate calls per responsive field.

### Implementation Requirements

1. **Analyze current pattern**:
   - Look at `headings.ts` and similar files in `inc/customizer/js/postmessage-parts/`
   - Identify responsive fields that make 3 separate `writeCSS()` calls

2. **Implement consolidated approach**:
   - Modify `writeCSS()` or create a new utility function for responsive CSS
   - Use media queries within a single style tag instead of 3 separate tags

3. **Test**:
   - Verify responsive preview still works correctly
   - Verify style changes apply at correct breakpoints

### Files to Review

- `inc/customizer/js/customizer-util.ts` - Contains `writeCSS()` function
- `inc/customizer/js/postmessage-parts/headings.ts` - Example of responsive handling

### Reference Files

- `ai-docs/page-builder-framework/memory-issues.md`

---

## Previous Session Summary (v2.11.8+74)

✅ Added WooCommerce conditional loading in `postmessage.ts`
✅ Added `wpbfIsWooActive` PHP flag in `customizer-functions.php`
✅ Saves ~35 bindings when WooCommerce is not active

---

## Recent Completed

- ✅ WooCommerce Conditional Loading (v2.11.8+74)
- ✅ Typography Control Hook Fix (v2.11.8+73)
- ✅ Sortable Control Destroy Method (v2.11.8+72)
- ✅ Repeater Control Destroy Method (v2.11.8+71)
