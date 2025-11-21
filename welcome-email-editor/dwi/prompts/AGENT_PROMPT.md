# Agent Prompt: Refactor Settings Sections & Visibility

## Objective

Reorganize the settings fields to improve usability by moving the "Mailer Type" to General Settings and creating a dedicated section for Mailjet API configuration. Ensure field visibility logic aligns with the selected mailer type.

## Context

The user wants to separate the configuration for different mailers more clearly.
- **Mailer Type** should be a high-level setting in **General Settings**.
- **Mailjet API** fields should have their own dedicated section.
- **SMTP** fields should remain in the SMTP section (or be hidden when not in use).

## Instructions

### 1. Reorganize Settings Sections

- [ ] Modify `modules/settings/class-settings-module.php`:
    - [ ] **Move "Mailer Type"**: Change the section for the `mailer-type` field to `weed-general-section`.
    - [ ] **Create New Section**: Register a new settings section for "Mailjet API Settings" (e.g., `weed-mailjet-api-section`).
    - [ ] **Move Mailjet Fields**: Move the following fields to the new "Mailjet API Settings" section:
        - `mailjet-api-key`
        - `mailjet-secret-key`
        - `mailjet-sender-name`
        - `mailjet-sender-email`

### 2. Update Visibility Logic

- [ ] Update `assets/js/settings.js` (and potentially PHP templates if they use data attributes for parent sections) to ensure:
    - **When "SMTP (Default)" is selected:**
        - **Show:** SMTP Host, SMTP Encryption, SMTP Port, SMTP Username, SMTP Password.
        - **Hide:** Mailjet API Key, Mailjet Secret Key, Sender Name, Sender Email.
        - *Note:* Consider if the entire "Mailjet API Settings" section should be hidden.
    - **When "Mailjet API" is selected:**
        - **Show:** Mailjet API Key, Mailjet Secret Key, Sender Name, Sender Email.
        - **Hide:** SMTP Host, SMTP Encryption, SMTP Port, SMTP Username, SMTP Password.
        - *Note:* Consider if the entire "SMTP Settings" section should be hidden.

## Expected Deliverables

1. `class-settings-module.php` with reorganized fields and sections.
2. Updated `settings.js` handling the visibility of these specific fields (and/or sections).

## Definition of Done

- [ ] "Mailer Type" is located in the "General Settings" section.
- [ ] A new "Mailjet API Settings" section exists containing the Mailjet-specific fields.
- [ ] Selecting "SMTP (Default)" shows only SMTP fields and hides Mailjet fields.
- [ ] Selecting "Mailjet API" shows only Mailjet fields and hides SMTP fields.
- [ ] Settings are saved correctly after the reorganization.
