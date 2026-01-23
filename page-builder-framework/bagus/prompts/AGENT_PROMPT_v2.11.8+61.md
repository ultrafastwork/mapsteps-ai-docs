# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Work on pending issues from `issues.md` or new feature requests.

**Status**: Session v2.11.8+61 - Ready to start.

---

## Pending Tasks (v2.11.8+61)

- **Improve Footer Builder Layout & Styling** based on the attached screenshot:
  - **Issue 1: Vertical Centering**: The footer content is currently centered vertically. Change this to top-aligned (standard for footers).
    - *Actionable Suggestion*: Consider removing `wpbf-items-center` from the `.wpbf-row-content` wrapper in `FooterBuilderOutput.php` (line 228).
    - *Caution*: Be aware that `.wpbf-row-content` also has `align-items: center` defined in the CSS (e.g., `_navigation.scss`). Modifying this shared class directly could break the **Header Builder** output. Think about CSS isolation or row-specific overrides.
  - **Issue 2: Un-designed Menus**: "Menu 1" and "Menu 2" widgets use browser defaults. Re-style them to look like proper footer menus.
    - *Research*: Check `render_menu_widget` in `FooterBuilderOutput.php` (line 371). Consider using or adapting classes from the header builder (e.g., `.wpbf-menu`).
  - **Issue 3: Menu Customization**: Consider adding Customizer fields for "Menu 1" and "Menu 2" widgets to control padding, gap, or margin.
    - *Research*: Check existing fields in `inc/customizer/settings/footer-builder/desktop/menu-1-section.php`.
- **Note**: The user has attached a screenshot showing these issues for reference.
- **Critical Considerations**:
  - **Isolation**: Check if existing classes (like `.wpbf-menu`) are used in the header builder. Ensure changes to the footer don't break the header. Use scoped classes where necessary.
  - **Stability**: Ensure that adding new fields doesn't conflict with existing behavior or premium features.

---

## Recent Completed

- ✅ Test Footer Builder widget CSS fixes (HTML margin-bottom, Social Icons spacing) (v2.11.8+60)
- ✅ Test Theme Author instant preview fix with Footer Builder (v2.11.8+60)
- ✅ Issue #2: Footer Builder HTML Widget margin-bottom fix (v2.11.8+60)
- ✅ Issue #3: Footer Builder Social Icons spacing fix (v2.11.8+60)
- ✅ Issue #1: Footer Builder Copyright Widget Theme Author Instant Preview fix (v2.11.8+59)
- ✅ Issue #6: Footer Builder Issues - Complete fix (v2.11.8+56, v2.11.8+57)
- ✅ Issue #1: Footer Builder Preview & Settings fix (v2.11.8+53)
