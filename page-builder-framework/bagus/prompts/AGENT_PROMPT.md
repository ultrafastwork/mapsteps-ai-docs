# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Conditionally hide desktop menu trigger widget when wpbf-premium plugin is inactive.

**Status**: Session v2.11.8+80 - Desktop Menu Trigger Conditional Display.

---

## Task Details

### Background

The desktop menu trigger widget in Header Builder can be added regardless of whether wpbf-premium plugin is active. However, this widget only triggers Desktop Off-Canvas or Full-Screen menus, which are premium-only features. When premium is inactive, the widget serves no purpose on desktop view.

### Problem

- Desktop menu trigger widget appears in Header Builder widget list even when wpbf-premium is inactive
- Widget is useless without premium features (Desktop Off-Canvas/Full-Screen menus)
- Mobile menu trigger should remain available (triggers dropdown menu - free feature)

### Objective

Hide or disable the desktop menu trigger widget from the Header Builder widget list when wpbf-premium plugin is inactive, while keeping it available for mobile/tablet versions.

### Key Files

1. **`Customizer/HeaderBuilder/HeaderBuilderConfig.php`** (line 36-40)
   - Registers desktop menu trigger widget in `availableWidgets()` method
   
2. **`inc/init.php`** (line 15-17)
   - Contains `wpbf_is_premium()` function for premium detection

3. **`inc/customizer/settings/header-builder/desktop/offcanvas-section.php`** (line 44)
   - Example of premium check implementation

### Implementation Steps

1. **Modify Widget Registration**:
   - File: `Customizer/HeaderBuilder/HeaderBuilderConfig.php`
   - Action: Add conditional check in `availableWidgets()` method to exclude `desktop_menu_trigger` from desktop widgets array when `!wpbf_is_premium()`
   - Keep mobile menu trigger widget available (it works with free dropdown menu)

2. **Test Scenarios**:
   - Verify desktop menu trigger is hidden in customizer when premium is inactive
   - Verify desktop menu trigger appears when premium is active
   - Verify mobile menu trigger remains available in both cases

### Expected Outcome

- Desktop menu trigger widget only appears in Header Builder widget list when wpbf-premium is active
- Mobile menu trigger widget remains available regardless of premium status
- Existing desktop menu trigger widgets in saved layouts continue to work when premium is active

---

## Recent Accomplishments (v2.11.8+79)

### Row 2 Menu Style Decoupling Implementation

**Changes Made**:

1. **Scoped Legacy Styles** (`inc/customizer/styles/header-styles.php`):
   - Wrapped `menu_bg_color` and `menu_font_colors` logic with `if ( ! wpbf_header_builder_enabled() )`.
   - Prevents global CSS leakage when Header Builder is active.

2. **Added Row 2 Controls** (`inc/customizer/settings/header-builder/desktop/main-row-section.php`):
   - Added `accent_colors` (multicolor) control with 'default' and 'hover' choices.

3. **Updated Row Styles** (`inc/customizer/styles/header-builder-rows-styles.php`):
   - Row 2 now applies its own `accent_colors` to row-specific selectors.
   - Row 2 is now row-agnostic like Row 3.

**Result**:
- ✅ Menus in Row 3 or Row 1 are no longer affected by Row 2's legacy color settings.
- ✅ Row 2 can be styled independently with its own font and accent colors.
- ✅ Row 1 maintains its connection to `pre_header_*` settings (intended behavior).

---

## Recent Completed

- ✅ Row 2 Menu Style Decoupling Implementation (v2.11.8+79)
- ✅ Row 2 Menu Style Decoupling Analysis (v2.11.8+78)
- ✅ Custom Select2 DataAdapter Implementation (v2.11.8+77)
- ✅ Typography Controls Memory Analysis (v2.11.8+76)
- ✅ Responsive Style Tag Consolidation (v2.11.8+75)
