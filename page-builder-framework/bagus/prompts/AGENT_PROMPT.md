# Agent Prompt

**Role**: You are an expert WordPress developer and AI coding assistant.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is the file:
`ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)
2. `.antigravityignore` (Forbidden files and directories that you MUST NOT access)
3. `ai-docs/page-builder-framework/rules.md` (Project-specific rules)

**Objective**:
Refactor `inc/customizer/styles/header-builder-styles.php` by splitting it into smaller, logical modules as defined in `PROGRESS_HANDOFF.md`.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md` to understand the plan.

2. **Execute Refactoring**:
   - Create the following new files in `inc/customizer/styles/`:
     - `header-builder-rows-styles.php`
     - `header-builder-button-styles.php`
     - `header-builder-search-styles.php`
     - `header-builder-menu-styles.php`
   - Move the corresponding code from `header-builder-styles.php` to these new files.
   - **IMPORTANT**: Do NOT change any logic. Just move the code.

3. **Update Loader**:
   - Update `inc/customizer/styles/header-builder-styles.php` to only contain `require_once` statements for the new modules.

4. **Verify**:
   - Run `php -l` on all new and modified files to ensure no syntax errors.
   - Verify that the order of execution is preserved.

5. **Document**: Update `PROGRESS_HANDOFF.md` with the results.
