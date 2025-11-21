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
Start the refactoring of `wp-content/themes/page-builder-framework/inc/customizer/js/postmessage.ts`.
The goal is to split this large file into smaller, modular components.

**Instructions**:

1.  **Read Context**: Read `ai-docs/page-builder-framework/progress-handoffs/PROGRESS_HANDOFF.md` to understand the specific requirements and status.
2.  **Analyze**: Review `postmessage.ts` to identify distinct sections (Layout, Typography, etc.) that can be extracted to `wp-content\themes\page-builder-framework\inc\customizer\js\postmessage-parts` directory.
3.  **Plan & Execute**:
    - Propose structure and name for the new files.
    - Begin extracting sections one by one, a backup already created in `wp-content/themes/page-builder-framework/inc/customizer/js/postmessage-backup.ts`.
    - Ensure `postmessage.ts` imports and uses these new files correctly.
4.  **Verify**: Ensure no functionality is lost during the refactor.
5.  **Update Handoff**: **CRITICAL**: Before finishing, update `PROGRESS_HANDOFF.md` with:
    - Which sections were moved.
    - The new file structure.
    - Any remaining sections to be moved in the next session.
