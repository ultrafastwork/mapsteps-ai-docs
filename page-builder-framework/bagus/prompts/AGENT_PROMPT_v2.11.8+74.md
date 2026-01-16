# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Add WooCommerce conditional loading to postmessage.ts.

**Status**: Session v2.11.8+74 - WooCommerce conditional loading.

---

## Task Details

### Background

The `postmessage.ts` file calls `woocommerceSetup()` unconditionally, creating ~35 bindings even when WooCommerce is not active. This wastes resources.

### Objective

Add a check to only call `woocommerceSetup()` when WooCommerce is active.

### Implementation Requirements

1. **Find the WooCommerce setup call**:
   - Look for `woocommerceSetup()` call in `inc/customizer/js/postmessage.ts`

2. **Add conditional check**:
   - Check if WooCommerce is active before calling `woocommerceSetup()`
   - Use a PHP-provided flag or check for WooCommerce-specific elements

3. **Test**:
   - Verify WooCommerce preview still works when WooCommerce is active
   - Verify no errors when WooCommerce is not active

### Files to Modify

- `inc/customizer/js/postmessage.ts`

### Reference Files

- `ai-docs/page-builder-framework/memory-issues.md`

---

## Previous Session Summary (v2.11.8+73)

✅ Fixed hook accumulation in `typography-control.ts`
✅ Moved `wp.hooks.addAction()` from `composeFontProperties()` to `setupTypographyFields()`

---

## Pending Tasks (v2.11.8+74)

- [ ] Add WooCommerce conditional loading in `postmessage.ts`
- [ ] Build postmessage bundle
- [ ] Test WooCommerce preview functionality

---

## Recent Completed

- ✅ Typography Control Hook Fix (v2.11.8+73)
- ✅ Sortable Control Destroy Method (v2.11.8+72)
- ✅ Repeater Control Destroy Method (v2.11.8+71)
