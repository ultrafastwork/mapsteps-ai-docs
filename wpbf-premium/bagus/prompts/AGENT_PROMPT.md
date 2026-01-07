# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Continue wpbf-premium plugin development.

**Status**: Session v2.11.8+25 - Ready for next task.

---

## Recent Context

### Footer Builder Integration (v2.11.8+24)

Created `settings-footer-builder.php` with premium controls for footer builder row sections:

- Added "Custom Content" controls to all 6 footer builder row sections (desktop and mobile)
- Updated `customizer-settings.php` to require the new file

### Potential Enhancements

1. **Output Integration**: Implement output logic in theme's `FooterBuilderOutput.php` to render custom content when set
2. **Controls Movement**: Consider moving existing footer premium controls (sticky footer, theme author, etc.) to footer builder sections when enabled
3. **Additional Premium Controls**: Add more premium controls to footer builder widget sections (logo, menu, html, social, copyright)

---

## Task

Await instructions from the user for the next task.

---

## Notes

- Footer builder does **NOT** have off-canvas (unlike header builder) - footers are static content areas
- The custom content controls allow users to replace entire row content with page builder templates
- Theme's `FooterBuilderOutput.php` may need to be updated to check for and render custom content
