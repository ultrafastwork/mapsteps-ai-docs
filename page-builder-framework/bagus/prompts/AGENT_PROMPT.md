# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Review and implement next feature or enhancement for Footer Builder.

**Status**: Session v2.11.8+50 - Footer Builder complete, awaiting next task.

---

## Background

The **Footer Builder** feature is now complete with:
- Widget and slot definitions (`FooterBuilderConfig.php`)
- Frontend rendering (`FooterBuilderOutput.php`)
- Controls movement (v2.11.8+46)
- Postmessage support for live preview (v2.11.8+47)
- CSS output for row controls (v2.11.8+48)
- Row content filter for premium plugin integration (v2.11.8+49)

---

## Completed: Row Content Filter (v2.11.8+49)

The `wpbf_footer_builder_row_content` filter has been added to `FooterBuilderOutput.php`:

```php
$custom_content = apply_filters( 'wpbf_footer_builder_row_content', '', $row_key );
```

**Parameters**:
- `$custom_content` (string): Empty string by default
- `$row_key` (string): Row key (e.g., 'desktop_row_1', 'mobile_row_2')

The wpbf-premium plugin can now hook into this filter to render custom content (page builder shortcodes).

---

## Potential Next Tasks

1. **Footer Builder visibility controls** (optional)
   - Header builder has visibility controls for responsive display
   - Footer builder could have similar controls if needed

2. **Premium plugin integration work**
   - Implement the premium plugin side that hooks into `wpbf_footer_builder_row_content`
   - Add "Custom Content" controls in wpbf-premium for footer builder rows

3. **Other enhancements**
   - Await user direction for next feature or bug fix

---

## Notes

- Footer builder uses CSS class `.wpbf-footer-row-{row_key}` for row styling
- The `wpbf_footer_builder_row_content` filter uses `do_shortcode()` to process page builder templates
- Check `PROGRESS_HANDOFF.md` for full history of Footer Builder implementation
