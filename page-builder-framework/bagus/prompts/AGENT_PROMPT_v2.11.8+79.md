# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Implement Row 2 menu style decoupling from classical settings in Header Builder.

**Status**: Session v2.11.8+79 - Implementation of Row-Agnostic Styles.

---

## Task Details

### Background

Currently, Row 2 (Main Row) in the Header Builder re-uses classical (non-header builder) settings for font colors and background colors. This causes styles to leak to menus in other rows (Row 1/Row 3) and prevents Row 2 from being styled independently when a different row is used as the "main" row.

### Objective

Make Row 2 row-agnostic like Row 3, while preserving the "pre-header" concept for Row 1.

### Implementation Steps

1. **Scope Legacy Styles**:
   - File: `inc/customizer/styles/header-styles.php`
   - Action: Wrap `menu_font_colors` and `menu_bg_color` logic in `if ( ! wpbf_header_builder_enabled() )`.

2. **Add Row 2 Controls**:
   - File: `inc/customizer/settings/header-builder/desktop/main-row-section.php`
   - Action: Add `accent_colors` (multicolor) control. Follow the pattern in `bottom-row-section.php`.

3. **Update Row Styles**:
   - File: `inc/customizer/styles/header-builder-rows-styles.php`
   - Action: Update logic for `desktop_row_2` to apply its own `text_color` and the new `accent_colors` to its specific row selector, instead of relying on legacy global settings.

### Expected Outcome

- Menus in Row 3 or Row 1 will no longer be affected by Row 2's legacy color settings.
- Row 2 can be styled independently with its own font and accent colors.
- Row 1 maintains its connection to `pre_header_*` settings (intended behavior).

---

## Previous Session Summary (v2.11.8+78)

Session v2.11.8+78 focused on analyzing the "master" row issue:
- ✅ Identified global CSS leakage from `header-styles.php`.
- ✅ Confirmed Row 2 lacks independent accent controls.
- ✅ Validated that Row 1 should keep its "pre-header" re-use logic.

---

## Recent Completed

- ✅ Row 2 Menu Style Decoupling Analysis (v2.11.8+78)
- ✅ Custom Select2 DataAdapter Implementation (v2.11.8+77)
- ✅ Typography Controls Memory Analysis (v2.11.8+76)
- ✅ Responsive Style Tag Consolidation (v2.11.8+75)
- ✅ WooCommerce Conditional Loading (v2.11.8+74)
