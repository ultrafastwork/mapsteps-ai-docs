# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Add controls movement for Footer Builder and confirm off-canvas is not needed.

**Status**: Session v2.11.8+46 - Footer Builder controls movement.

---

## Background

The **Footer Builder** feature was implemented in session v2.11.8+45, following the Header Builder pattern. The implementation includes:

- `Customizer/FooterBuilder/FooterBuilderConfig.php` - Widget and slot definitions
- `Customizer/FooterBuilder/FooterBuilderOutput.php` - Frontend rendering
- `inc/customizer/settings/settings-footer-builder.php` - Main settings
- `inc/customizer/settings/footer-builder/desktop/*.php` - 10 desktop section files
- `inc/customizer/settings/footer-builder/mobile/*.php` - 10 mobile section files

---

## Task 1: Add Controls Movement for Footer Builder

The header builder moves some existing controls selectively from old sections into header builder sections when the toggle is enabled. This allows reusing existing styling controls within the builder context.

### Reference Implementation

Study `inc/customizer/js/customizer-parts/setup-controls-movement.ts` to understand the pattern:

```typescript
moveCustomizerControls({
    dependency: {
        settingId: "wpbf_enable_header_builder",
        moveForwardWhenValueIs: true,
    },
    sections: [
        {
            from: "wpbf_pre_header_options",
            to: "wpbf_header_builder_desktop_row_1_section",
            controlsToMove: [
                { id: "pre_header_width", label: { to: "Container Width" }, prio: { to: 10 } },
                // ...
            ],
        },
        // ...
    ],
});
```

### Controls to Move for Footer Builder

The existing footer settings (`inc/customizer/settings/settings-footer.php`) have these controls that should be moved to footer builder row sections:

| Control ID | Current Section | Target Section | New Label |
|------------|-----------------|----------------|-----------|
| `footer_width` | `wpbf_footer_options` | `wpbf_footer_builder_desktop_row_2_section` | Container Width |
| `footer_height` | `wpbf_footer_options` | `wpbf_footer_builder_desktop_row_2_section` | Vertical Padding |
| `footer_bg_color` | `wpbf_footer_options` | `wpbf_footer_builder_desktop_row_2_section` | (keep label) |
| `footer_font_color` | `wpbf_footer_options` | `wpbf_footer_builder_desktop_row_2_section` | (keep label) |
| `footer_accent_color` | `wpbf_footer_options` | `wpbf_footer_builder_desktop_row_2_section` | (keep label) |
| `footer_accent_color_alt` | `wpbf_footer_options` | `wpbf_footer_builder_desktop_row_2_section` | (keep label) |
| `footer_font_size` | `wpbf_footer_options` | `wpbf_footer_builder_desktop_row_2_section` | (keep label) |

### Implementation Steps

1. Update `inc/customizer/js/customizer-parts/setup-controls-movement.ts`:
   - Add footer builder controls movement configuration
   - Use `wpbf_enable_footer_builder` as the dependency setting

2. Rebuild customizer assets: `pnpm run build-customizer`

3. Test in customizer:
   - Toggle footer builder OFF → controls should be in `wpbf_footer_options`
   - Toggle footer builder ON → controls should move to footer builder row sections

---

## Task 2: Confirm Off-Canvas Not Needed

The footer builder was intentionally implemented **without off-canvas panels** (unlike header builder).

### Reasoning

- Header builder needs off-canvas for: full-screen menu, slide-out mobile menu
- Footer builder doesn't have these interaction patterns - footers are static content areas

### Verification

Confirm that `FooterBuilderConfig::availableSlots()` does NOT include `offcanvas` key:

```php
// Correct - no offcanvas
'desktop' => array(
    'rows' => array( /* 3 rows */ ),
),

// Header builder has offcanvas - footer should NOT
'desktop' => array(
    'offcanvas' => array( /* ... */ ), // NOT needed for footer
    'rows' => array( /* 3 rows */ ),
),
```

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
- **No offcanvas needed for footer** (unlike header) - this is intentional
