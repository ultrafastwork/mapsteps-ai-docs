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
Cleanup: Delete `postmessage-backup.ts` and verify overall project health.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/progress-handoffs/PROGRESS_HANDOFF.md` to understand the current state.

2. **Cleanup Task**:
   - Delete `inc/customizer/js/postmessage-backup.ts` as it is no longer needed.

3. **Verification**:
   - Run `npx prettier --write .` to ensure the entire project is formatted correctly.
   - Run `npx tsc --noEmit` to verify no type errors remain in the project.

4. **Update Documentation**:
   - Update `PROGRESS_HANDOFF.md` with completion status.
   - Archive session if needed per workflow rules.
