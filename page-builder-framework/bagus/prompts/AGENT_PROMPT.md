# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Implement lazy postMessage registration for Customizer.

**Status**: Session v2.11.8+76 - Lazy postMessage registration.

---

## Task Details

### Background

All 340+ postMessage bindings are registered at customizer load, regardless of which sections the user opens. This consumes memory upfront. Implementing lazy registration would defer binding until sections are first expanded.

### Objective

Implement lazy postMessage registration so handlers are only bound when their corresponding section is first opened.

### Implementation Requirements

1. **Analyze current registration pattern**:
   - Review `postmessage.ts` entry point
   - Understand how sections map to handler files

2. **Design lazy registration approach**:
   - Create a registry mapping section IDs to handler functions
   - Listen to `section.expanded` events
   - Register handlers on first section expand

3. **Implement and test**:
   - Ensure handlers still work correctly after lazy registration
   - Verify initial values are applied when section opens

### Files to Review

- `inc/customizer/js/postmessage.ts` - Entry point
- `inc/customizer/js/postmessage-parts/*.ts` - Handler files

### Reference Files

- `ai-docs/page-builder-framework/memory-issues.md`

---

## Previous Session Summary (v2.11.8+75)

**Premium Plugin:**
✅ Added `writeResponsiveCSS()` to utils.ts
✅ Updated `headings.ts` (18 → 6 tags) and `text.ts` (3 → 1 tags)

**Theme:**
✅ Added `writeResponsiveCSSMultiSelector()` to customizer-util.ts
✅ Updated `logo.ts` (6 → 2 tags), `tagline.ts` (3 → 1 tags), `layout.ts` (3 → 1 tags)

**Total reduction**: 33 → 11 style tags (22 fewer DOM elements)

---

## Recent Completed

- ✅ Responsive Style Tag Consolidation (v2.11.8+75)
- ✅ WooCommerce Conditional Loading (v2.11.8+74)
- ✅ Typography Control Hook Fix (v2.11.8+73)
- ✅ Sortable Control Destroy Method (v2.11.8+72)
- ✅ Repeater Control Destroy Method (v2.11.8+71)
