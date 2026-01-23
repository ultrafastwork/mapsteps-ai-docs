# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`

**Objective**: Verify Custom Sections refactoring from previous session.

**Status**: Session v2.10.3+18 ready to start. Previous session refactored `class-custom-sections.php`.

## Previous Work (v2.10.3+17)

- Refactored `class-custom-sections.php` (2,377 lines) into modular components:
  - `inc/custom-sections/trait-post-type-helpers.php` - Post type utilities
  - `inc/custom-sections/class-display-rules-matcher.php` - Display rules matching
  - `inc/custom-sections/class-display-rules-ui.php` - Admin UI for display rules
  - `inc/custom-sections/class-frontend-renderer.php` - Frontend rendering
- Main class reduced to ~740 lines, now uses composition
- Fixed singleton pattern
- Backup file: `inc/class-custom-sections-backup.php`

## Instructions

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for full details on what was done.
2. **Verify Refactoring**:
   - Compare combined content of all new module files against `class-custom-sections-backup.php`
   - Ensure all methods are preserved and no code is lost
   - Check that namespace references and class dependencies are correct
3. **Test Functionality**:
   - If WordPress is available, test Custom Sections admin page
   - Verify display rules metabox loads correctly
   - Verify saving/updating a Custom Section works
4. **Report Findings**: Document any issues found or confirm verification passed.
