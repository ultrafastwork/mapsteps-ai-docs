# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin and "page-builder-framework" theme.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`
**Global Rules**: `.windsurfrules`

**Objective**: Fix issue number 3 from `ai-docs/page-builder-framework/issues.md`.

**Status**: Session v2.10.3+29 - Completed.

---

## Completed

- **Issue #3**: Hamburger Icon Customization on "Full Screen" Menu in Non-Header Builder - ✅ FIXED (both color and size)

---

## Accomplishments

### Icon Color Fix (wpbf-premium)
- Fixed the `menu_off_canvas_hamburger_color` setting selector from `.wpbf-nav-item, .wpbf-nav-item a` to `.wpbf-menu-toggle`
- Updated both PHP styles and postMessage handler
- Built the postmessage.js file

### Icon Size Fix (page-builder-framework)
- Fixed CSS cascade conflict where theme's `wpbf_header_builder_desktop_menu_trigger_icon_size` style tag overrode premium's `menu_off_canvas_hamburger_size`
- Added `removeStyleTag()` call when header builder is disabled
- Added listener for `wpbf_enable_header_builder` toggle to clean up style tag when disabled mid-session
- Modified `inc/customizer/js/postmessage-parts/menu-triggers.ts`
- Built the postmessage.js file
