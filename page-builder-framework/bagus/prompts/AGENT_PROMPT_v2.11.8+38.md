# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Continue refactoring large customizer settings files to improve maintainability.

**Status**: Session v2.11.8+39 ready to start. Previous session refactored `settings-blog.php`.

## Completed Work

### Task: Split settings-blog.php (v2.11.8+38)

- Split `settings-blog.php` (919 lines) into 5 modular files in `inc/customizer/settings/blog/`.
- Main file reduced to 25 lines (includes only).
- Verified exact match with backup: 1 panel, 4 sections, 56 fields.
- All code content verified line-by-line against original backup.

## Instructions

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for full details.
2. **Read Rules**: Check `ai-docs/page-builder-framework/rules.md` for project-specific guidelines.
3. **Await Instructions**: Wait for user to provide next task for customizer settings refactoring.
