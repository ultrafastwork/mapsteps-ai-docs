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
- Last Completed Session: **v2.11.9+07**
- Current Session: **v2.11.9+08**

**Objective**:
Waiting for next task.

**Previous Session Summary (v2.11.9+07)**:
✅ Footer Builder HTML Widget Default Value Saving:
1.  Fixed issue where default text was not saved when HTML widgets were added without edits.
2.  Used `wpbf_customize_str_value` in `FooterBuilderOutput.php` to handle default values correctly.
3.  Ensured consistent behavior between Customizer preview and front-end.

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Read `.antigravityrules` for core principles.
3. Run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.
