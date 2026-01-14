# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Work on pending issues from `issues.md` or new feature requests.

**Status**: Session v2.11.8+60 - Ready to start.

---

## Pending Issues

- **Issue #2: Footer Builder - HTML Widget margin-bottom**
  - **Condition**: Footer Builder Enabled.
  - **Issue**: HTML 1 and HTML 2 text/paragraph has margin-bottom 20px by default.
  - **Steps to reproduce**: Add HTML 1 or HTML 2 widget and set the content.
  - **Current Behavior**: The output has extra space on the bottom of the text, so the text is not vertically centered.
  - **Goal**: Remove or reset the default margin-bottom on HTML widget content.

- **Issue #3: Footer Builder - Social Icons spacing**
  - **Condition**: Footer Builder Enabled.
  - **Issue**: Social Icons widget does not have default margin/padding.
  - **Steps to reproduce**: Add 2 or 3 social media items.
  - **Current Behavior**: When there is more than 1 social icon, the icon list does not have margin/padding in the output.
  - **Goal**: Add appropriate spacing between social icons.

---

## Recent Completed

- ✅ Issue #1: Footer Builder Copyright Widget Theme Author Instant Preview fix (v2.11.8+59)
  - **Problem**: When changing Theme Author settings, the footer reverted to standard layout instead of Footer Builder layout.
  - **Fix**: Updated partial refresh callbacks to use `footer-builder.php` when Footer Builder is enabled. Added `[theme_author]` placeholder support to `wpbf_parse_template_tags()`.
- ✅ Issue #6: Footer Builder Issues - Complete fix (v2.11.8+56, v2.11.8+57)
- ✅ Issue #1: Footer Builder Preview & Settings fix (v2.11.8+53)
