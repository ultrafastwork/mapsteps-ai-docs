# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Add a `destroy()` method to `sortable-control.ts` to fix memory leak issues.

**Status**: Session v2.11.8+72 - Implement destroy method for Sortable control.

---

## Task Details

### Background

The Sortable control is identified as a **memory leak source** (see `ai-docs/page-builder-framework/memory-issues.md`). It extends `wp.customize.Control` directly but has **no destroy method**, despite creating:

- jQuery Sortable instances
- Click event handlers on visibility icons

### Objective

Add a `destroy()` method to `Customizer/Controls/Sortable/src/sortable-control.ts` that properly cleans up all resources.

### Implementation Requirements

1. **Destroy jQuery Sortable**:
   ```typescript
   this.container?.find("ul.sortable").sortable("destroy");
   ```

2. **Unbind container events**:
   ```typescript
   this.container?.off();
   ```

3. **Add removed event handler** (follow repeater-control.ts pattern):
   - Bind to "removed" event in ready()
   - Call destroy() when this control is removed

### Files to Modify

- `Customizer/Controls/Sortable/src/sortable-control.ts`

### Reference Files

- `ai-docs/page-builder-framework/memory-issues.md` - Full analysis
- `Customizer/Controls/Repeater/src/repeater-control.ts` - Example of destroy implementation

---

## Previous Session Summary (v2.11.8+71)

✅ Added `destroy()` method to `repeater-control.ts`
✅ Implemented cleanup for jQuery Sortable, container events, wp.media frames, color pickers, row objects
✅ Added removed event handler to trigger destroy on control removal
✅ Built controls bundle successfully

---

## Pending Tasks (v2.11.8+72)

- [x] Implement `destroy()` method for `sortable-control.ts`
- [x] Test that destroy method properly cleans up resources

---

## Recent Completed

- ✅ Repeater Control Destroy Method (v2.11.8+71)
- ✅ Footer Builder Buttons & Margin Controls (v2.11.8+69)
- ✅ Handoff Documentation (v2.11.8+68)
- ✅ "Sticky Footer" Field Reordering (v2.11.8+67)
