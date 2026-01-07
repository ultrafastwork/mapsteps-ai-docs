# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Create Footer Builder feature based on the existing Header Builder implementation.

**Status**: Session v2.11.8+45 - Footer Builder development.

---

## Background

The theme has a **Header Builder** feature that allows users to build custom headers via drag-and-drop in the WordPress Customizer. The footer builder should follow the same pattern.

### Header Builder Toggle Behavior

- **Toggle OFF**: Shows old non-header-builder "Header" settings
- **Toggle ON**: Shows new header builder drag-and-drop interface

The footer builder should work the same way:

- **Toggle OFF**: Shows existing footer settings (`settings-footer.php`)
- **Toggle ON**: Shows new footer builder drag-and-drop interface

---

## Reference Files (Header Builder)

Study these files to understand the implementation pattern:

### PHP Classes

- `Customizer/HeaderBuilder/HeaderBuilderConfig.php` - Defines available widgets and slots
- `Customizer/HeaderBuilder/HeaderBuilderOutput.php` - Renders header builder output on frontend

### Builder Controls (Reusable)

- `Customizer/Controls/Builder/BuilderControl.php`
- `Customizer/Controls/Builder/ResponsiveBuilderControl.php`
- `Customizer/Controls/Builder/BuilderStore.php`
- `Customizer/Controls/Builder/src/builder-control.ts`
- `Customizer/Controls/Builder/src/responsive-builder-control.ts`

### Customizer Settings

- `inc/customizer/settings/settings-header-builder.php` - Main settings file
- `inc/customizer/settings/header-builder/desktop/` - Desktop widget sections
- `inc/customizer/settings/header-builder/mobile/` - Mobile widget sections

### TypeScript (Customizer Behavior)

- `inc/customizer/js/customizer.ts` - Main customizer entry
- `inc/customizer/js/customizer-parts/setup-builder-control.ts` - Toggle behavior logic
- `inc/customizer/js/customizer-parts/setup-conditional-controls.ts` - Conditional visibility

---

## Task: Create Footer Builder

### 1. Create FooterBuilder PHP Classes

Create new directory: `Customizer/FooterBuilder/`

- **FooterBuilderConfig.php** - Define footer widgets (e.g., Logo, Menu, Social Icons, HTML, Copyright) and slots (rows/columns)
- **FooterBuilderOutput.php** - Render footer builder output on frontend

### 2. Create Customizer Settings

Create new file: `inc/customizer/settings/settings-footer-builder.php`

- Add `wpbf_footer_builder_main_section` (expanded section in `footer_panel`)
- Add `wpbf_enable_footer_builder` toggle (headline-toggle type)
- Add `wpbf_footer_builder` control (responsive-builder type)

Create new directory: `inc/customizer/settings/footer-builder/`

- Desktop row sections (top, main, bottom)
- Mobile row sections
- Widget sections (menu, html, social, copyright, etc.)

### 3. Update TypeScript

The existing `setup-builder-control.ts` should automatically handle the footer builder toggle if you use the same pattern:

```php
->properties([
    'wrapper_attrs' => [
        'class'                  => 'wpbf-builder-toggle',
        'data-connected-builder' => 'wpbf_footer_builder',
    ],
])
```

### 4. Update Conditional Controls

Update `setup-conditional-controls.ts` to handle footer builder enable/disable visibility.

### 5. Frontend Output

- Hook into footer template parts
- Conditionally render footer builder output when enabled

---

## Footer Builder Widgets (Suggested)

| Widget Key | Label | Description |
|------------|-------|-------------|
| `footer_logo` | Logo | Site logo |
| `footer_menu_1` | Menu 1 | Footer menu |
| `footer_menu_2` | Menu 2 | Secondary footer menu |
| `footer_html_1` | HTML 1 | Custom HTML |
| `footer_html_2` | HTML 2 | Custom HTML |
| `footer_social` | Social Icons | Social media links |
| `footer_copyright` | Copyright | Copyright text |

---

## Footer Builder Slots (Suggested)

- **Desktop**: 3 rows (Top, Main, Bottom) with 5 columns each
- **Mobile**: 3 rows with 5 columns each
- No offcanvas needed for footer

---

## Implementation Order

1. Create `FooterBuilderConfig.php` with widgets and slots
2. Create `settings-footer-builder.php` with toggle and builder control
3. Create widget section files in `footer-builder/desktop/` and `footer-builder/mobile/`
4. Create `FooterBuilderOutput.php` for frontend rendering
5. Update conditional controls for footer settings visibility
6. Test in customizer
7. Build assets if needed (`pnpm run build`)

---

## Notes

- Reuse the existing `ResponsiveBuilderControl` - no need to create new control types
- Follow the exact same pattern as header builder for consistency
- The `setup-builder-control.ts` is generic and should work for any builder with the `wpbf-builder-toggle` class
