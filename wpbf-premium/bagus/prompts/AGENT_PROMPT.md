# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`

**Objective**: Awaiting user instructions for next tasks.

**Status**: Session v2.11.8+19 ready to start.

## Completed Work (v2.11.8+17-18)

- Refactored `class-custom-sections.php` (2,377 lines) into 4 modular components
- Updated namespaces:
  - Main class: `WPBF` → `Wpbf\Premium`
  - Modules: `WPBF\CustomSections` → `Wpbf\Premium\CustomSections`
- Added backwards compatibility via `class_alias` for `WPBF\Custom_Sections`
- Backup file preserved: `inc/class-custom-sections-backup.php`

## Instructions

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for full details.
2. **Read Rules**: Check `ai-docs/wpbf-premium/rules.md`.
3. **Await Instructions**: Wait for user to provide next task.
