# Agent Prompt

**Role**: You are an expert Node.js, WordPress, and test automation developer and AI coding assistant.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is the file:
`ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Please strictly follow the rules defined in:

1. `ai-docs/page-builder-framework/rules.md` (Project-specific rules)

**Objective**:
Expand the Nightwatch v3 E2E test suite with WPBF-specific control tests and control dependency testing.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md` to understand the project state and requirements.

2. **Verify Setup**:
   - Navigate to `d:/www/mapsteps/page-builder-framework-e2e-testing/`
   - Run `pnpm test` to verify the existing test suite works
   - Update WordPress credentials in `config/globals.js` if needed

3. **Map WPBF Control Dependencies**:
   - Review controls in `wp-content/themes/page-builder-framework/Customizer/Controls/`
   - Identify control dependencies (show/hide relationships)
   - Document which controls depend on other controls

4. **Add WPBF-Specific Tests**:
   - Create tests for Typography controls
   - Create tests for MarginPadding controls
   - Create tests for Responsive controls
   - Create tests for Builder controls (if applicable)

5. **Test Control Dependencies**:
   - Create tests that verify dependent controls show/hide correctly
   - Test nested dependencies
   - Verify control state persistence

6. **Test Preview Updates**:
   - Verify CSS changes appear in preview iframe
   - Test live preview for different control types
   - Test postMessage vs refresh preview modes

7. **Document**:
   - Update README with new test patterns
   - Document control dependency mappings
   - Update `PROGRESS_HANDOFF.md` with results and next steps

**Important Notes**:

- Tests are in **`d:/www/mapsteps/page-builder-framework-e2e-testing/`**
- Use existing custom commands in `helpers/commands/`
- Follow existing test patterns in `tests/customizer/controls/`
- Focus on WPBF-specific controls and their dependencies
