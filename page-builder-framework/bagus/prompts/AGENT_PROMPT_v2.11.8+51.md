# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Awaiting next task assignment.

**Status**: Session v2.11.8+51 - Footer Builder implementation complete.

---

## Previous Session Summary (v2.11.8+50)

Footer Builder vs Header Builder verification completed successfully. All 6 verification aspects passed:

1. ✅ Existing Controls Handling - Premium controls movement matches
2. ✅ New Controls - Row and widget controls implemented
3. ✅ Fields Output - Output classes follow same patterns
4. ✅ Styles Output - CSS generation matches header builder
5. ✅ Postmessage Scripts - Live preview handlers implemented
6. ✅ Premium Plugin Integration - Controls movement configured

**Result**: No code changes required. Footer Builder implementation already matches Header Builder pattern.

---

## Suggested Next Tasks

The Footer Builder feature is complete. Suggested next steps:

1. **Manual Testing** - Test Footer Builder in WordPress Customizer to ensure all controls work correctly
2. **Documentation** - Update user documentation for the new Footer Builder feature
3. **Bug Fixes** - Address any bugs reported from testing
4. **New Feature** - Proceed with next feature request from the team

---

## Footer Builder Reference

### Key Files

| Category | File |
|----------|------|
| Config | `Customizer/FooterBuilder/FooterBuilderConfig.php` |
| Output | `Customizer/FooterBuilder/FooterBuilderOutput.php` |
| Settings | `inc/customizer/settings/settings-footer-builder.php` |
| Postmessage | `inc/customizer/js/postmessage-parts/footer-builder-rows.ts` |
| Styles | `inc/customizer/styles/footer-builder-styles.php` |
| Premium | `wpbf-premium/inc/customizer/js/customizer.ts` |

### CSS Class Pattern

- Desktop rows: `.wpbf-footer-row-desktop_row_1`, `.wpbf-footer-row-desktop_row_2`, `.wpbf-footer-row-desktop_row_3`
- Mobile rows: `.wpbf-footer-row-mobile_row_1`, `.wpbf-footer-row-mobile_row_2`, `.wpbf-footer-row-mobile_row_3`
