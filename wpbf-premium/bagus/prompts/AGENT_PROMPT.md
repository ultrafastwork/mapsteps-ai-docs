# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Continue WPBF Premium development.

**Status**: Session v2.11.8+29 - Footer Builder premium integration complete.

---

## Background

### Footer Builder Premium Integration Complete

All Footer Builder premium controls have been integrated:

- **v2.11.8+27**: Added `footer_sticky` controls movement to Row 2 section
- **v2.11.8+28**: Added `footer_theme_author_name` and `footer_theme_author_url` controls movement to Copyright section

---

## Current State

Footer Builder premium integration is complete. The following controls are moved when footer builder is enabled:

| Control | Target Section |
|---------|---------------|
| `footer_sticky` | `wpbf_footer_builder_desktop_row_2_section` |
| `footer_theme_author_name` | `wpbf_footer_builder_desktop_copyright_section` |
| `footer_theme_author_url` | `wpbf_footer_builder_desktop_copyright_section` |

---

## Suggested Next Tasks

1. **Manual Testing**: Test Footer Builder premium controls in WordPress Customizer
2. **Additional Premium Controls**: Add more premium controls to footer builder widget sections (only if needed)
3. **Footer Builder Styles**: Create `footer-builder-styles.php` when premium controls with styling options are added
4. **New Feature Development**: Proceed with next feature request

---

## Instructions

1. Review the current state above
2. Discuss with the user what task to work on next
3. Implement the chosen task following existing patterns
