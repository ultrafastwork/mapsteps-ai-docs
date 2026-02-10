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
- Last Completed Session: **v2.11.9+21**
- Current Session: **v2.11.9+22**

**Objective**:
Waiting for next task.

**Previous Session Summary (v2.11.9+21)**:
✅ Search Alignment & Style Cleanup:
1.  Fixed non-HB mobile search icon alignment via flexbox.
2.  Scoped `header-builder-styles.php` inclusion to only when active.
3.  Refined search animation transition timings (200ms/250ms).
4.  Rebuild minified CSS via `pnpm build-style`.

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Read `.antigravityrules` for core principles.
3. Run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.
