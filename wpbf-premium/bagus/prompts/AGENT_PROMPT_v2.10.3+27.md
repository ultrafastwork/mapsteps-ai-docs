# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Implement future enhancements for Footer Builder premium controls.

**Status**: Session v2.10.3+27 - Footer Builder controls movement.

---

## Background

### Footer Builder Integration Complete (v2.10.3+24 - v2.10.3+26)

- Created `settings-footer-builder.php` with premium "Custom Content" controls for all 6 row sections
- Implemented output hook in `customizer-functions.php` to filter `wpbf_footer_builder_row_content`
- Analyzed styles output - **No CSS styles needed** for current controls (page builder templates have their own styles)

---

## Available Tasks

Choose one of the following enhancement tasks:

### Option 1: Controls Movement

Move existing footer premium controls to footer builder sections when footer builder is enabled.

**Controls to Consider Moving**:
- Sticky footer (`footer_sticky`)
- Theme author credit
- Other footer-related premium controls

**Implementation Approach**:
1. Check if footer builder is enabled
2. Conditionally move/duplicate controls to appropriate footer builder sections
3. Ensure controls work in both legacy footer and footer builder modes

### Option 2: Additional Premium Controls

Add more premium controls to footer builder widget sections.

**Potential Controls**:
- Logo widget: Additional styling options
- Menu widget: Premium menu effects
- HTML widget: Advanced content options
- Social widget: Additional social platforms, styling
- Copyright widget: Advanced formatting options

**Implementation Approach**:
1. Identify which widgets need premium enhancements
2. Add controls to `settings-footer-builder.php`
3. Implement output hooks if needed
4. Add styles output if controls require CSS

### Option 3: Footer Builder Styles

Create `footer-builder-styles.php` when premium controls with styling options are added.

**When to Implement**:
- Only needed if Option 2 adds controls that require CSS output
- Follow existing pattern in `inc/customizer/styles/` directory

---

## Files Reference

| File | Purpose |
|------|---------|
| `inc/customizer/settings/settings-footer-builder.php` | Premium footer builder controls |
| `inc/customizer/customizer-functions.php` | Output hooks (custom content filter added here) |
| `inc/customizer/styles.php` | Main styles entry |
| `inc/customizer/styles/footer-styles.php` | Existing footer WIDGETS styles |

---

## Instructions

1. Review the available tasks above
2. Discuss with the user which enhancement to prioritize
3. Implement the chosen enhancement following existing patterns
