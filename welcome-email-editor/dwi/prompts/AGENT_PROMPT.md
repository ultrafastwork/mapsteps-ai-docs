# Agent Prompt: Verify Mailjet Implementation Correctness

## Objective

Review and verify that the Mailjet integration (both SMTP and API backends) is implemented correctly according to Mailjet's specifications and best practices.

## Context

The previous session (v6.2.2+3) implemented the Mailjet backend choice feature, allowing users to select between SMTP and API methods. Before manual testing, we need to ensure the implementation is correct.

## Current Implementation

### SMTP Backend
- **File:** `modules/smtp/class-smtp-output.php`
- **Configuration:**
  - Host: `in-v3.mailjet.com`
  - Port: `587`
  - Encryption: `STARTTLS`
  - Authentication: API Key (username) + Secret Key (password)

### API Backend
- **File:** `modules/mailjet-api/class-mailjet-api-sender.php`
- **Endpoint:** `https://api.mailjet.com/v3.1/send`
- **Authentication:** Basic Auth (API Key:Secret Key)
- **Method:** POST with JSON payload

## Instructions

### 1. Verify SMTP Configuration

Review `modules/smtp/class-smtp-output.php` and verify:

- [ ] **Host is correct**: Should be `in-v3.mailjet.com` (or check if there's a regional variant)
- [ ] **Port is correct**: `587` for STARTTLS or `465` for SSL
- [ ] **Encryption is correct**: Using `PHPMailer::ENCRYPTION_STARTTLS`
- [ ] **Authentication method**: API Key as username, Secret Key as password
- [ ] **No hardcoded credentials**: Using values from settings

**Reference:** [Mailjet SMTP Documentation](https://dev.mailjet.com/smtp-relay/overview/)

### 2. Verify API Implementation

Review `modules/mailjet-api/class-mailjet-api-sender.php` and verify:

- [ ] **Endpoint is correct**: `https://api.mailjet.com/v3.1/send` (not v3)
- [ ] **Authentication format**: Basic Auth with `base64_encode(api_key:secret_key)`
- [ ] **Request headers**: `Content-Type: application/json`
- [ ] **Payload structure**: Matches Mailjet Send API v3.1 spec
  - `Messages` array
  - `From` object with `Email` and `Name`
  - `To` array with objects containing `Email` and optionally `Name`
  - `Subject` string
  - `HTMLPart` and/or `TextPart`
- [ ] **Response handling**: Checks for `Status: "success"` in response
- [ ] **Error handling**: Logs appropriate error messages

**Reference:** [Mailjet Send API v3.1 Documentation](https://dev.mailjet.com/email/guides/send-api-v31/)

### 3. Verify Email Interception Logic

Review `modules/smtp/class-smtp-output.php` method `maybe_use_mailjet_api()`:

- [ ] **Filter hook is correct**: Using `pre_wp_mail` filter
- [ ] **Priority is appropriate**: Currently set to `10`
- [ ] **Return value handling**: Returns boolean to short-circuit `wp_mail()`
- [ ] **Conditional logic**: Only intercepts when both conditions are true:
  - `mailer_type === 'mailjet'`
  - `mailjet_backend === 'api'`

### 4. Check for Common Issues

- [ ] **Character encoding**: Verify UTF-8 handling for international characters
- [ ] **Email address parsing**: Check regex patterns for "Name <email>" format
- [ ] **Multiple recipients**: Verify array handling for multiple To addresses
- [ ] **Empty values**: Check handling of empty/missing headers
- [ ] **Content type detection**: Verify HTML vs plain text handling
- [ ] **Error propagation**: Ensure API errors are properly returned to WordPress

### 5. Review Security

- [ ] **Credentials storage**: API keys stored securely (sanitized on save)
- [ ] **No credentials in logs**: Error logs don't expose API keys
- [ ] **Input sanitization**: All user inputs properly sanitized
- [ ] **Output escaping**: Template outputs properly escaped

### 6. Verify Backward Compatibility

- [ ] **Default value**: `mailjet_backend` defaults to `'smtp'` if not set
- [ ] **Existing installations**: Won't break existing Mailjet SMTP setups
- [ ] **Graceful degradation**: Falls back to SMTP if API fails

## Expected Deliverables

1. **Code Review Report**: Document any issues found with specific line numbers
2. **Corrections**: Fix any incorrect implementations
3. **Recommendations**: Suggest improvements if any
4. **Documentation Updates**: Update implementation docs if corrections are made

## Definition of Done

- All verification checklist items reviewed
- Any issues found are documented and fixed
- Code follows Mailjet's official specifications
- Implementation is ready for manual testing

## Resources

- [Mailjet SMTP Relay Documentation](https://dev.mailjet.com/smtp-relay/overview/)
- [Mailjet Send API v3.1 Documentation](https://dev.mailjet.com/email/guides/send-api-v31/)
- [Mailjet API Authentication](https://dev.mailjet.com/email/guides/authentication/)

## Notes

- User will perform manual testing after verification is complete
- Focus on correctness, not testing
- Check against official Mailjet documentation
