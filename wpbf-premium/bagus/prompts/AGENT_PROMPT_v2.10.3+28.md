# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Implement future enhancements for Footer Builder premium controls.

**Status**: Session v2.10.3+28 - Footer Builder future enhancements.

---

## Background

### Footer Builder Controls Movement Complete (v2.10.3+27)

- Removed unwanted `_custom` controls feature (didn't match header builder pattern)
- Added proper controls movement for `footer_sticky` to `wpbf_footer_builder_desktop_row_2_section`
- Deleted `settings-footer-builder.php` (contained only `_custom` controls)
- Removed `wpbf_footer_builder_row_content` filter from both plugin and theme

---

## Available Tasks

Choose one of the following enhancement tasks:

### Option 1: Additional Controls Movement

Move more existing footer premium controls to footer builder sections.

**Controls to Consider Moving**:
- `footer_theme_author_name` → footer builder copyright widget section
- `footer_theme_author_url` → footer builder copyright widget section

### Option 2: Additional Premium Controls

Add more premium controls to footer builder widget sections.

**Potential Controls**:
- Logo widget: Additional styling options
- Menu widget: Premium menu effects
- HTML widget: Advanced content options
- Social widget: Additional social platforms, styling
- Copyright widget: Advanced formatting options

### Option 3: Footer Builder Styles

Create `footer-builder-styles.php` when premium controls with styling options are added.

**When to Implement**:
- Only needed if Option 2 adds controls that require CSS output
- Follow existing pattern in `inc/customizer/styles/` directory

---

## Files Reference

| File | Purpose |
|------|---------|
| `inc/customizer/js/customizer.ts` | Controls movement (footer builder added in v2.10.3+27) |
| `inc/customizer/customizer-functions.php` | Output hooks |
| `inc/customizer/styles.php` | Main styles entry |
| `inc/customizer/styles/footer-styles.php` | Existing footer WIDGETS styles |

---

## Instructions

1. Review the available tasks above
2. Discuss with the user which enhancement to prioritize
3. Implement the chosen enhancement following existing patterns
