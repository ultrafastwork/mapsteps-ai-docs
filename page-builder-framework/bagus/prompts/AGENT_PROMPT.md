# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Work on pending issues from `issues.md` or new feature requests.

**Status**: Session v2.11.8+58 - Ready to start.

---

## Pending Issues

- No pending issues. All known issues (#1-#6) have been resolved.
- Check `issues.md` for any new issues that may have been added.

---

## Recent Completed

- ✅ Issue #6: Footer Builder Issues - Complete fix (v2.11.8+56, v2.11.8+57)
  - **Problem**: Main Row settings (padding, colors, etc.), Logo Width, and Copyright placeholders were missing or incomplete. HTML widget live preview was broken (resetting styles on edit).
  - **Fix**: Added all missing controls, updated `wpbf_parse_template_tags()`, and implemented postMessage-based live preview for HTML widgets.
  - Main Row Settings fixed (added all controls)
  - Copyright Widget placeholders fixed ([year], [blogname])
  - Logo Widget controls added (Logo Width)
  - HTML Widget Live Preview fixed (postMessage-based)
