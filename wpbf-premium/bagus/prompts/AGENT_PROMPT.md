# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Implement Footer Builder output rendering and styles output for premium controls.

**Status**: Session v2.11.8+26 - Footer Builder output & styles integration.

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

## Task 1: Footer Builder Custom Content Output

Hook into theme's filter to render custom content (page builder templates) when set.

### Dependency

**Requires theme work first**: The theme (page-builder-framework) needs to add a filter hook `wpbf_footer_builder_row_content` in `FooterBuilderOutput.php`. This is being handled by another AI agent working on the theme.

Once the theme filter is available, implement the plugin hook.

### Implementation

Hook into the theme's filter to check for custom content and return it:

```php
add_filter( 'wpbf_footer_builder_row_content', function( $content, $row_key ) {
    $custom_content = get_theme_mod( "wpbf_footer_builder_{$row_key}_custom", '' );
    
    if ( ! empty( $custom_content ) ) {
        return $custom_content; // Theme will do_shortcode() this
    }
    
    return $content;
}, 10, 2 );
```

### Key Files

| File | Location | Purpose |
|------|----------|---------|
| `FooterBuilderOutput.php` | Theme: `Customizer/FooterBuilder/` | Will have `wpbf_footer_builder_row_content` filter |
| `settings-footer-builder.php` | Plugin: `inc/customizer/settings/` | Premium "Custom Content" controls |

### Implementation Steps

1. **Wait for theme filter**: Verify `wpbf_footer_builder_row_content` filter exists in theme
2. **Create output hook**: Add filter callback in plugin to return custom content
3. **Test**: Add Elementor/Beaver Builder template shortcode, verify it replaces row content

---

## Task 2: Footer Builder Styles Output

Analyze if CSS styles output is needed for footer builder premium controls.

### Current Premium Controls

The current premium footer builder controls are **"Custom Content" code fields**:
- These render shortcodes (Elementor/Beaver Builder templates)
- Page builder templates have their own styles
- **Likely NO CSS styles needed** for these controls

### When Styles Would Be Needed

Styles output would be needed if premium plugin adds controls like:
- Custom colors, fonts, spacing for footer builder rows
- Widget-specific styling options

### Reference Files

| File | Purpose |
|------|---------|
| `inc/customizer/styles.php` | Main styles entry - uses `$header_builder_enabled` check |
| `inc/customizer/styles/footer-styles.php` | Existing footer WIDGETS styles (not footer builder) |

### Action Items

1. **Verify if styles are needed**: Current "Custom Content" controls likely don't need CSS
2. **If no styles needed**: Document this and skip creating styles file
3. **If future controls need styles**: Create `footer-builder-styles.php` following existing patterns

---

## Premium Footer Builder Controls

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
| `inc/customizer/styles.php` | Main styles entry - study header builder pattern |
| `inc/customizer/styles/footer-styles.php` | Existing footer WIDGETS styles |
| Theme's `inc/output/FooterBuilderOutput.php` | Footer builder output rendering |

---

## Alternative Tasks

If output/styles integration is complex or requires theme changes, consider:

1. **Controls Movement**: Move existing footer premium controls (sticky footer, theme author, etc.) to footer builder sections when enabled
2. **Additional Premium Controls**: Add more premium controls to footer builder widget sections (logo, menu, html, social, copyright)
