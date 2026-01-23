# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Work on pending issues from `issues.md`.

**Status**: Session v2.11.8+57 - Completed.

---

## Completed Issues
- **Issue #6**: Footer Builder Issues (Remaining)
  - **Problem**: HTML widget live preview was broken (resetting styles on edit) because it used `partialRefresh` which re-rendered the whole footer without applying dynamic styles.
  - **Fix**: Implemented postMessage-based live preview for HTML widgets. Changed from partialRefresh to postMessage transport, added unique CSS classes to each HTML widget for targeting, and added postMessage handlers in `footer-builder-rows.ts`.
- **Issue #6**: Footer Builder Issues (Initial)
  - **Problem**: Main Row settings (padding, colors, etc.), Logo Width, and Copyright placeholders were missing or incomplete.
  - **Fix**: Added all controls to desktop and mobile main-row-section.php and logo-section.php files. Updated `wpbf_parse_template_tags()` for placeholders. (v2.11.8+56)
