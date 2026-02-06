# Agent Prompt

**Role**: You are an expert Node.js, WordPress, and JavaScript performance optimization developer.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is:
`ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Strictly follow:
1. `.antigravityrules` (Root-level operating principles)

**Session Info**:
- Last Completed Session: **v2.11.9+11**
- Current Session: **v2.11.9+12**

**Objective**:
Waiting for next task.

**Previous Session Summary (v2.11.9+11)**:
✅ Fixed Issue #4 - Logo Width Live Preview:
1.  **Fixed Selector**: Updated `logo.ts` to target `.wpbf-logo img` in addition to `.wpbf-mobile-logo img` for tablet and mobile breakpoints, resolving the issue where styles weren't applying to the visible logo.
2.  **Cleaned Media Queries**: Simplified `mediaQueries` definitions in `customizer-util.ts` (removed `screen and` prefix) to ensure valid CSS syntax when wrapped in parentheses by `writeCSS`.
3.  Verified via code inspection and `pnpm build-customizer`.

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Read `.antigravityrules` for core principles.
3. Run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.
