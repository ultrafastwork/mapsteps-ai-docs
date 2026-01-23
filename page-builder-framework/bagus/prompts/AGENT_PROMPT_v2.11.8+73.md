# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Fix hook accumulation bug in `typography-control.ts`.

**Status**: Session v2.11.8+73 - Fix typography control hook accumulation.

---

## Task Details

### Background

The Typography control has a hook accumulation bug (see `ai-docs/page-builder-framework/memory-issues.md`). Every time `composeFontProperties()` runs (on every font-family change), it adds a new WordPress hook action, causing memory leaks.

### Objective

Fix the hook accumulation issue in `Customizer/Controls/Typography/src/typography-control.ts` by moving `wp.hooks.addAction()` outside of the `composeFontProperties()` function.

### Implementation Requirements

1. **Identify the problematic pattern**:
   - Look for `wp.hooks.addAction()` calls inside `composeFontProperties()`
   - These should only be registered once, not on every font change

2. **Move hook registration**:
   - Move hook registration to control initialization (outside the change handler)
   - Ensure hooks are registered only once per control lifetime

3. **Test**:
   - Verify font-family changes work correctly
   - Verify no duplicate hook registrations

### Files to Modify

- `Customizer/Controls/Typography/src/typography-control.ts`

### Reference Files

- `ai-docs/page-builder-framework/memory-issues.md` - Full analysis (lines 57-77)

---

## Previous Session Summary (v2.11.8+72)

✅ Added `destroy()` method to `sortable-control.ts`
✅ All Priority 1 memory leak fixes are now complete

---

## Pending Tasks (v2.11.8+73)

- [ ] Fix hook accumulation in `typography-control.ts`
- [ ] Build controls bundle
- [ ] Test font-family changes work correctly

---

## Recent Completed

- ✅ Sortable Control Destroy Method (v2.11.8+72)
- ✅ Repeater Control Destroy Method (v2.11.8+71)
- ✅ Footer Builder Buttons & Margin Controls (v2.11.8+69)
