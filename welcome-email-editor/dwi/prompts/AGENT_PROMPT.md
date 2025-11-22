# Agent Prompt: Add Mailjet API Test Email Section

**Status:** 🎯 Active
**Version:** v6.2.2+8
**Last Updated:** 2025-11-22

## Objective

Add a dedicated "Send Test Email" section for Mailjet API in the settings page, allowing users to test both regular emails and emails with attachments using the Mailjet API.

## Context

Currently, the plugin has a "Send Test Email" section that tests SMTP functionality. We need to add a similar section specifically for Mailjet API to allow users to:
- Test basic email sending via Mailjet API
- Test email with attachment functionality
- Verify Mailjet API configuration independently from SMTP

## Current Implementation

**Existing:** 
- Settings page has "Send Test Email" section for SMTP testing
- Located in: `modules/settings/templates/settings-template.php`
- AJAX handler in: `modules/settings/ajax/class-test-emails.php`
- Test email template in: `modules/settings/templates/emails/smtp-test-*.php`

## Instructions

### 1. Add Mailjet API Test Section to Settings Page

- [ ] Modify `modules/settings/class-settings-module.php`:
    - [ ] Add new settings section: `weed-mailjet-api-test-section`
    - [ ] Add settings field for Mailjet API test email with callback method
    - [ ] Create `mailjet_api_test_field()` method

### 2. Create Field Template

- [ ] Create new template file:
    - [ ] `modules/settings/templates/fields/mailjet-api/test-email.php`
    - [ ] Include recipient email input field
    - [ ] Add "Test Regular Email" button
    - [ ] Add "Test Email with Attachment" button
    - [ ] Add section visibility control: `data-show-when-mailer-type="mailjet_api"`

### 3. Create AJAX Handler

- [ ] Create or update `modules/settings/ajax/class-test-emails.php`:
    - [ ] Add method `test_mailjet_api_email()` for regular email test
    - [ ] Add method `test_mailjet_api_with_attachment()` for attachment test
    - [ ] Generate sample PDF/image attachment for testing
    - [ ] Return success/error response

### 4. Update JavaScript

- [ ] Update `assets/js/settings.js`:
    - [ ] Add AJAX handler for Mailjet API test email buttons
    - [ ] Add nonce for Mailjet API test actions
    - [ ] Display success/error messages

### 5. Create Test Email Templates (Optional)

- [ ] Consider creating Mailjet-specific test email templates:
    - [ ] `modules/settings/templates/emails/mailjet-api-test-html-email.php`
    - [ ] `modules/settings/templates/emails/mailjet-api-test-text-email.php`
    - [ ] Or reuse existing SMTP test templates

## Expected Deliverables

1. New "Send Test Email (Mailjet API)" settings section
2. Field template with two test buttons
3. AJAX handler methods for both test scenarios
4. Updated JavaScript with AJAX calls and response handling
5. Visibility control based on Mailer Type selection

## Definition of Done

- [ ] Mailjet API test section appears in settings when "Mailjet API" is selected
- [ ] "Test Regular Email" button sends email via Mailjet API successfully
- [ ] "Test Email with Attachment" button sends email with sample attachment
- [ ] Success/error messages display correctly
- [ ] Section visibility toggles correctly with Mailer Type selection
- [ ] No JavaScript errors in browser console

## Notes

- The test section should only be visible when Mailer Type is set to "Mailjet API"
- For attachment testing, generate a simple test file (e.g., small PDF or text file) programmatically
- Reuse existing SMTP test email templates if possible to maintain consistency
- Follow the same pattern as the existing SMTP test email functionality

## Testing Recommendations

1. Select "Mailjet API" as mailer type
2. Verify Mailjet API test section appears
3. Click "Test Regular Email" and verify receipt
4. Click "Test Email with Attachment" and verify attachment received
5. Switch to "SMTP" and verify section hides
6. Check error handling with invalid API credentials
