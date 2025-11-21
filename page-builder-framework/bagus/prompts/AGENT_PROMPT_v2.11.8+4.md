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
Perform comprehensive verification of all refactored modules (including 5 newly extracted modules) against `postmessage-backup.ts` to ensure 100% code preservation.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/progress-handoffs/PROGRESS_HANDOFF.md` to understand the current state.

2. **Review Previous Work**:
   - 5 new modules created: header-builder-rows.ts, header-builder-buttons.ts, header-builder-search.ts, mobile-header-builder-rows.ts, header-builder-reveal.ts
   - off-canvas.ts updated with customizer parameter
   - postmessage.ts updated with new module imports

3. **Comprehensive Verification**:
   - Systematically verify ALL 26 modules (21 existing + 5 new) against backup
   - Use line number mapping from backup file
   - Create verification matrix documenting each module
   - Identify any remaining unextracted logic

4. **Verification Criteria**:
   - ✅ PASS: Logic exactly matches backup
   - ⚠️ MINOR: Minor refactoring but functionally identical
   - ❌ FAIL: Logic missing or significantly different

5. **Report & Update**:
   - Document findings in detailed verification report
   - Fix any critical discrepancies found
   - Update `PROGRESS_HANDOFF.md` with verification results
