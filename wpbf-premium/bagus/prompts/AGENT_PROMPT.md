# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Implement Footer Builder output integration for custom content.

**Status**: Session v2.11.8+26 - Footer Builder output integration.

---

## Background

### Footer Builder Integration (v2.11.8+24)

Created `settings-footer-builder.php` with premium controls for footer builder row sections:

- Added "Custom Content" controls to all 6 footer builder row sections (desktop and mobile)
- Control IDs: `wpbf_footer_builder_{row_key}_custom` (code field for shortcodes)

### Footer Builder Postmessage Analysis (v2.11.8+25)

Analyzed postmessage requirements and determined:

- **No postmessage implementation needed** for premium footer builder controls
- Code fields with `partialRefresh` handle live preview via AJAX (server-side rendering)
- Theme's `footer-builder-rows.ts` handles styling controls (bg_color, text_color, etc.)

---

## Task: Footer Builder Output Integration

Implement output logic in theme's `FooterBuilderOutput.php` to render custom content when set.

### Implementation Steps

1. **Study theme's FooterBuilderOutput.php**:
   - Locate in `themes/page-builder-framework/inc/output/`
   - Understand how row content is rendered

2. **Add custom content rendering**:
   - Check if `wpbf_footer_builder_{row_key}_custom` has a value
   - If set, render the shortcode content instead of default row content
   - Use `do_shortcode()` to process shortcodes

3. **Test in customizer**:
   - Add an Elementor or Beaver Builder template shortcode
   - Verify it replaces the row content correctly

### Premium Footer Builder Controls

| Control ID | Purpose |
|------------|---------|
| `wpbf_footer_builder_desktop_row_1_custom` | Custom content for desktop top row |
| `wpbf_footer_builder_desktop_row_2_custom` | Custom content for desktop main row |
| `wpbf_footer_builder_desktop_row_3_custom` | Custom content for desktop bottom row |
| `wpbf_footer_builder_mobile_row_1_custom` | Custom content for mobile top row |
| `wpbf_footer_builder_mobile_row_2_custom` | Custom content for mobile main row |
| `wpbf_footer_builder_mobile_row_3_custom` | Custom content for mobile bottom row |

---

## Files Reference

| File | Purpose |
|------|---------|
| `inc/customizer/settings/settings-footer-builder.php` | Premium footer builder controls |
| Theme's `inc/output/FooterBuilderOutput.php` | Footer builder output rendering |

---

## Alternative Tasks

If output integration is complex or requires theme changes, consider:

1. **Controls Movement**: Move existing footer premium controls (sticky footer, theme author, etc.) to footer builder sections when enabled
2. **Additional Premium Controls**: Add more premium controls to footer builder widget sections (logo, menu, html, social, copyright)
