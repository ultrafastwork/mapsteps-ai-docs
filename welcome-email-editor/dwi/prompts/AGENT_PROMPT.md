# Agent Prompt: Expand E2E Test Coverage for Email Functionality

**Status:** 🎯 Active
**Version:** v6.2.2+13
**Last Updated:** 2025-11-25

## Objective

Expand the existing Nightwatch v3 E2E test suite to comprehensively test all email functionality of the Welcome Email Editor plugin. Verify that both SMTP and Mailjet API mailer types work correctly with their respective configurations.

## Background

The E2E testing framework is already set up and operational:
- **Location:** `c:\laragon\www\mapsteps\welcome-email-editor-e2e-testing\`
- **Framework:** Nightwatch v3.12.3
- **Authentication:** WordPress login working (`nightwatch` user)
- **Base URL:** `http://mapsteps.local`
- **First test:** Passing (3 assertions)

## Requirements

### 1. SMTP Mailer Type Testing

Test the complete SMTP configuration flow:

**Configuration Tests:**
- Select "SMTP (Default)" as Mailer Type
- Verify SMTP-specific fields are visible:
  - SMTP Host
  - SMTP Port
  - Encryption (None/SSL/TLS)
  - SMTP Username
  - SMTP Password
- Verify Mailjet API fields are hidden when SMTP is selected
- Save SMTP configuration and verify settings persist

**Functionality Tests:**
- Send test email using SMTP configuration
- Verify test email form is visible for SMTP
- Verify test email can be sent successfully
- Check for success/error messages

### 2. Mailjet API Mailer Type Testing

Test the complete Mailjet API configuration flow:

**Configuration Tests:**
- Select "Mailjet API" as Mailer Type
- Verify Mailjet API-specific fields are visible:
  - Mailjet API Key
  - Mailjet Secret Key
  - Sender Name
  - Sender Email
- Verify SMTP fields are hidden when Mailjet API is selected
- Save Mailjet API configuration and verify settings persist

**Functionality Tests:**
- Send test email using Mailjet API
- Verify test email form is visible for Mailjet API
- Verify test email can be sent successfully
- Check for success/error messages
- Test attachment support (if applicable)

### 3. Field Visibility & Switching Tests

**Dynamic Visibility:**
- Test switching between SMTP and Mailjet API
- Verify correct fields show/hide when switching
- Verify correct test email metabox shows/hides
- Ensure no JavaScript errors during switching

**Form Validation:**
- Test required field validation for both mailer types
- Test email format validation
- Test API key format validation (Mailjet)

### 4. Settings Persistence

**Save & Reload:**
- Save SMTP settings, reload page, verify values persist
- Save Mailjet settings, reload page, verify values persist
- Switch mailer types, verify selection persists

## Test Organization

### Recommended Test Structure

```
tests/specs/
├── settings-load.spec.ts          # (Existing - authentication)
├── smtp-configuration.spec.ts     # (NEW) SMTP setup & config
├── smtp-email-sending.spec.ts     # (NEW) SMTP test email
├── mailjet-configuration.spec.ts  # (NEW) Mailjet setup & config
├── mailjet-email-sending.spec.ts  # (NEW) Mailjet test email
└── mailer-type-switching.spec.ts  # (NEW) Field visibility & switching
```

### Helper Functions Needed

Consider creating additional helpers in `tests/helpers/`:

- `settings-helpers.js` - Functions to interact with settings fields
- `email-helpers.js` - Functions to send test emails
- `selectors.js` - Centralized CSS selectors for the settings page

## Implementation Steps

### Step 1: Explore the Settings Page
- Navigate to Swift SMTP settings
- Identify CSS selectors for all form fields
- Identify selectors for mailer type dropdown/radio
- Identify selectors for test email forms
- Document the page structure

### Step 2: Create Helper Functions
- `selectMailerType(browser, type)` - Switch mailer type
- `fillSMTPSettings(browser, config)` - Fill SMTP form
- `fillMailjetSettings(browser, config)` - Fill Mailjet form
- `sendTestEmail(browser, emailAddress)` - Send test email
- `assertFieldVisible(browser, selector)` - Check visibility
- `assertFieldHidden(browser, selector)` - Check hidden

### Step 3: Create Test Specifications
- Write comprehensive tests for each scenario
- Use descriptive test names
- Add assertions for both positive and negative cases
- Include wait times for AJAX operations

### Step 4: Run and Verify
- Run all tests in headless mode
- Verify all tests pass
- Fix any failures
- Document any issues or limitations

## Test Data Requirements

### SMTP Configuration
You may need test SMTP credentials. Options:
- Use a test SMTP service (e.g., Mailtrap, MailHog)
- Use user's existing SMTP settings (ask if needed)
- Mock SMTP responses (if possible)

### Mailjet API Configuration
You may need test Mailjet credentials. Options:
- Use test Mailjet sandbox credentials (ask user)
- Use user's existing Mailjet settings
- Mock API responses (if possible)

### Test Email Address
- Use a test email address for sending test emails
- Could be: `test@example.com` or ask user for preference

## Important Considerations

### 1. Asynchronous Operations
- Settings save operations are likely AJAX-based
- Wait for success messages before proceeding
- Use proper `waitForElementVisible()` for dynamic content

### 2. Test Isolation
- Each test should be independent
- Reset state between tests if needed
- Don't rely on test execution order

### 3. Error Handling
- Test both success and failure scenarios
- Verify error messages are displayed correctly
- Handle timeouts gracefully

### 4. Page Object Pattern (Optional but Recommended)
- Create a `SettingsPage` class/object
- Encapsulate all settings page interactions
- Makes tests more maintainable and readable

## Success Criteria

✅ All tests pass successfully
✅ Both SMTP and Mailjet API configurations tested
✅ Field visibility switching works correctly
✅ Test email sending works for both mailer types
✅ Settings persistence verified
✅ No regression in existing authentication test
✅ Comprehensive test coverage documented

## Resources

- **Existing Tests:** `tests/specs/settings-load.spec.ts`
- **Authentication Helper:** `tests/helpers/auth.js`
- **Nightwatch Docs:** https://nightwatchjs.org/api/
- **Nightwatch Assertions:** https://nightwatchjs.org/api/assertions/

## Notes

- The authentication test is already working, build upon that foundation
- Reuse the `loginToWordPress()` and `goToSwiftSMTPSettings()` helpers
- Start with simple tests and gradually increase complexity
- Document any assumptions or limitations

---

**Status:** 🎯 Ready to implement comprehensive E2E testing
