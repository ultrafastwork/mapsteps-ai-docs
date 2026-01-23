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
- Last Completed Session: **v2.11.9+01**
- Current Session: **TBD**

**Objective**:
Waiting for next task.

**Previous Session Summary (v2.11.9+01)**:
✅ Fixed HTML Widget "Code" tab width issue in the Header Builder:
1. Wrapped the editor `textarea` in a `wpbf-control-form` div in `EditorControl.php`.
2. Corrected the SCSS selector in `editor-control.scss` from `.customize-control-kirki-editor` to `.editor-control`.
3. Rebuilt the Customizer controls bundle to apply the CSS changes.

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Read `.antigravityrules` for core principles.
3. Run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.
