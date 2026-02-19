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
- Last Completed Session: **v2.11.9+17**
- Current Session: **v2.11.9+18**

**Objective**:
Waiting for next task.

**Previous Session Summary (v2.11.9+17)**:
✅ Fixed Menu Trigger Alignment & Spacing:
1.  Added missing `.use-header-builder` class to Top Row and Mobile Rows in `HeaderBuilderOutput.php`.
2.  Fixed filter name typo in `HeaderBuilderOutput.php`.
3.  Adjusted menu trigger `column-gap` in `_navigation.scss`.
4.  Verified via `pnpm build-style`.

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Read `.antigravityrules` for core principles.
3. Run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.
