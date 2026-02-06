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
- Last Completed Session: **v2.11.9+10**
- Current Session: **v2.11.9+11**

**Objective**:
Waiting for next task.

**Previous Session Summary (v2.11.9+10)**:
✅ Fixed Issue #5 - Menu Trigger Alignment & Spacing:
1.  Fixed vertical misalignment by updating SVG `viewBox` (0 0 32 27) and adding optical CSS alignment (`top: 0.2em`).
2.  Ensured robust spacing between icon and text by applying `margin-right: 8px` to the SVG element.
3.  Verified via visual inspection and asset build (`pnpm build-style`).

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Read `.antigravityrules` for core principles.
3. Run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.
