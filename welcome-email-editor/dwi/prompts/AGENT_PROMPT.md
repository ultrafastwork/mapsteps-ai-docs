# Agent Prompt: Setup Nightwatch v3 E2E Testing

**Status:** 🎯 Active
**Version:** v6.2.2+12
**Last Updated:** 2025-11-25

## Objective

Set up end-to-end (E2E) testing for the plugin using Nightwatch.js version 3. The goal is to establish a testing framework that can verify critical plugin functionalities.

## Directory Structure & Best Practices

**Location:** Tests MUST be placed inside the plugin repository to ensure they are version-controlled with the code they test.
-   **Path:** `wp-content/plugins/welcome-email-editor/tests/e2e/`
-   **Build Exclusion:** Ensure that the `tests/` directory, `nightwatch.conf.js`, and `node_modules` are **excluded** from the final production zip/build of the plugin. (If a build script or `.distignore` exists, update it).

## Requirements

1.  **Install Nightwatch v3:**
    -   Initialize Nightwatch in the plugin root (`wp-content/plugins/welcome-email-editor/`).
    -   Use `npm` for dependency management.
    -   Select "TypeScript" if the project is already using it.
    -   Select "Chrome" as the primary browser.

2.  **Configuration:**
    -   Configure `nightwatch.conf.js` (or `.ts`).
    -   Set up a base URL for the local WordPress instance. **IMPORTANT:** Ask the user for their local WordPress URL (e.g., `http://mapsteps.test`) before finalizing the config.

3.  **Create First Test:**
    -   Create a basic test in `tests/e2e/specs/` to verify the plugin settings page loads correctly.
    -   Example: Navigate to the settings page and assert that the "Swift SMTP" header is visible.

4.  **Scripts:**
    -   Add npm scripts to `package.json` for running tests (e.g., `npm run test:e2e`).

## Context

The user is concerned about cluttering the plugin with test files.
**Solution:** We keep the source clean by organizing tests in `tests/e2e` and ensure they are NOT included in the distributed version of the plugin.

## Instructions

### 1. Installation
- Run `npm init nightwatch@latest` in the plugin directory.
- Follow the prompts (TypeScript: Yes, Browser: Chrome).

### 2. Configuration
- Update `nightwatch.conf.js` to point `src_folders` to `tests/e2e`.
- Configure the `baseUrl`.

### 3. Implementation
- Create `tests/e2e/specs/settings-load.spec.ts`.
- Write a simple test to check for the plugin title.

### 4. Build Exclusion (Crucial)
- Check for a `.distignore` file or build script.
- Add `tests/`, `nightwatch.conf.js`, and `test_results/` to the exclusion list to address the user's concern.

## Resources
- [Nightwatch.js v3 Documentation](https://nightwatchjs.org/)
