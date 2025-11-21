# Agent Prompt: Remove Mailjet Sender Fields

**Status:** 🎯 Active
**Version:** v6.2.2+6
**Last Updated:** 2025-11-21

## Objective

Remove the Mailjet Sender Name and Mailjet Sender Email fields from the Mailjet API Settings section, as these fields are redundant (the sender information should come from the General Settings "From Email" and "From Name" fields).

## Context

The Mailjet API Settings currently has four fields:
- Mailjet API Key (keep)
- Mailjet Secret Key (keep)
- Sender Name (remove - redundant)
- Sender Email (remove - redundant)

The sender name and email should be taken from the General Settings section instead, making the configuration simpler and more consistent.

## Instructions

### 1. Remove Mailjet Sender Fields from Settings Module

- [ ] Modify `modules/settings/class-settings-module.php`:
    - [ ] **Remove Field Registration**: Remove the `add_settings_field` calls for:
        - `mailjet-sender-name`
        - `mailjet-sender-email`
    - [ ] **Remove Field Methods**: Remove or comment out the methods:
        - `mailjet_sender_name_field()`
        - `mailjet_sender_email_field()`

### 2. Remove Field Template Files

- [ ] Delete or archive the field template files:
    - [ ] `modules/settings/templates/fields/smtp/mailjet-sender-name.php`
    - [ ] `modules/settings/templates/fields/smtp/mailjet-sender-email.php`

### 3. Update Settings Sanitization

- [ ] Modify `modules/settings/class-settings-module.php`:
    - [ ] In the `sanitize_settings()` method, remove or comment out the sanitization for:
        - `mailjet_sender_name`
        - `mailjet_sender_email`

### 4. Verify Mailjet API Implementation

- [ ] Check if `modules/mailjet-api/class-mailjet-api-sender.php` uses these fields
- [ ] If used, update the implementation to use the General Settings fields instead:
    - Use `from_name` from general settings
    - Use `from_email` from general settings

## Expected Deliverables

1. Updated `class-settings-module.php` with removed field registrations and methods
2. Deleted or archived field template files
3. Updated sanitization logic
4. Verified/updated Mailjet API sender implementation (if needed)

## Definition of Done

- [ ] Mailjet Sender Name field is removed from settings
- [ ] Mailjet Sender Email field is removed from settings
- [ ] Mailjet API Settings section only shows API Key and Secret Key fields
- [ ] Mailjet API implementation uses General Settings for sender information
- [ ] Settings page loads without errors
- [ ] Settings save correctly after the removal

## Notes

- The "From Email" and "From Name" fields in General Settings should be used by the Mailjet API implementation
- This simplification makes the configuration more intuitive - users set sender info once in General Settings for all mailer types
