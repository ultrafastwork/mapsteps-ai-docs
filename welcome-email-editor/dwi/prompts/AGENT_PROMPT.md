# Agent Prompt: Fix Mailjet API Test Email 500 Error

**Status:** 🎯 Active
**Version:** v6.2.2+9
**Last Updated:** 2025-11-22

## Objective

Debug and fix the 500 error that occurs when testing Mailjet API email sending functionality in the test email section.

## Problem Description

After implementing the Mailjet API test email section (v6.2.2+8), manual testing revealed a 500 Internal Server Error when attempting to send test emails via Mailjet API.

**Error Details:**
- **Location:** Mailjet API test email section in settings
- **Trigger:** Clicking "Test Regular Email" or "Test Email with Attachment" buttons
- **Response:** 500 Internal Server Error
- **Expected:** Success message and email delivery via Mailjet API

## Context

The Mailjet API test email section was recently implemented with:
- AJAX handlers in `modules/settings/ajax/class-test-emails.php`
  - `test_mailjet_api_email()` method for regular email test
  - `test_mailjet_api_with_attachment()` method for attachment test
- Both methods use `Mailjet_Api_Sender::get_instance()->send_email()`
- Proper nonce verification is in place
- JavaScript properly sends AJAX requests

## Instructions

### 1. Investigate the Error

- [ ] Check WordPress debug logs for PHP errors
- [ ] Add error logging to the AJAX handler methods
- [ ] Verify Mailjet API credentials are configured correctly
- [ ] Check if Mailjet_Api_Sender class is being loaded properly
- [ ] Inspect the AJAX request/response in browser developer tools

### 2. Common Issues to Check

- [ ] **Namespace Issues:** Verify `\Weed\Mailjet_Api\Mailjet_Api_Sender` is correctly referenced
- [ ] **Class Loading:** Ensure Mailjet API sender class is autoloaded/required
- [ ] **Method Signature:** Verify `send_email()` method parameters match usage
- [ ] **API Credentials:** Check if API key and secret key are properly retrieved from settings
- [ ] **Error Handling:** Ensure proper error handling in Mailjet API sender
- [ ] **File Permissions:** For attachment test, verify temp file creation permissions

### 3. Debug Approach

1. Enable WordPress debugging:
   - Set `WP_DEBUG` to `true`
   - Set `WP_DEBUG_LOG` to `true`
   - Check `wp-content/debug.log` for errors

2. Add temporary logging in AJAX handler:
   ```php
   error_log('Mailjet API Test: Starting...');
   error_log('Recipient: ' . $recipient);
   error_log('Mailjet Sender exists: ' . (class_exists('\Weed\Mailjet_Api\Mailjet_Api_Sender') ? 'yes' : 'no'));
   ```

3. Test the Mailjet API sender directly in a test script if needed

4. Verify AJAX nonce and action are correct

### 4. Fix the Issue

- [ ] Identify the root cause from error logs
- [ ] Implement the fix in the appropriate file(s)
- [ ] Test both regular email and email with attachment
- [ ] Ensure proper error messages are returned to the user
- [ ] Verify no JavaScript console errors

### 5. Validation

- [ ] Test email sending with valid Mailjet API credentials
- [ ] Test error handling with invalid credentials
- [ ] Verify attachment test creates and cleans up temp file properly
- [ ] Confirm success/error messages display correctly
- [ ] Test on both regular and attachment scenarios

## Files to Check

**AJAX Handler:**
- `modules/settings/ajax/class-test-emails.php` (lines 239-314)
  - `test_mailjet_api_email()` method
  - `test_mailjet_api_with_attachment()` method

**Mailjet API Sender:**
- `modules/mailjet-api/class-mailjet-api-sender.php`
  - Check `send_email()` method signature and implementation
  - Verify error handling

**Settings Module:**
- `modules/settings/class-settings-module.php`
  - Check if settings are being retrieved correctly for API credentials

## Expected Outcome

- ✅ Test emails send successfully via Mailjet API
- ✅ Appropriate success messages display
- ✅ Error handling works correctly with invalid credentials
- ✅ No 500 errors occur
- ✅ Attachment test properly creates, sends, and cleans up temp files

## Notes

- The SMTP test email functionality works correctly, so the issue is specific to Mailjet API
- The JavaScript AJAX implementation appears correct based on the pattern
- Focus debugging on the PHP side, particularly the AJAX handler and Mailjet API sender integration

---

**Priority:** High - Blocking feature functionality
