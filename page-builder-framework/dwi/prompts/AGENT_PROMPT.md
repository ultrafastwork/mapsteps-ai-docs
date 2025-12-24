# Agent Prompt

**Role**: You are an expert Node.js, WordPress, and test automation developer and AI coding assistant.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is the file:
`ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)

**Objective**:
Investigate and fix Customizer live preview and frontend layout issues.

**Previous Session Summary (v2.11.8+24)**:
- ✅ Fixed Header Builder Menu font size live preview for Menu 1 and Menu 2
- ✅ Updated selectors in `navigation.ts` and `mobile-header-builder-rows.ts`
- ✅ Updated PHP style generation for consistency
- ✅ Verified build success with `pnpm run build-all`

**Current State**:
- All 22 Header Builder elements have verified postMessage handlers
- Font size live preview working for both Desktop Menu 1 and Menu 2
- Build system stable and all changes compiled successfully
- E2E test suite available for validation

**Task Details**:

**Issue 1 - Desktop Menu Center Position Bug**:
- Desktop menu center position works in Customizer but breaks on frontend
- Need to investigate CSS generation and frontend/preview differences

**Issue 2 - Mobile Main Row Design Controls**:
- Design tab changes don't show live preview (only partial refresh)
- Need postMessage handlers for real-time updates

**Issue 3 - Mobile Bottom Row Design Controls**:
- Design tab changes don't show live preview (only partial refresh)  
- Need postMessage handlers for real-time updates

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md` for complete task details.

2. **Investigation Priority**:
   - Start with Desktop menu center position CSS analysis
   - Then focus on Mobile row design control postMessage handlers
   - Verify all fixes with build and manual testing

3. **Document Results**:
   - Update `PROGRESS_HANDOFF.md` with findings and fixes
   - Archive session prompt when complete
