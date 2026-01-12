# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`

**Objective**: Split settings-header.php into modular files.

**Status**: Session v2.10.3+14 completed. Refactored `settings-header.php`.

## Completed Work

### Task: Split settings-header.php (v2.10.3+14)

- Split `settings-header.php` (2267 lines) into 11 modular partials in `inc/customizer/controls/header/`.
- Verified all 104 Customizer field IDs preserved.
- Verified all 4 sections preserved.

## Instructions

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for full details.
2. **Read Rules**: Check `ai-docs/wpbf-premium/rules.md` for project-specific guidelines.
3. **Next Tasks**:
   - Test customizer in WordPress admin
   - Delete backup file after verification
   - Consider similar refactoring for other large files
