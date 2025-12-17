# Progress Handoff

**Date**: 2025-12-17
**Status**: Completed
**Last Completed Session**: v2.11.8+30
**Current Session**: v2.11.8+31 (Sub Menu Settings - Header Builder Integration)
**Archive**: See `PROGRESS_HANDOFF_v2.11.8+30_PENDING.md` for CSS issues task (deferred).

## 1. Current State Summary

**Header Builder Status**: Fully functional with all 22 elements (11 Desktop + 11 Mobile) verified.

**Issue Fixed**: Sub Menu and Mobile Sub Menu sections are now visible when Header Builder is enabled.

## 2. Task Completed: Sub Menu Settings - Header Builder Integration

### Root Cause Found

The CSS in `Customizer/Controls/Builder/src/builder-control.scss` was hiding ALL section titles when Header Builder is enabled, except for `.builder-control-section`:

```scss
.customize-pane-child.control-panel-wpbf-builder {
	&.builder-is-shown
		> .control-subsection:not(.builder-control-section)
		> .accordion-section-title {
		display: none;
	}
}
```

This caused `wpbf_sub_menu_options` and `wpbf_mobile_sub_menu_options` sections to be hidden.

### Fix Applied

Updated the CSS selector to exclude Sub Menu sections from being hidden:

```scss
.customize-pane-child.control-panel-wpbf-builder {
	&.builder-is-shown
		> .control-subsection:not(.builder-control-section):not(#accordion-section-wpbf_sub_menu_options):not(#accordion-section-wpbf_mobile_sub_menu_options)
		> .accordion-section-title {
		display: none;
	}
}
```

### Files Modified

1. `Customizer/Controls/Builder/src/builder-control.scss` - Added `:not()` selectors for Sub Menu sections
2. `Customizer/Controls/Bundle/dist/controls-bundle-min.css` - Rebuilt CSS bundle

### Build Commands Used

```bash
pnpm run build-control --name=builder
pnpm run build-controls-bundle
```

## 3. Testing Instructions

1. Go to WordPress Customizer
2. Navigate to **Header** panel
3. Enable **Header Builder** toggle
4. Verify that **Sub Menu** and **Mobile Sub Menu** sections are visible in the Header panel
5. Click on each section and verify controls are accessible
6. Change some settings and verify they apply correctly to the frontend

## 4. Deferred Tasks

The following task was deferred and saved in `PROGRESS_HANDOFF_v2.11.8+30_PENDING.md`:
- **Visual CSS Issues**: Grey line above "Header Builder" section title, Toggle position slightly off when toggled off

## 5. Next Steps

1. Test the fix in the Customizer to confirm Sub Menu sections are visible
2. Commit the changes with appropriate message
3. Address the deferred CSS issues (see `PROGRESS_HANDOFF_v2.11.8+30_PENDING.md`)
