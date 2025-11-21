# Agent Prompt: Implement Mailjet Backend Choice (SMTP vs API)

## Objective

Extend the existing Mailjet implementation to allow users to choose between **Mailjet SMTP** or **Mailjet API** as the backend method for sending emails.

## Context

Currently, the plugin supports Mailjet via SMTP only. Mailjet also provides a REST API for sending emails, which has a key advantage: **emails sent via the API do not automatically save contacts to the Mailjet contact list**. This prevents hitting contact list limitations, making the API method more suitable for high-volume transactional emails.

The existing implementation includes:

- Mailer Type selection: `default` (Manual SMTP) or `mailjet` (Mailjet SMTP)
- Mailjet API Key and Secret Key fields
- SMTP configuration in `class-smtp-output.php`

## Instructions

### 1. Update Settings Module (`modules/settings/class-settings-module.php`)

#### A. Add "Mailjet Backend" Setting

- Add a new setting field `mailjet_backend` to the `weed-smtp-section`.
- Type: Radio buttons.
- Options:
  - `smtp`: "SMTP" (default)
  - `api`: "API"
- Default value: `smtp`.
- This field should only be visible when `mailer_type` is set to `mailjet`.

#### B. Update Sanitization

- Add sanitization for `mailjet_backend` in the `sanitize_settings` method.
- Allowed values: `smtp`, `api`.

#### C. Add Field Callback

- Create `mailjet_backend_field()` method to render the radio buttons.

### 2. Template Updates

#### A. Create New Template

- Create `modules/settings/templates/fields/smtp/mailjet-backend.php`.
- Render radio buttons for SMTP and API options.
- Add `data-show-when-mailer-type="mailjet"` attribute for conditional visibility.

### 3. Implement Mailjet API Support

#### A. Create New Email Sender Module

- Create `modules/mailjet-api/class-mailjet-api-sender.php`.
- Implement a method to send emails using Mailjet's Send API v3.1.
- API Endpoint: `https://api.mailjet.com/v3.1/send`
- Authentication: Basic Auth using API Key and Secret Key.
- Request format: JSON with proper message structure.

#### B. API Request Structure

```json
{
	"Messages": [
		{
			"From": {
				"Email": "sender@example.com",
				"Name": "Sender Name"
			},
			"To": [
				{
					"Email": "recipient@example.com",
					"Name": "Recipient Name"
				}
			],
			"Subject": "Email Subject",
			"TextPart": "Plain text content",
			"HTMLPart": "<h1>HTML content</h1>"
		}
	]
}
```

### 4. Update SMTP Output Module (`modules/smtp/class-smtp-output.php`)

#### A. Modify PHPMailer Hook Behavior

When `mailer_type` is `mailjet` AND `mailjet_backend` is `api`:

- **Do not configure PHPMailer** in `phpmailer_init()`.
- Instead, hook into `wp_mail` filter or `phpmailer_init` to intercept the email.
- Extract email data (to, subject, message, headers, attachments).
- Call the Mailjet API sender to send the email.
- Return success/failure appropriately.

When `mailer_type` is `mailjet` AND `mailjet_backend` is `smtp`:

- Keep the existing SMTP configuration (already implemented).

### 5. Error Handling

- Implement proper error handling for API requests.
- Log errors appropriately.
- Return meaningful error messages to WordPress.

## Definition of Done

- User can select "Mailjet Backend" when Mailjet is chosen as mailer type.
- Selecting "SMTP" uses the existing Mailjet SMTP implementation.
- Selecting "API" sends emails via Mailjet's Send API.
- Emails sent via API do not save contacts to Mailjet contact list.
- Settings are saved correctly.
- Error handling is implemented for API failures.

## Resources

- [Mailjet Send API Documentation](https://dev.mailjet.com/email/guides/send-api-v31/)
- Mailjet API Endpoint: `https://api.mailjet.com/v3.1/send`
- Authentication: Basic Auth with API Key as username and Secret Key as password
