# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Work on pending issues from `issues.md`.

**Status**: Session v2.11.8+57 - Ready to start.

---

## Pending Issues
- **Issue #6**: Footer Builder Issues (Remaining)
  - **Live Preview (HTML Widget)**: When changing the content of a specific widget (e.g., HTML 1), the preview output resets to the Default Footer Style. This is architectural - the partialRefresh mechanism reloads the entire `#footer` element. A proper fix would require implementing postMessage-based live preview for the HTML widget content. Please check if HTML widget in header builder is using postmessage for its live preview.

---

## Recent Completed

- ✅ Issue #6: Footer Builder Issues - Partial fix (v2.11.8+56) - See `PROGRESS_HANDOFF_v2.11.8+56_COMPLETE.md` for details.
  - Main Row Settings fixed (added all controls)
  - Copyright Widget placeholders fixed ([year], [blogname])
  - Logo Widget controls added (Logo Width)
