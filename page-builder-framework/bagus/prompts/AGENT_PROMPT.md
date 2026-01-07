# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Add CSS output for Footer Builder row controls.

**Status**: Session v2.11.8+48 - Footer Builder CSS output.

---

## Background

The **Footer Builder** feature now has:
- Widget and slot definitions (`FooterBuilderConfig.php`)
- Frontend rendering (`FooterBuilderOutput.php`)
- Controls movement (v2.11.8+46)
- Postmessage support for live preview (v2.11.8+47)

In session v2.11.8+47, new controls were added to footer builder rows 1 and 3:
- Desktop: `max_width`, `vertical_padding`, `bg_color`, `text_color`, `accent_colors`, `font_size`
- Mobile: `vertical_padding`, `bg_color`, `text_color`, `accent_colors`, `font_size`

These controls have postmessage handlers for live preview, but they need **CSS output** to persist the styles on page load.

---

## Task: Add CSS Output for Footer Builder Row Controls

### Reference: Header Builder CSS Output

Study how header builder generates CSS for row controls. Look for:
- `Customizer/HeaderBuilder/` - Header builder classes
- CSS generation patterns for row styling

### Implementation Steps

1. **Analyze header builder CSS output pattern**
   - Find where header builder row CSS is generated
   - Understand the CSS output structure

2. **Create CSS output for footer builder rows**
   - Add CSS generation for new row controls (rows 1 and 3)
   - Use selectors matching the postmessage handlers:
     - `.wpbf-footer-row-desktop_row_1`, `.wpbf-footer-row-desktop_row_3`
     - `.wpbf-footer-row-mobile_row_1`, `.wpbf-footer-row-mobile_row_3`

3. **Test in Customizer**
   - Verify styles persist after page refresh
   - Verify live preview still works

### New Controls Needing CSS Output

| Control ID | CSS Property | Selector |
|------------|--------------|----------|
| `wpbf_footer_builder_desktop_row_1_max_width` | `max-width` | `.wpbf-footer-row-desktop_row_1 .wpbf-container` |
| `wpbf_footer_builder_desktop_row_1_vertical_padding` | `padding-top/bottom` | `.wpbf-footer-row-desktop_row_1 .wpbf-row-content` |
| `wpbf_footer_builder_desktop_row_1_bg_color` | `background-color` | `.wpbf-footer-row-desktop_row_1` |
| `wpbf_footer_builder_desktop_row_1_text_color` | `color` | `.wpbf-footer-row-desktop_row_1` |
| `wpbf_footer_builder_desktop_row_1_accent_colors` | `color` (links) | `.wpbf-footer-row-desktop_row_1 a` |
| `wpbf_footer_builder_desktop_row_1_font_size` | `font-size` | `.wpbf-footer-row-desktop_row_1` |

(Same pattern for `desktop_row_3`, `mobile_row_1`, `mobile_row_3`)

---

## Files Reference

### CSS Output Files (Key Files)

| File | Purpose |
|------|---------|
| `inc/customizer/styles.php` | Main entry point - includes all style files |
| `inc/customizer/styles/footer-builder-styles.php` | **TARGET FILE** - Currently empty, add CSS output here |
| `inc/customizer/styles/header-builder-rows-styles.php` | **PATTERN TO FOLLOW** - Header builder rows CSS output |

### Other Reference Files

| File | Purpose |
|------|---------|
| `Customizer/FooterBuilder/FooterBuilderOutput.php` | Footer builder frontend rendering |
| `inc/customizer/js/postmessage-parts/footer-builder-rows.ts` | Postmessage handlers (CSS selectors reference) |
| `inc/customizer/settings/footer-builder/desktop/top-row-section.php` | Row 1 controls |
| `inc/customizer/settings/footer-builder/desktop/bottom-row-section.php` | Row 3 controls |

---

## Notes

- **`footer-builder-styles.php` exists but is empty** - this is where CSS output should be added
- Follow the pattern in `header-builder-rows-styles.php` for CSS generation
- CSS output should match the selectors used in `footer-builder-rows.ts`
- Row 2 (Main Row) uses moved controls that already have CSS output in existing footer CSS
- Mobile rows don't have `max_width` control
