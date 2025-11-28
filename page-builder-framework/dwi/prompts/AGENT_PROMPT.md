# Agent Prompt

**Role**: You are an expert Node.js, WordPress, and test automation developer and AI coding assistant.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is the file:
`ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Please strictly follow the rules defined in:

1. `ai-docs/page-builder-framework/rules.md` (Project-specific rules)

**Objective**:
Build on the stabilized E2E smoke and Header Builder tests to **fix WordPress Customizer postMessage (instant preview) issues** in the Page Builder Framework theme. Focus on the live-preview behavior for:

- Mobile menu trigger (border radius & padding)
- Desktop off-canvas push menu (push effect & menu width)
- Mobile Header Builder buttons 1 & 2 (border radius, border width, border style)


**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/dwi/progress-handoffs/PROGRESS_HANDOFF.md` to understand the current state, known issues (e.g., redirects from customize.php), and required actions.

2. **E2E Context (Already Stabilized)**:
	- The Nightwatch smoke test (`pnpm test:smoke`) is already hardened and passing reliably.
	- The Header Builder test suite (`pnpm test:builder`) has been made more robust (reduced flakiness from panel/section opening and overly strict visibility checks).
	- You generally **do not** need to modify tests unless you introduce regressions or add new Customizer functionality that requires coverage.

3. **Primary Task: Fix Customizer postMessage Issues**:
	- Start from `wp-content/themes/page-builder-framework/inc/customizer/js/postmessage.ts` and the related `postmessage-parts/*` modules.
	- Use the current handoff file (`PROGRESS_HANDOFF.md`) as the source of truth for:
		- Which settings/controls are affected.
		- Which JS modules have already been analyzed.

	**3.1 Mobile Menu Trigger (Header Builder)**
	- Review and, if necessary, adjust:
		- `postmessage-parts/menu-triggers.ts`
		- `postmessage-parts/mobile-navigation.ts`
	- Ensure that the mobile trigger’s border radius and padding update in live preview according to the intended UX for all relevant styles (`simple`, `solid`, `outline`).

	**3.2 Desktop Off-Canvas Push Menu**
	- Review `postmessage-parts/off-canvas.ts` and the corresponding Customizer settings and markup.
	- Ensure that **both** menu width and push transform respond instantly to `off_canvas_width` (or the correct setting ID) via `postMessage`.

	**3.3 Mobile Header Builder Buttons 1 & 2**
	- Review `postmessage-parts/header-builder-buttons.ts`.
	- Ensure that border radius, border width, and border style for `mobile_button_1` and `mobile_button_2`:
		- Are wired to the correct setting IDs.
		- Use `transport => 'postMessage'`.
		- Target the correct selectors in the rendered header builder markup.

4. **CI/CD (Manual Only)**:
	- CI workflow should remain manual via `workflow_dispatch` only (no push/PR triggers).
	- Do not introduce automatic triggers; prioritize fast local Customizer iteration.

5. **Document**:
	- Update `PROGRESS_HANDOFF.md` with:
		- Any implemented postMessage fixes.
		- Verified live-preview patterns and remaining edge cases.
	- Only adjust E2E docs/README if you extend or change the test suite.

**Important Notes**:

- Tests are in **`page-builder-framework-e2e-testing/`**
- Use existing custom commands in `helpers/commands/`
- Follow existing test patterns in `tests/customizer/controls/`
- If the test receives an HTTP 502 response, run the `wsm-restart-php` command.
- See README.md for documented WPBF control types and dependencies
- CI/CD workflow is in `.github/workflows/e2e-tests.yml` and is manual-only for now
