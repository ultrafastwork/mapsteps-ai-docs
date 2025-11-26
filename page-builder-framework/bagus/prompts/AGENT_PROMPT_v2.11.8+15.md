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
Continue expanding the Nightwatch v3 E2E test suite with Builder, Repeater, and Enhanced Select control tests, plus CI/CD integration.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md` to understand the project state and requirements.

2. **Verify Setup**:
   - Navigate to `d:/www/mapsteps/page-builder-framework-e2e-testing/`
   - Run `pnpm test` to verify the existing test suite works
   - Update WordPress credentials in `config/globals.js` if needed

3. **Add Builder Control Tests**:
   - Review Header Builder controls in `wp-content/themes/page-builder-framework/Customizer/Controls/Builder/`
   - Create tests for builder-specific interactions
   - Test row/column configurations

4. **Add Repeater Control Tests**:
   - Review Repeater controls in `wp-content/themes/page-builder-framework/Customizer/Controls/Repeater/`
   - Test add/remove/reorder functionality
   - Test nested repeater fields

5. **Add Enhanced Select Tests**:
   - Test enhanced-select dropdowns (Select2-style)
   - Test search functionality within selects
   - Test multi-select capabilities

6. **Set Up CI/CD Integration**:
   - Create GitHub Actions workflow for automated testing
   - Configure headless browser testing
   - Add test reporting

7. **Document**:
   - Update README with new test patterns
   - Update `PROGRESS_HANDOFF.md` with results and next steps

**Important Notes**:

- Tests are in **`d:/www/mapsteps/page-builder-framework-e2e-testing/`**
- Use existing custom commands in `helpers/commands/`
- Follow existing test patterns in `tests/customizer/controls/`
- See README.md for documented WPBF control types and dependencies
