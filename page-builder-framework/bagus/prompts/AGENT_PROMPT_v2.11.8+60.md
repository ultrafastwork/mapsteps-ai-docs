# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Work on pending issues from `issues.md` or new feature requests.

**Status**: Session v2.11.8+60 - Completed.

---

## Recent Completed

- ✅ Issue #2: Footer Builder HTML Widget margin-bottom fix (v2.11.8+60)
  - **Problem**: HTML widget content (paragraphs) had 20px margin-bottom causing text to not be vertically centered.
  - **Fix**: Added CSS rule to reset margin-bottom on last element in `.wpbf-footer-html-widget`.
- ✅ Issue #3: Footer Builder Social Icons spacing fix (v2.11.8+60)
  - **Problem**: Social icons had no spacing between them when multiple icons were added.
  - **Fix**: Added flexbox with `gap: 10px` to `.wpbf-footer-social` container.
- ✅ Issue #1: Footer Builder Copyright Widget Theme Author Instant Preview fix (v2.11.8+59)
  - **Problem**: When changing Theme Author settings, the footer reverted to standard layout instead of Footer Builder layout.
  - **Fix**: Updated partial refresh callbacks to use `footer-builder.php` when Footer Builder is enabled. Added `[theme_author]` placeholder support to `wpbf_parse_template_tags()`.
- ✅ Issue #6: Footer Builder Issues - Complete fix (v2.11.8+56, v2.11.8+57)
- ✅ Issue #1: Footer Builder Preview & Settings fix (v2.11.8+53)
