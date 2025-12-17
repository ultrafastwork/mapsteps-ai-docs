# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Ensure Sub Menu and Mobile Sub Menu settings remain visible and functional when Header Builder is enabled.

**Status**: Header Builder is fully functional, but Sub Menu sections are not integrated.

## Task: Sub Menu Settings - Header Builder Integration (Option 1)

### Background

When Header Builder is toggled ON, most header settings are moved to Header Builder sections. However, **Sub Menu** and **Mobile Sub Menu** sections are not handled - they should remain visible as global settings that apply to all menus.

### What to Do

1. **Verify Visibility**: Check if `wpbf_sub_menu_options` and `wpbf_mobile_sub_menu_options` sections are visible when Header Builder is enabled.

2. **If Hidden**: Find where the hiding logic is implemented and ensure these sections are NOT conditionally hidden based on `wpbf_enable_header_builder` setting.

3. **Test**: Confirm that Sub Menu and Mobile Sub Menu settings work correctly when Header Builder is active.

### Key Files

- `inc/customizer/settings/settings-header.php` - Sub Menu sections defined here
- `inc/customizer/js/customizer-parts/setup-controls-movement.ts` - Controls movement logic
- `wp-content/plugins/wpbf-premium/inc/customizer/js/customizer.ts` - Premium movement logic

### Instructions

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for full details and control IDs.

2. **Read Rules**: Check `ai-docs/page-builder-framework/rules.md` for project-specific guidelines.

3. **Investigate**: Check if sections are hidden when Header Builder is enabled.

4. **Fix if Needed**: Ensure sections remain visible.

5. **Document**: Update `PROGRESS_HANDOFF.md` with results.
