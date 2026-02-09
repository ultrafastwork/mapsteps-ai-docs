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
- Last Completed Session: **v2.11.9+15**
- Current Session: **v2.11.9+16**

**Objective**:
Waiting for next task.

**Previous Session Summary (v2.11.9+15)**:
✅ Fixed Search Widget Icon Shift in Header Builder:
1.  Removed the `translateY(-85%)` hack from `header-builder-search-styles.php`.
2.  Added `right: -20px !important` for `.wpbf-header-column .wpbf-menu-item-search .wpbf-menu-search` in `_navigation.scss`.
3.  Kept `inline-flex` and `align-items: center` for Header Builder search widget.
4.  Refactored desktop search icon size handling in `header-builder.ts` to use `parseJsonOrUndefined` for responsive values.
5.  Added desktop search icon size PHP handler in `header-builder-search-styles.php`.
6.  Verified via `pnpm build-style`.

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Read `.antigravityrules` for core principles.
3. Run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.
