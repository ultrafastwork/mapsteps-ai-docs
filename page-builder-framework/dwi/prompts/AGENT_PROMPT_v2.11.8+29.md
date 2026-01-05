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
- Last Completed Session: **v2.11.8+28**
- Current Session: **v2.11.8+29**

**Objective**:
Optimize the enhanced-select control (Select2) to reduce memory consumption when displaying Google fonts. The current implementation causes memory spikes because Select2 creates internal copies of the font list for each instance.

**Problem Statement**:
- The Google font list definition already uses a single global object
- However, Select2 internally copies the font list for each select2 instance
- When multiple font fields are present (e.g., in Header Builder), memory consumption spikes significantly
- This is observable in browser tab memory (hover Chrome/Brave tab to see memory usage)
- Do NOT open DevTools inspect panel during testing as it dramatically increases memory

**Testing Instructions**:
1. Open Customizer → Header Builder
2. Hover over browser tab to observe memory consumption
3. Navigate through font-related fields across different sections
4. Hover over tab again to check memory changes
5. **Important**: Avoid opening inspect element panel

**Previous Session Summary (v2.11.8+28)**:
✅ Fixed Header Builder desktop off-canvas menu bugs:
1. Push menu white space appearing on wrong side (Off-Canvas Left)
2. Font colors not applied on Customizer reload
3. Missing default value for reveal_as setting

**Instructions**:
1. Read `PROGRESS_HANDOFF.md` for full context and next tasks.
2. Research Select2 memory optimization strategies (lazy loading, shared data stores, virtual scrolling, etc.)
3. Implement solution to prevent Select2 from duplicating font data per instance.
4. Test in Customizer with multiple font fields; verify memory is stable.
5. Run relevant builds with **pnpm** (avoid npm).
6. Update `PROGRESS_HANDOFF.md` with findings, fixes, and tests; archive this prompt when the session is complete.

**Key Files to Investigate**:
- `Customizer/Controls/Select/` - Enhanced select control implementation
- Files containing Select2 initialization and Google fonts data
- Any shared font list/data module

**Reminder**: When handing off, archive `AGENT_PROMPT.md` with the session version and refresh the new prompt per `PROGRESS_HANDOFF.md`.
