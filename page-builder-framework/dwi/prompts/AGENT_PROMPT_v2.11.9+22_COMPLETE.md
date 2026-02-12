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
- Last Completed Session: **v2.11.9+22**
- Current Session: **v2.11.9+23**

**Objective**:
Waiting for next task.

**Previous Session Summary (v2.11.9+22)**:
✅ Customizer Persistence & Font Colors:
1.  Fixed off-canvas visibility persistence via `maintainActiveState: true` and new PHP callbacks.
2.  Moved theme's `menu_font_colors` to Header Builder Desktop Off-Canvas section.
3.  Removed redundant premium setting and updated style generation/PostMessage logic.
4.  Refactored all custom `activeCallback` functions into `settings-helpers.php`.

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Read `.antigravityrules` for core principles.
3. Run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.
