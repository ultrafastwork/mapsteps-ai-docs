# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Work on pending issues from `issues.md` or new feature requests.

**Status**: Session v2.11.8+59 - Completed.

---

## Pending Issues

- **Issue #1: Footer Builder - Copyright Widget Theme Author Instant Preview**
  - **Condition**: Footer Builder Enabled.
  - **Issue**: Copyright Widget Theme Author Instant Preview does not work.
  - **Steps to reproduce**: Try to set the Theme Author and URL in the Copyright Widget.
  - **Current Behavior**: When set / change the theme author, the output is back to default layout (standard layout) and when this occurred, the others widgets live preview are also does not work.
  - **Goal**: Fix the instant preview for the Copyright Widget when Footer Builder is enabled, ensuring it doesn't break other widgets' live previews.

---

## Recent Completed

- ✅ Issue #6: Footer Builder Issues - Complete fix (v2.11.8+56, v2.11.8+57)
  - **Problem**: Main Row settings (padding, colors, etc.), Logo Width, and Copyright placeholders were missing or incomplete. HTML widget live preview was broken (resetting styles on edit).
  - **Fix**: Added all missing controls, updated `wpbf_parse_template_tags()`, and implemented postMessage-based live preview for HTML widgets.
- ✅ Issue #1: Footer Builder Preview & Settings fix (v2.11.8+53)
  - **Note**: This was a previous fix for general footer builder preview issues. Now focusing on the specific Copyright Widget Theme Author issue.
  - Main Row Settings fixed (added all controls)
  - Copyright Widget placeholders fixed ([year], [blogname])
  - Logo Widget controls added (Logo Width)
  - HTML Widget Live Preview fixed (postMessage-based)
