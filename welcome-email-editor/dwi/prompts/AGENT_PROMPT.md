# Agent Prompt: Implement Test Email Metabox Visibility

**Status:** 🎯 Active
**Version:** v6.2.2+10
**Last Updated:** 2025-11-22

## Objective

Implement visibility logic for the Test Email metaboxes in the settings page. The goal is to ensure that only the relevant test email section is displayed based on the selected "Mailer Type".

## Requirements

1.  **Mailjet API Test Metabox:**
    - Show ONLY when "Mailer Type" is set to "Mailjet API".
    - Hide when "Mailer Type" is set to "SMTP (Default)".

2.  **SMTP Test Metabox:**
    - Show ONLY when "Mailer Type" is set to "SMTP (Default)".
    - Hide when "Mailer Type" is set to "Mailjet API".

## Context

Currently, both test sections might be visible or not toggling correctly when the mailer type changes. The visibility logic needs to be enforced in the JavaScript/TypeScript handlers and potentially in the initial PHP rendering (or via CSS/JS on load).

## Instructions

### 1. Investigate Current Implementation
- Check `modules/settings/templates/settings-template.php` to see how metaboxes are rendered.
- Check `assets-src/ts/settings.ts` (or `test-emails.ts`) to see existing visibility logic.
- Identify the IDs or classes used for the test email metaboxes.

### 2. Implement Visibility Logic
- Update the JavaScript/TypeScript to listen for changes on the "Mailer Type" selector.
- Add logic to toggle the display of the test email metaboxes accordingly.
- Ensure the correct state is applied on page load.

### 3. Verify
- Test switching between "SMTP (Default)" and "Mailjet API".
- Confirm the correct test section appears and the other disappears immediately.
- Reload the page to ensure the state persists visually based on the saved setting.

## Files to Check
- `modules/settings/templates/settings-template.php`
- `assets-src/ts/settings.ts`
- `assets-src/scss/settings.scss` (if CSS helper classes are needed)
