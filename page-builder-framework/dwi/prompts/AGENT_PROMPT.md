# Agent Prompt

**Role**: You are an expert Node.js, WordPress, and test automation developer and AI coding assistant.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is the file:
`ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)
2. `.antigravityignore` (Forbidden files and directories that you MUST NOT access)
3. `ai-docs/page-builder-framework/rules.md` (Project-specific rules)

**Objective**:
Verify and ensure all Customizer Header Builder controls are working properly.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md` to understand the recent fixes (Mobile Button Border Radius/Width) and the current state.

2. **Comprehensive Header Builder Verification (Primary Task)**:
   - **Goal**: Systematically verify that ALL controls within the Header Builder (Desktop & Mobile) are functioning correctly.
   - **Scope**:
     - **Elements**: Logo, Navigation (Menu), Search, HTML, Social, Button 1 & 2, Off-Canvas, etc.
     - **Settings**: Layout, Typography, Colors, Spacing, Visibility, Responsive settings.
     - **Live Preview**: Ensure changes update instantly and correctly in the Customizer preview (postMessage).
   - **Method**:
     - Manual verification in the Customizer.
     - Running existing E2E tests (`pnpm test:builder`).
     - Creating new E2E tests if coverage is missing for specific controls.

3. **Fix & Refine**:
   - If any control is found to be broken or lagging (refreshing instead of instant preview), investigate and fix.
   - Apply the same "Responsive Input Slider" fix logic if other responsive controls are misbehaving.

4. **Document Results**:
   - Update `PROGRESS_HANDOFF.md` with a list of verified controls.
   - Report any bugs fixed or outstanding issues.
