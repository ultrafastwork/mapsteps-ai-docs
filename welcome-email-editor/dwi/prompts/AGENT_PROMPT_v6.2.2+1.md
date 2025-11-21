# Agent Prompt: Implement Mailjet Support

## Objective

Implement Mailjet support in the Settings module of the `welcome-email-editor` plugin.

## Context

Currently, the settings module (`modules/settings`) supports manual SMTP settings. We need to add "Mailjet" as a supported mailer.
This involves adding a "Mailer Type" selection and specific fields for Mailjet (API Key and Secret Key).

## Instructions

### 1. Modify `modules/settings/class-settings-module.php`

#### A. Add "Mailer Type" Setting

- Add a new setting field `mailer_type` to the `weed-smtp-section`.
- Type: Radio buttons.
- Options:
  - `default`: "Default (SMTP)" - This should correspond to the existing manual SMTP settings.
  - `mailjet`: "Mailjet"
- Default value: `default`.

#### B. Add Mailjet Fields

- Add the following fields to the `weed-smtp-section`:
  - `mailjet_api_key`: "Mailjet API Key"
  - `mailjet_secret_key`: "Mailjet Secret Key"

#### C. Update Sanitization

- Update the `sanitize_settings` method to handle `mailer_type`, `mailjet_api_key`, and `mailjet_secret_key`.

### 2. Implement Conditional Logic (UI)

- The settings page should dynamically show/hide fields based on the selected `mailer_type`.
- If `default` is selected: Show existing SMTP fields (`smtp_host`, `smtp_port`, etc.) and HIDE Mailjet fields.
- If `mailjet` is selected: Show Mailjet fields and HIDE existing SMTP fields.
- You may need to update `assets/js/settings.js` (or create a new JS handler) to implement this toggle logic.

### 3. Modify `modules/smtp/class-smtp-output.php`

- Update `phpmailer_init` method to check `mailer_type`.
- If `mailer_type` is `mailjet`:
  - Set `Host` to `in-v3.mailjet.com`.
  - Set `Port` to `587`.
  - Set `SMTPSecure` to `tls`.
  - Set `Username` to `mailjet_api_key`.
  - Set `Password` to `mailjet_secret_key`.
  - Set `SMTPAuth` to `true`.
- If `mailer_type` is `default` (or unset):
  - Use existing logic (Custom SMTP settings).

### 4. Template Updates

- Create necessary template callbacks/files for the new fields in `modules/settings/templates/fields/`.

## Definition of Done

- User can select between "Default" and "Mailjet" in the SMTP settings.
- Selecting "Mailjet" reveals API Key and Secret Key fields and hides manual SMTP fields.
- Settings are saved correctly.
