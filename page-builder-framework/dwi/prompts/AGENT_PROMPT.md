# Agent Prompt

**Role**: You are an expert Node.js, WordPress, and test automation developer and AI coding assistant.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is:
`ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Strictly follow:
1. `.antigravityrules` (Root-level operating principles)

**Session Info**:
- Last Completed Session: **v2.11.8+27**
- Current Session: **v2.11.8+28**

**Objective**:
Continue development on the Page Builder Framework theme. Check PROGRESS_HANDOFF.md for any pending tasks or new objectives.

**Previous Session Summary (v2.11.8+27)**:
All 5 header/Header Builder/Customizer live-preview issues were fixed:
1. ✅ Header Builder Desktop Search Widget - icon color/size live preview
2. ✅ Navigation Hover Effects - live preview + frontend persistence (esc_html issue fixed)
3. ✅ CTA Button Border Radius - live preview
4. ✅ Mobile Navigation Icon Color - SVG fill/stroke added
5. ✅ Search Widget Positioning - left-aligned expansion fixed

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Follow WordPress APIs/hooks consistently and sanitize/escape as needed.
3. Test in Customizer live preview and frontend; run relevant builds with **pnpm** (avoid npm).
4. Update `PROGRESS_HANDOFF.md` with findings, fixes, tests; archive this prompt when the session is complete.

**Reminder**: When handing off, archive `AGENT_PROMPT.md` with the session version and refresh the new prompt per `PROGRESS_HANDOFF.md`.
