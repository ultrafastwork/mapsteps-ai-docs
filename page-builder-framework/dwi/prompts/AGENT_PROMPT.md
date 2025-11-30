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
Perform manual verification of the Customizer postMessage fixes implemented in Session v2.11.8+18.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md` to understand what was implemented in the previous session.

2. **Manual Verification (High Priority)**:
   - Open the WordPress Customizer at `http://mapsteps.local/wp-admin/customize.php`
   - Follow the verification instructions documented in Section 10 of the handoff file
   - Test mobile menu trigger padding in both header builder and legacy modes:
     - With header builder enabled: custom padding should take precedence
     - Without header builder: default 10px padding should apply
   - Verify off-canvas push menu width and transform behavior
   - Verify mobile header builder buttons 1 & 2 border radius, width, and style live preview
   - Report any issues found

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
