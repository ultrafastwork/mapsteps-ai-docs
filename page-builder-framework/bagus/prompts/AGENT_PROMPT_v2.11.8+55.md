# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Resolve Issue #5 in `issues.md` - Menu Font Size not applied on frontend.

**Status**: Session v2.11.8+55 - Ready to start.

---

## Current Task: Issue #5 - Menu Font Size Implementation (Header Builder)

### Condition
- Header Builder's "HTML 1" or "HTML 2" widget added to main row (second row)
- "Menu 1" OR "Menu 2" widget also in main row
- Main Row's `wpbf_header_builder_desktop_row_2_font_size` set to `14px`
- Menu widget has its own font size setting (`menu_font_size` for Menu 1, `wpbf_header_builder_desktop_menu_2_menu_font_size` for Menu 2)

### Expected Behavior
HTML widget inherits row's font size (14px), Menu widget uses its own font size (16px).

### Problem
Works in Customizer preview, but **not on frontend**. On frontend, Menu widget uses 14px (row's value) instead of its own 16px value. Inheriting value is correct, but when an element has its own setting value, then it should be prioritized.

### Investigation Notes
- TBD

---

## Other Pending Issues

- **Issue #3**: Hamburger Icon Customization (Full Screen)
- **Issue #4**: Mobile Navigation Padding
