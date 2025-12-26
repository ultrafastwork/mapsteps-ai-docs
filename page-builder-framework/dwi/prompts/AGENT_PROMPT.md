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
- Last Completed Session: **v2.11.8+26**
- Current Session: **v2.11.8+27**

**Objective**:
Investigate and fix header/header-builder/customizer live-preview issues (desktop & mobile) so settings update instantly in Customizer and persist correctly on the frontend.

**Scope (Must address all)**:
1. Header Builder – Search Widget (Desktop): icon color/size not updating live or after save.
2. Header – Navigation Hover Effects: hover color & border radius not applying (Customizer + frontend).
3. Header – CTA Button (Non-Header Builder): border radius not live-updating (works after save).
4. Header – Mobile Navigation Icon Color (Non-Header Builder): Design tab color not applying.
5. Header Builder – Search Widget Positioning: left-aligned search input expands off-screen; keep fully visible.

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and expected behaviors.
2. Debug and implement fixes for all five issues; ensure live preview + saved frontend outputs match.
3. Sanitize/escape as needed; use WordPress APIs/hooks consistently.
4. Test in Customizer live preview and frontend; run relevant builds with **pnpm** (avoid npm).
5. Update `PROGRESS_HANDOFF.md` with findings, fixes, tests; archive this prompt when the session is complete.

**Reminder**: When handing off, archive `AGENT_PROMPT.md` with the session version and refresh the new prompt per `PROGRESS_HANDOFF.md`.
