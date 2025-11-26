# Agent Prompt: Verify and Expand E2E Test Script Correctness

**Status:** 🎯 Active
**Version:** v6.2.2+13
**Last Updated:** 2025-11-26

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)
2. `.antigravityignore` (Forbidden files and directories that you MUST NOT access)
3. `ai-docs/welcome-email-editor/rules.md` (Project-specific rules)

## Objective

Verify the correctness of the existing E2E test scripts and implement new comprehensive tests for email functionality. The primary focus is to ensure that the test scripts themselves are robust, logically correct, and accurately validate the plugin's behavior (SMTP and Mailjet API configurations).

## Background

The E2E testing framework is set up, but we need to ensure the tests are doing what they are supposed to do.
- **Location:** `c:\laragon\www\mapsteps\welcome-email-editor-e2e-testing\`
- **Framework:** Nightwatch v3.12.3
- **Authentication:** WordPress login working (`nightwatch` user)
- **Base URL:** `http://mapsteps.local`
- **First test:** Passing (3 assertions)

## Requirements

### 1. Verify Existing Test Correctness
- Review `tests/specs/settings-load.spec.ts` and `tests/helpers/auth.js`.
- Ensure assertions are meaningful and not just checking for existence of generic elements.
- Verify that the authentication helper handles edge cases (e.g., already logged in, login failure).
- **Goal:** Confirm the foundation is solid before building on top of it.

### 2. SMTP Mailer Type Testing (Correctness Focus)
- **Configuration:**
  - Test that selecting "SMTP (Default)" *actually* reveals SMTP fields and *hides* Mailjet fields.
  - Verify that saving settings *actually* persists them (reload page and check values).
- **Functionality:**
  - Send test email.
  - **Crucial:** Verify the *result* of the sending operation. Don't just check if the button was clicked; check for success/error messages.

### 3. Mailjet API Mailer Type Testing (Correctness Focus)
- **Configuration:**
  - Test that selecting "Mailjet API" *actually* reveals Mailjet fields and *hides* SMTP fields.
  - Verify persistence of API keys and settings.
- **Functionality:**
  - Send test email.
  - **Crucial:** Verify the *result* (success/error message).
  - Test attachment support if possible, or at least verify the UI elements for it.

### 4. Robustness and Validation
- **Field Visibility:** Ensure dynamic switching doesn't throw JS errors.
- **Form Validation:** Test that invalid inputs (e.g., bad email format) are caught by the UI *before* submission if client-side validation exists, or by the server response if not.
- **Error Handling:** Ensure the tests fail gracefully with clear messages if something goes wrong.

## Test Organization

### Recommended Structure
```
tests/specs/
├── settings-load.spec.ts          # (Review & Refine)
├── smtp-correctness.spec.ts       # (NEW) SMTP logic verification
├── mailjet-correctness.spec.ts    # (NEW) Mailjet logic verification
└── ui-logic.spec.ts               # (NEW) Visibility & switching logic
```

### Helper Functions
- Refine `tests/helpers/auth.js` if needed.
- Create `tests/helpers/settings.js` for robust interaction with form fields.

## Implementation Steps

### Step 1: Review and Refine
- Audit existing tests.
- Run them to confirm they pass *for the right reasons*.

### Step 2: Implement Logic Verification Tests
- Create tests that specifically target the *logic* of the settings page (visibility, persistence).
- Use `browser.expect.element(...).to.be.visible` vs `.to.be.present` carefully.

### Step 3: Implement Functional Verification Tests
- Create tests for the "Send Test Email" flow.
- Ensure assertions cover the full lifecycle of the action (Click -> Wait -> Verify Result).

### Step 4: Run and Validate
- Run all tests.
- **Self-Correction:** If a test passes but shouldn't (false positive), fix the test. If it fails, determine if it's a bug in the plugin or the test.

## Success Criteria
✅ Existing tests verified for correctness.
✅ New tests implemented for SMTP and Mailjet logic.
✅ Tests accurately reflect the state of the application (no false positives).
✅ Comprehensive coverage of email functionality.

## Resources
- **Nightwatch API:** https://nightwatchjs.org/api/
- **Existing Code:** `welcome-email-editor-e2e-testing/`

---

**Status:** 🎯 Ready to verify and expand test correctness
