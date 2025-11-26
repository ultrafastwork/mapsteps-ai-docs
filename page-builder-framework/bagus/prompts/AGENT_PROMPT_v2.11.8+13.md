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
Set up automated end-to-end (E2E) UI testing for WordPress Customizer controls using **Nightwatch v3**.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md` to understand the project state and requirements.

2. **Research & Install**:
   - Research Nightwatch v3 setup and best practices
   - Create `page-builder-framework-e2e-testing` directory in project root (`d:/www/mapsteps/`)
   - Install Nightwatch v3 and required dependencies in the new directory
   - Set up browser drivers (ChromeDriver, GeckoDriver, etc.)

3. **Configure**:
   - Create Nightwatch configuration file (`nightwatch.conf.js` or similar)
   - Configure for WordPress environment and Customizer testing
   - Set up appropriate test environments (local, CI, etc.)

4. **Structure**:
   - Set up directory structure inside `page-builder-framework-e2e-testing` (e.g., `tests/`, `helpers/`, `config/`)
   - Organize tests by control type or feature area
   - Create helper utilities for common Customizer operations (navigation, control interaction, etc.)

5. **Write Initial Tests**:
   - Create sample tests for basic Customizer controls
   - Test control dependencies and relationships
   - Verify control state changes and live preview updates
   - Document test patterns and conventions

6. **Integration**:
   - Add npm scripts for running tests (e.g., `test:e2e`, `test:e2e:watch`)
   - Document how to run tests locally
   - (Optional) Set up CI/CD integration

7. **Document**:
   - Create README for the test suite
   - Document test architecture and patterns
   - Update `PROGRESS_HANDOFF.md` with results and next steps

**Important Notes**:

- Testing scripts must be in **`d:/www/mapsteps/page-builder-framework-e2e-testing/`**, **NOT** inside `wp-content` directory
- Use **Nightwatch v3** (modern and robust)
- Focus on WordPress Customizer controls and their dependencies
- The theme has tens or hundreds of controls with complex relationships
