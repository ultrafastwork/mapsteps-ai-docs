# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Add filter hook in FooterBuilderOutput for premium plugin integration.

**Status**: Session v2.11.8+49 - Footer Builder row content filter.

---

## Background

The **Footer Builder** feature is now complete with:
- Widget and slot definitions (`FooterBuilderConfig.php`)
- Frontend rendering (`FooterBuilderOutput.php`)
- Controls movement (v2.11.8+46)
- Postmessage support for live preview (v2.11.8+47)
- CSS output for row controls (v2.11.8+48)

**Premium plugin integration needed**: The wpbf-premium plugin has "Custom Content" controls that allow users to replace entire row content with page builder templates (Elementor/Beaver Builder shortcodes). The theme needs to provide a filter hook so the premium plugin can override row content.

---

## Task: Add Filter Hook in FooterBuilderOutput

Add a filter in `FooterBuilderOutput.php` to allow premium plugin to override row content rendering.

### Implementation

In `render_row()` method, add a filter before rendering the row content:

```php
private function render_row( $row_key, $columns ) {
    // Allow premium plugin to override entire row content
    $custom_content = apply_filters( 'wpbf_footer_builder_row_content', '', $row_key );
    
    if ( ! empty( $custom_content ) ) {
        // Render row wrapper with custom content
        $row_class = 'wpbf-footer-row wpbf-footer-row-' . esc_attr( $row_key );
        echo '<div class="' . esc_attr( $row_class ) . '">';
        echo '<div class="wpbf-container wpbf-container-center">';
        echo do_shortcode( $custom_content );
        echo '</div>';
        echo '</div>';
        return;
    }
    
    // ... existing row rendering code ...
}
```

### Reference: Header Builder Pattern

Check if `HeaderBuilderOutput.php` has similar filter for consistency. If so, follow the same pattern.

### Files to Modify

| File | Changes |
|------|---------|
| `Customizer/FooterBuilder/FooterBuilderOutput.php` | Add `wpbf_footer_builder_row_content` filter in `render_row()` |

---

## Testing

After adding the filter:

1. Verify footer builder still renders correctly (filter returns empty by default)
2. Test that the filter can be hooked into:
   ```php
   add_filter( 'wpbf_footer_builder_row_content', function( $content, $row_key ) {
       if ( 'desktop_row_1' === $row_key ) {
           return '<p>Test custom content</p>';
       }
       return $content;
   }, 10, 2 );
   ```

---

## Notes

- The premium plugin (wpbf-premium) will hook into this filter to render custom content
- Premium plugin controls: `wpbf_footer_builder_{row_key}_custom` (code fields for shortcodes)
- Use `do_shortcode()` to process page builder template shortcodes
