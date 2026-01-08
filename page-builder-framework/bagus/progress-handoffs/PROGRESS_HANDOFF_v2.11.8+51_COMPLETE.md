# Progress Handoff

**Date**: 2026-01-08
**Status**: Completed
**Last Completed Session**: v2.11.8+51
**Current Session**: v2.11.8+52
**Archive**: See `PROGRESS_HANDOFF_v2.11.8+49_COMPLETE.md` for Footer Builder row content filter.

## 1. Current State Summary

**Completed Tasks**:

- ✅ Header settings refactoring verified
- ✅ Typography settings refactoring verified
- ✅ General settings refactoring verified
- ✅ Blog settings refactoring verified
- ✅ CSS class naming refactored (v2.11.8+43)
- ✅ CSS class refactoring testing (v2.11.8+44)
- ✅ Footer Builder implementation (v2.11.8+45)
- ✅ Footer Builder controls movement (v2.11.8+46)
- ✅ Footer Builder postmessage support (v2.11.8+47)
- ✅ Footer Builder CSS output (v2.11.8+48)
- ✅ Footer Builder row content filter (v2.11.8+49)
- ✅ Footer Builder vs Header Builder verification (v2.11.8+50)
- ✅ Header Builder regression fix (v2.11.8+51)

**Codebase Health**: All settings files use modular structure. Footer Builder complete. Header Builder regression fixed.

## 2. Session v2.11.8+51 Accomplishments

Fixed **Header Builder regression** caused by Footer Builder introduction. The builder controls were using global selectors that caused cross-contamination between header and footer builders.

### Root Cause

Two issues in `Customizer/Controls/Builder/src/responsive-builder-control.ts` and `builder-control.ts`:

1. **Hardcoded Section Prefix**: `handleRowSettingClick()` and `bindCustomizeSection()` used hardcoded `wpbf_header_builder_` prefix instead of dynamic `this.params.id`.

2. **Global Sortable Selectors**: `initSortable()` used global jQuery selectors like `jQuery(".active-widgets")` which selected elements from ALL builder panels, causing:
   - Widgets could be sorted across different builders
   - The `update` callback fired on wrong control instance
   - Values weren't saved correctly

### Fix Applied

#### 1. Dynamic Section Prefix

**Before:**
```typescript
handleRowSettingClick: function (rowKey) {
    customizer?.section(`wpbf_header_builder_${rowKey}_section`, ...);
}
```

**After:**
```typescript
handleRowSettingClick: function (rowKey) {
    const controlId = this.params?.id;
    if (!controlId) return;
    customizer?.section(`${controlId}_${rowKey}_section`, ...);
}
```

#### 2. Scoped Sortable Initialization

**Before:**
```typescript
jQuery(".active-widgets:not(.wpbf-premium-locked-dropzone)").sortable({
    connectWith: ".active-widgets:not(.wpbf-premium-locked-dropzone)",
```

**After:**
```typescript
const $builderPanel = jQuery(this.builderPanel);
const $activeWidgets = $builderPanel.find(".active-widgets:not(.wpbf-premium-locked-dropzone)");
$activeWidgets.sortable({
    connectWith: $activeWidgets,
```

### Files Modified

| File | Changes |
|------|---------|
| `Customizer/Controls/Builder/src/responsive-builder-control.ts` | Fixed `handleRowSettingClick`, `bindCustomizeSection`, `initSortable` |
| `Customizer/Controls/Builder/src/builder-control.ts` | Fixed `handleRowSettingClick`, `bindCustomizeSection`, `initSortable` |
| `Customizer/Controls/Bundle/dist/controls-bundle-min.js` | Rebuilt |

## 3. Pending Tasks (v2.11.8+52)

1. **Manual Testing** - Verify Header Builder widget movement works in Customizer:
   - Add widgets to rows
   - Move widgets between columns
   - Verify instant preview updates
   - Save and verify frontend renders correctly

2. **Footer Builder Testing** - Verify Footer Builder still works correctly after fix

3. **Regression Testing** - Ensure no other builder functionality was affected

## 4. Notes

- The regression was introduced when Footer Builder was added because both builders share the same `ResponsiveBuilderControl` class
- The fix ensures each builder instance operates independently with its own scoped selectors
- Built with `pnpm run build-controls-bundle`
