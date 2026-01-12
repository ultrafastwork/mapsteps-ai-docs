# Agent Prompt: WPBF Premium Development

## Objective

Test the `mobile_menu_overlay` fix and perform optional cleanup tasks.

---

## Prerequisites

**1. Read the project rules:**
```
ai-docs/wpbf-premium/rules.md
```

**2. Read the progress handoff document:**
```
ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md
```

---

## Context

The previous session (v2.10.3+9) fixed the `mobile_menu_overlay` control not rendering issue by adding `->tab('general')` to the `mobile_menu_overlay_separator` control.

**File modified:** `wp-content/plugins/wpbf-premium/inc/customizer/controls/settings-header.php`

---

## Instructions

### Testing
1. Open WordPress Customizer
2. Navigate to: Header → Mobile Navigation
3. Select "Off Canvas" menu type in General tab
4. Verify the "Off Canvas Settings" headline and "Menu Width" control appear in General tab
5. Switch to Design tab and verify "Overlay" toggle and "Background Color" controls appear

### Optional Cleanup
- Delete `package-backup.json` if no longer needed
- Migrate SCSS from `@import` to `@use` (Sass deprecation warning)

---

## Key Principles

- **Control dependencies require `wpbf-controls-bundle` script handle** (not `wpbf-base-control`)
- Controls in tabbed sections MUST have a `->tab()` assignment to render properly

---

## Available Build Commands

```bash
pnpm run wpbf                    # Interactive CLI menu
pnpm run build-asset --path=...  # Build any asset
pnpm run build-wp-plugin         # Build plugin distribution
```

---

## Notes

- Use `pnpm` for package management (not `npm`)
- Spurious JS files from CSS builds are cleaned up during `build-wp-plugin`
