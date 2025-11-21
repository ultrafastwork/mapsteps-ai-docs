# Progress Handoff

**Current Version:** `v6.2.2+2`
**Status:** Active

## Pending Tasks

- [ ] **Implement Mailjet Backend Choice (SMTP vs API)**
  - [ ] Add `mailjet_backend` setting to choose between SMTP and API.
  - [ ] Create `modules/mailjet-api/class-mailjet-api-sender.php` for API implementation.
  - [ ] Update UI to show "Mailjet Backend" option when Mailjet is selected.
  - [ ] Modify `class-smtp-output.php` to route to API sender when API backend is selected.
  - [ ] Test email sending with both SMTP and API backends.
  - [ ] Verify that API method does not save contacts to Mailjet contact list.

## Context from Previous Session

The previous session (v6.2.2+1) successfully implemented basic Mailjet support with SMTP backend:

- Added Mailer Type selection (Default SMTP / Mailjet)
- Implemented conditional field visibility
- Configured Mailjet SMTP settings (in-v3.mailjet.com, port 587, TLS)
- All changes are in `modules/settings/` and `modules/smtp/`

## Next Steps for Agent

Please execute the instructions in: `ai-docs/welcome-email-editor/dwi/prompts/AGENT_PROMPT.md`

The goal is to extend Mailjet support by adding an API backend option, which will prevent contacts from being auto-saved to Mailjet's contact list.
