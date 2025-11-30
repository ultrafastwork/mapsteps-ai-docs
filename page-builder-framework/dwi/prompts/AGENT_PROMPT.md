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
Fix critical display issues with Desktop Off-Canvas and Mobile Menus, and finalize the Mobile Button live preview fixes.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md` to understand the recent changes.

2. **Fix Menu Display Issues (Critical)**:
   - **Desktop Off-Canvas Menu**: Investigate and fix why it is not showing.
   - **Mobile Menu**: Investigate and fix why it is not showing.
   - Check if recent changes to `off-canvas.ts` or `mobile-navigation.ts` caused regressions.
   - Verify HTML markup and CSS classes match the selectors in the JavaScript.

3. **Fix Mobile Button Live Preview**:
   - **Mobile Button 1 & 2**: The user reports that border radius and border width live preview is still not working correctly.
   - Review the changes made in Session v2.11.8+18 (initial value application, listener type change, !important).
   - Debug why the preview might still be failing (check console logs, inspect elements).
   - Ensure the correct CSS selectors are being used and that styles are not being overridden.

3. **E2E Regression Testing (Medium Priority)**:
   - Navigate to `page-builder-framework-e2e-testing` directory
   - Run: `pnpm test:smoke` to ensure Customizer loads properly after changes
   - Run: `pnpm test:builder` to ensure Header Builder interactions still work
   - If tests fail, investigate whether failures are related to the postMessage changes

4. **PHP Settings Verification (Only if issues found)**:
   - If manual tests reveal problems, inspect PHP Customizer settings registration:
     - Verify setting IDs match JavaScript expectations
     - Confirm `transport => 'postMessage'` is set for all instant-preview controls
     - Confirm HTML markup matches CSS selectors used in postMessage JavaScript modules

5. **Document Results**:
   - Update `PROGRESS_HANDOFF.md` with verification results
   - Report any bugs found or additional fixes needed
   - If all tests pass, consider this issue resolved
