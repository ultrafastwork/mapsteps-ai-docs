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
Prioritize expanding Nightwatch v3 E2E tests for the Header Builder (enable/disable toggle, rows/columns, widget placement, responsive views). Keep CI manual-only while focusing on local development.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md` to understand the project state and requirements.

2. **Verify Setup**:
   - Navigate to `d:/www/mapsteps/page-builder-framework-e2e-testing/`
   - Run `pnpm install` to install dependencies (including dotenv)
   - Run `pnpm test` to verify the existing test suite works
   - Credentials are loaded from `d:/www/mapsteps/.env.local` (WP_USERNAME, WP_PASSWORD)

3. **Header Builder Tests**:
   - Review Builder controls in `wp-content/themes/page-builder-framework/Customizer/Controls/Builder/`
   - Test enabling/disabling `wpbf_enable_header_builder`
   - Interact with rows/columns and drag-and-drop widgets
   - Test responsive device switcher (desktop/tablet/mobile)

4. **Optional (Later) Controls**:
   - Sortable: drag-and-drop reordering and item interactions
   - Media: image upload and media library selection
   - Code Editor: code input and syntax highlighting

5. **CI/CD (Manual Only)**:
   - CI workflow should be manual via `workflow_dispatch` only (no push/PR triggers)
   - Ensure theme installation/setup steps exist but do not auto-run
   - Consider adding test data seeding and visual regression later

7. **Document**:
   - Update README with new test patterns
   - Update `PROGRESS_HANDOFF.md` with results and next steps

**Important Notes**:

- Tests are in **`d:/www/mapsteps/page-builder-framework-e2e-testing/`**
- Use existing custom commands in `helpers/commands/`
- Follow existing test patterns in `tests/customizer/controls/`
- See README.md for documented WPBF control types and dependencies
- CI/CD workflow is in `.github/workflows/e2e-tests.yml` and is manual-only for now
