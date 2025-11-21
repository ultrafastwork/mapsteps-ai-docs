# Agent Prompt

**Role**: You are an expert WordPress developer and AI coding assistant.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is the file:
`ai-docs/page-builder-framework/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)
2. `.antigravityignore` (Forbidden files and directories that you MUST NOT access)
3. `ai-docs/page-builder-framework/rules.md` (Project-specific rules)

**Objective**:
Refactor `styles.php` and `header-builder-styles.php` by splitting them into smaller, manageable modules to improve maintainability and AI-friendliness.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/progress-handoffs/PROGRESS_HANDOFF.md` to understand the current state and the files involved.

2. **Analyze & Plan**:
   - Analyze `inc/customizer/styles.php` (~1800 lines) and `inc/customizer/styles/header-builder-styles.php` (~850 lines).
   - Identify logical sections (e.g., Typography, Layout, Header, Footer, Mobile).
   - Create a plan to split these into smaller files within `inc/customizer/styles/`.

3. **Refactor**:
   - Create new PHP files for each identified section in `inc/customizer/styles/`.
   - Move the relevant code from the large files to the new smaller files.
   - Ensure the new files are correctly included/required in the main files or a central loader.
   - **Goal**: Reduce the size of the main files significantly.

4. **Verification**:
   - Verify that the Customizer styles still load correctly (manual check or dry run if possible).
   - Ensure no syntax errors (run `php -l` on new files if possible, or rely on careful code movement).
   - Run `npx prettier --write .` to maintain formatting.

5. **Update Documentation**:
   - Update `PROGRESS_HANDOFF.md` with the new file structure and completion status.
   - Archive session if needed per workflow rules.
