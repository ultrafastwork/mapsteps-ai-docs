# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Work on pending issues from `issues.md`.

**Status**: Session v2.11.8+56 - Completed.

---

## Completed in This Session

- ✅ **Main Row Settings**: Added controls (Container Width, Vertical Padding, Background Color, Font Color, Accent Color, Font Size) to desktop and mobile main-row-section.php files.
- ✅ **Copyright Widget Placeholders**: Updated `wpbf_parse_template_tags()` to support `[year]` and `[blogname]`.
- ✅ **Logo Widget Controls**: Added Logo Width control to both desktop and mobile logo-section.php files.

---

## Remaining Issues

- **Live Preview (HTML Widget)**: When changing the content of a specific widget (e.g., HTML 1), the preview output resets to the Default Footer Style. This is architectural - partialRefresh reloads entire footer template.
