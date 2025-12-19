# Progress Handoff: Fix menu_overlay PostMessage in Header Builder

**Current Session:** v2.11.8+3
**Date:** December 19, 2024
**Status:** Active

---

## Project Rules

See `ai-docs/wpbf-premium/rules.md` for project-specific guidelines and workflows.

---

## Summary

The `menu_overlay` and `menu_overlay_color` settings do not have working instant preview (postMessage) when Header Builder is enabled. They work correctly in non-header builder (legacy) mode.

---

## Recent Accomplishments (v2.11.8+2)

### Desktop Off-Canvas Menu Font Colors Feature
- ✅ Added `wpbf_header_builder_desktop_offcanvas_menu_font_colors` multicolor control
- ✅ Added CSS output with proper selectors
- ✅ Added postMessage handler for live preview
- ✅ Build succeeded

### Files Modified (v2.11.8+2)
| File | Change |
|------|--------|
| `wp-content/plugins/wpbf-premium/inc/customizer/controls/settings-header-builder.php` | Added multicolor control (lines 135-150) |
| `wp-content/plugins/wpbf-premium/inc/customizer/styles.php` | Added CSS output (lines 845-876) |
| `wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage-parts/navigation.ts` | Added postMessage handler (lines 323-350) |

---

## Pending Tasks

1. **Debug `menu_overlay` postMessage** - Investigate why instant preview doesn't work in Header Builder mode
2. **Debug `menu_overlay_color` postMessage** - Same issue as above

---

## Known Issue Details

**Problem:** The instant preview for `menu_overlay` and `menu_overlay_color` works in non-header builder mode but NOT in Header Builder mode.

**Root Cause Analysis Needed:**
- In `wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage-parts/navigation.ts` (lines 285-321), the handlers for these settings explicitly skip execution when header builder is enabled:
  ```typescript
  if (headerBuilderEnabled(customizer)) return;
  ```
- There should be corresponding handlers in the theme's postmessage files for Header Builder mode, but they may be missing or not working.

**Files to Investigate:**
- `wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage-parts/navigation.ts` - Legacy handlers
- `wp-content/themes/page-builder-framework/inc/customizer/js/postmessage-parts/` - Theme postmessage files
- Check if Header Builder mode has its own handlers for these settings

**Reference:** Non-header builder version works - compare the implementation.

---

## Notes

- Build command: `pnpm run build-postmessage`
- Output: `js/postmessage.js`
