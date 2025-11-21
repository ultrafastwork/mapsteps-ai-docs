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
Consolidate duplicate `mediaQueries` constants into `customizer-util.ts` to eliminate code duplication.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/progress-handoffs/PROGRESS_HANDOFF.md` to understand the current state.

2. **Identify Duplicate mediaQueries**:
   - 4 files contain identical `const mediaQueries` with mobile/tablet/desktop properties:
     - `layout.ts` (lines 13-24)
     - `logo.ts` (lines 13-24)
     - `tagline.ts` (lines 12-23)
     - `header-builder-search.ts` (lines 12-23)

3. **Consolidation Task**:
   - Export `mediaQueries` as a constant from `customizer-util.ts`
   - Update all 4 files to import and use the shared `mediaQueries`
   - Remove the local `const mediaQueries` declarations from each file

4. **Verification**:
   - Run `npx prettier --write` on modified files
   - Run `npx tsc --noEmit` to verify no type errors
   - Ensure all modules still work correctly

5. **Update Documentation**:
   - Update `PROGRESS_HANDOFF.md` with completion status
   - Archive session if needed per workflow rules
