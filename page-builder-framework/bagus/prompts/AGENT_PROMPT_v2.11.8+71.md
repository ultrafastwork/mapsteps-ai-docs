# Agent Prompt v2.11.8+71

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Add a `destroy()` method to `repeater-control.ts` to fix memory leak issues.

**Status**: Session v2.11.8+71 - Implement destroy method for Repeater control.

---

## Task Details

### Background

The Repeater control is identified as a **critical memory leak source** (see `ai-docs/page-builder-framework/memory-issues.md`). It extends `wp.customize.Control` directly but has **no destroy method**, despite creating:

- jQuery Sortable instances
- Multiple container event handlers (6+)
- wp.media frames
- wpColorPicker instances
- Row objects with their own event handlers

### Objective

Add a `destroy()` method to `Customizer/Controls/Repeater/src/repeater-control.ts` that properly cleans up all resources.

### Implementation Requirements

1. **Destroy jQuery Sortable**:
   ```typescript
   this.repeaterFieldsContainer?.sortable("destroy");
   ```

2. **Unbind container events**:
   ```typescript
   this.container?.off();
   ```

3. **Destroy wp.media frame**:
   ```typescript
   this.frame?.dispose?.();
   // or this.frame?.remove?.();
   ```

4. **Destroy color pickers**:
   ```typescript
   this.container?.find(".color-picker-hex").wpColorPicker("destroy");
   ```

5. **Clean up row objects**: 
   - If rows have their own event handlers, unbind them
   - Clear any references to row objects

### Files to Modify

- `Customizer/Controls/Repeater/src/repeater-control.ts` (~950 lines)

### Reference Files

- `ai-docs/page-builder-framework/memory-issues.md` - Full analysis
- `Customizer/Controls/Sortable/src/sortable-control.ts` - Similar control needing destroy
- `Customizer/Controls/Base/src/base-control.ts` - Base control with basic destroy pattern
- `Customizer/Controls/Color/src/ColorControl.tsx` - Example of proper destroy pattern

---

## Previous Session Summary (v2.11.8+69-70)

✅ Added "Button 1" & "Button 2" widgets to Footer Builder.
✅ Implemented non-responsive margin controls for all button widgets.
✅ Built postmessage bundle successfully.

---

## Pending Tasks (v2.11.8+71)

- [ ] Implement `destroy()` method for `repeater-control.ts`
- [ ] Test that destroy method properly cleans up resources
- [ ] Consider adding destroy to `sortable-control.ts` as follow-up (Priority 2 task)

---

## Recent Completed

- ✅ Footer Builder Buttons & Margin Controls (v2.11.8+69)
- ✅ Handoff Documentation (v2.11.8+68)
- ✅ "Sticky Footer" Field Reordering (v2.11.8+67)
- ✅ Footer Separator Controls Refactor (v2.11.8+65)
