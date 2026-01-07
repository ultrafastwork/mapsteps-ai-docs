# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Add Footer Builder integration to wpbf-premium plugin.

**Status**: Session v2.11.8+24 - Footer Builder integration.

---

## Background

The **Footer Builder** feature was implemented in the `page-builder-framework` theme (see `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md` for details):

- Session v2.11.8+45: Created Footer Builder core files
- Session v2.11.8+46: Added controls movement for footer builder

The theme's Footer Builder includes:
- `Customizer/FooterBuilder/FooterBuilderConfig.php` - Widget and slot definitions
- `Customizer/FooterBuilder/FooterBuilderOutput.php` - Frontend rendering
- `inc/customizer/settings/settings-footer-builder.php` - Main settings
- `inc/customizer/settings/footer-builder/desktop/*.php` - Desktop sections
- `inc/customizer/settings/footer-builder/mobile/*.php` - Mobile sections

---

## Task: Footer Builder Integration in wpbf-premium

The `wpbf-premium` plugin has header builder integration that adds premium fields/controls to the theme's header builder sections. Similarly, footer builder integration needs to be added.

### Reference: Header Builder Integration Pattern

Study `inc/customizer/settings/settings-header-builder.php` to understand the pattern:

```php
// Example: Adding fields to header builder sections
$desktop_top_row_section_id = 'wpbf_header_builder_desktop_row_1_section';
$desktop_top_row_control_id_prefix = 'wpbf_header_builder_desktop_row_1_';

wpbf_customizer_field()
    ->id( $desktop_top_row_control_id_prefix . 'sticky_separator' )
    ->type( 'divider' )
    ->tab( 'general' )
    ->priority( 20 )
    ->addToSection( $desktop_top_row_section_id );
```

### Existing Footer Settings in wpbf-premium

The plugin already has footer settings in `inc/customizer/settings/settings-footer.php`:

| Control ID | Section | Description |
|------------|---------|-------------|
| `footer_widgets` | `wpbf_widget_footer_options` | Widget footer columns (0-5) |
| `footer_widgets_width` | `wpbf_widget_footer_options` | Footer width |
| `footer_widgets_bg_color` | `wpbf_widget_footer_options` | Background color |
| `footer_widgets_headline_color` | `wpbf_widget_footer_options` | Headline color |
| `footer_widgets_font_color` | `wpbf_widget_footer_options` | Font color |
| `footer_widgets_accent_color` | `wpbf_widget_footer_options` | Accent color |
| `footer_widgets_accent_color_alt` | `wpbf_widget_footer_options` | Accent hover color |
| `footer_widgets_font_size` | `wpbf_widget_footer_options` | Font size |
| `footer_sticky` | `wpbf_footer_options` | Sticky footer toggle |
| `footer_theme_author_name` | `wpbf_footer_options` | Theme author name |
| `footer_theme_author_url` | `wpbf_footer_options` | Theme author URL |
| `footer_custom` | `wpbf_footer_options` | Custom footer (shortcode) |

### Implementation Steps

1. **Explore theme's footer builder sections** to understand available section IDs:
   - `wpbf_footer_builder_desktop_row_1_section` (Top Row)
   - `wpbf_footer_builder_desktop_row_2_section` (Main Row)
   - `wpbf_footer_builder_desktop_row_3_section` (Bottom Row)
   - Mobile equivalents

2. **Create `settings-footer-builder.php`** in `inc/customizer/settings/`:
   - Add premium controls to footer builder row sections
   - Consider which existing footer controls should be integrated

3. **Update `customizer-settings.php`** to require the new file (if needed)

4. **Consider controls movement** if any premium footer controls should move to footer builder sections when enabled

---

## Footer Builder Files Reference (Theme)

| Component | Location (in page-builder-framework) |
|-----------|--------------------------------------|
| Config Class | `Customizer/FooterBuilder/FooterBuilderConfig.php` |
| Output Class | `Customizer/FooterBuilder/FooterBuilderOutput.php` |
| Settings | `inc/customizer/settings/settings-footer-builder.php` |
| Desktop Sections | `inc/customizer/settings/footer-builder/desktop/` |
| Mobile Sections | `inc/customizer/settings/footer-builder/mobile/` |
| Toggle Control | `wpbf_enable_footer_builder` |
| Builder Control | `wpbf_footer_builder` |

---

## Notes

- Footer builder does **NOT** have off-canvas (unlike header builder) - footers are static content areas
- Follow the same pattern as `settings-header-builder.php` for consistency
- Use `wpbf_footer_builder_enabled()` function to check if footer builder is active
