# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Test Footer Builder controls movement and review frontend output.

**Status**: Session v2.11.8+47 - Footer Builder testing.

---

## Background

The **Footer Builder** feature was implemented in session v2.11.8+45, and controls movement was added in session v2.11.8+46. The implementation includes:

- `Customizer/FooterBuilder/FooterBuilderConfig.php` - Widget and slot definitions
- `Customizer/FooterBuilder/FooterBuilderOutput.php` - Frontend rendering
- `inc/customizer/settings/settings-footer-builder.php` - Main settings
- `inc/customizer/settings/footer-builder/desktop/*.php` - 10 desktop section files
- `inc/customizer/settings/footer-builder/mobile/*.php` - 10 mobile section files
- `inc/customizer/js/customizer-parts/setup-controls-movement.ts` - Controls movement (header + footer)

---

## Task 1: Test Footer Builder Controls Movement

The controls movement was added in v2.11.8+46. Verify it works correctly:

### Testing Steps

1. Open WordPress Customizer
2. Navigate to Footer panel
3. Toggle footer builder OFF → verify controls are in `wpbf_footer_options` section
4. Toggle footer builder ON → verify controls move to `wpbf_footer_builder_desktop_row_2_section`
5. Verify control labels change correctly:
   - `footer_width` → "Container Width"
   - `footer_height` → "Vertical Padding"

### Controls Moved

| Control ID | New Label | Priority |
|------------|-----------|----------|
| `footer_width` | Container Width | 10 |
| `footer_height` | Vertical Padding | 15 |
| `footer_bg_color` | (keep label) | 200 |
| `footer_font_color` | (keep label) | 205 |
| `footer_accent_color` | (keep label) | 210 |
| `footer_accent_color_alt` | (keep label) | 215 |
| `footer_font_size` | (keep label) | 220 |

---

## Task 2: Review Footer Builder Frontend Output

Test the footer builder rendering on the frontend:

### Testing Steps

1. Enable footer builder in Customizer
2. Add widgets to different slots (Logo, Menu, HTML, Social Icons, Copyright)
3. Preview the frontend
4. Verify:
   - Widgets display correctly in assigned slots
   - Row styling applies correctly
   - Responsive behavior works (desktop vs mobile)

---

## Footer Builder Files Reference

| Component | Location |
|-----------|----------|
| Config Class | `Customizer/FooterBuilder/FooterBuilderConfig.php` |
| Output Class | `Customizer/FooterBuilder/FooterBuilderOutput.php` |
| Settings | `inc/customizer/settings/settings-footer-builder.php` |
| Desktop Sections | `inc/customizer/settings/footer-builder/desktop/` |
| Mobile Sections | `inc/customizer/settings/footer-builder/mobile/` |
| Controls Movement | `inc/customizer/js/customizer-parts/setup-controls-movement.ts` |
| Toggle Control | `wpbf_enable_footer_builder` (headline-toggle type) |
| Builder Control | `wpbf_footer_builder` (responsive-builder type) |

---

## Notes

- Footer builder uses same `ResponsiveBuilderControl` as header builder
- `setup-builder-control.ts` automatically handles footer builder toggle via `wpbf-builder-toggle` class
- Footer builder adds to existing `footer_panel` with priority 0 (appears first)
- **No offcanvas needed for footer** (unlike header) - footers are static content areas
