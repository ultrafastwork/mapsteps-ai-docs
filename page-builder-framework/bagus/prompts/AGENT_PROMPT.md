# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Test Footer Builder in Customizer.

**Status**: Session v2.11.8+49 - Footer Builder testing.

---

## Background

The **Footer Builder** feature is now complete with:
- Widget and slot definitions (`FooterBuilderConfig.php`)
- Frontend rendering (`FooterBuilderOutput.php`)
- Controls movement (v2.11.8+46)
- Postmessage support for live preview (v2.11.8+47)
- CSS output for row controls (v2.11.8+48)

---

## Task: Test Footer Builder in Customizer

### Test 1: Verify CSS Output Persists After Page Refresh

1. Open WordPress Customizer
2. Navigate to Footer Builder section
3. Configure row controls for desktop_row_1 and desktop_row_3:
   - Set `max_width` to a custom value (e.g., 1000px)
   - Set `vertical_padding` to a custom value (e.g., 30px)
   - Set `bg_color` to a visible color
   - Set `text_color` to a visible color
   - Set `accent_colors` (default and hover)
   - Set `font_size` to a custom value
4. Save and publish
5. Refresh the page
6. Verify styles persist

### Test 2: Verify Live Preview Works

1. Open WordPress Customizer
2. Change row control values
3. Verify changes appear immediately in preview (without refresh)
4. Verify no conflicts between CSS output and live preview

### Test 3: Mobile Rows

1. Test mobile_row_1 and mobile_row_3 controls
2. Verify mobile rows don't have max_width control
3. Verify other controls work correctly

---

## Files Reference

| File | Purpose |
|------|---------|
| `inc/customizer/styles/footer-builder-styles.php` | CSS output for footer builder rows |
| `inc/customizer/js/postmessage-parts/footer-builder-rows.ts` | Postmessage handlers for live preview |
| `inc/customizer/settings/footer-builder/desktop/top-row-section.php` | Desktop row 1 controls |
| `inc/customizer/settings/footer-builder/desktop/bottom-row-section.php` | Desktop row 3 controls |
| `inc/customizer/settings/footer-builder/mobile/top-row-section.php` | Mobile row 1 controls |
| `inc/customizer/settings/footer-builder/mobile/bottom-row-section.php` | Mobile row 3 controls |

---

## Notes

- Footer builder uses CSS class `.wpbf-footer-row-{row_key}` for row styling
- Mobile rows don't have `max_width` control (following header builder pattern)
- Row 2 (Main Row) uses existing footer controls with their own CSS output
