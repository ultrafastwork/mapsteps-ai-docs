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
- Last Completed Session: **v2.11.9+06**
- Current Session: **v2.11.9+06**

**Objective**:
Fixed Header Builder search icon vertical alignment in customizer preview for desktop.

**Session Summary (v2.11.9+06)**:
✅ Header Builder Desktop Search Icon Alignment:
1.  Identified that the search icon was misaligned (appeared too low) in the customizer preview on desktop.
2.  Initial attempts using `body.wpbf-desktop-preview` CSS selector failed because the class is applied to the customizer sidebar, not the preview iframe.
3.  Implemented solution using `is_customize_preview()` PHP conditional in `header-builder-search-styles.php`.
4.  Applied `transform: translateY(-85%)` only in customizer preview for desktop (min-width: 1024px).
5.  Also reset SVG icon `top` offset in `_content.scss` for `.searchform button .wpbf-icon svg`.

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Read `.antigravityrules` for core principles.
3. Run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.
