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
Stabilize Customizer navigation/login in Nightwatch and then expand Header Builder tests (enable/disable toggle, rows/columns, widget placement, responsive views). Keep CI manual-only, focus on local dev.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md` to understand the project state and requirements.

2. **Verify Setup**:
   - Navigate to `page-builder-framework-e2e-testing/`
   - Run `pnpm install` to install dependencies (including dotenv)
   - Run `pnpm test:chrome` to verify login + Customizer navigation visually
   - Credentials are loaded from `.env.local` at project root (WP_USERNAME, WP_PASSWORD)

3. **Stabilize Navigation + Login**:
   - Ensure `wpLogin` hits `http://mapsteps.local/wp-admin/` and waits for `#wpadminbar`.
   - Ensure `openCustomizer` navigates to `http://mapsteps.local/wp-admin/customize.php`, handles redirects to login, and retries.
   - Add/keep diagnostics in tests: log current URL; list panels/sections when needed.

4. **Header Builder Tests**:
   - Review Builder controls in `wp-content/themes/page-builder-framework/Customizer/Controls/Builder/`
   - Test enabling/disabling `wpbf_enable_header_builder`
   - Interact with rows/columns and drag-and-drop widgets
   - Test responsive device switcher (desktop/tablet/mobile)

5. **Optional (Later) Controls**:
   - Sortable: drag-and-drop reordering and item interactions
   - Media: image upload and media library selection
   - Code Editor: code input and syntax highlighting

6. **CI/CD (Manual Only)**:
   - CI workflow should be manual via `workflow_dispatch` only (no push/PR triggers)
   - Ensure theme installation/setup steps exist but do not auto-run
   - Consider adding test data seeding and visual regression later

7. **Document**:
   - Update README with new test patterns
   - Update `PROGRESS_HANDOFF.md` with results and next steps

**Important Notes**:

- Tests are in **`page-builder-framework-e2e-testing/`**
- Use existing custom commands in `helpers/commands/`
- Follow existing test patterns in `tests/customizer/controls/`
- If the test receives an HTTP 502 response, run the `wsm-restart-php` command.
- See README.md for documented WPBF control types and dependencies
- CI/CD workflow is in `.github/workflows/e2e-tests.yml` and is manual-only for now
