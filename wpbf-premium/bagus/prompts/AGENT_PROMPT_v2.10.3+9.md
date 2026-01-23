# Agent Prompt: WPBF Premium Development

## Objective

Fix the `mobile_menu_overlay` control not rendering in the Customizer Design tab.

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

## Issue Description

**Problem:** The `mobile_menu_overlay` control (registered in wpbf-premium) is not being rendered when:
- page-builder-framework theme and wpbf-premium plugin are active
- In Customizer, navigate to: Header → Mobile Navigation → Design tab

**Location:** `wp-content/plugins/wpbf-premium/inc/customizer/controls/settings-header.php` (lines 2186-2250)

**Root Cause Analysis:**
The `mobile_menu_overlay_separator` headline control (lines 2187-2199) is missing a `->tab()` call. When a section has tabs defined, controls without a tab assignment may not render properly.

**Controls affected:**
1. `mobile_menu_overlay_separator` (headline) - line 2187 - **MISSING `->tab()`**
2. `mobile_menu_width` - line 2202 - has `->tab( 'general' )`
3. `mobile_menu_overlay` - line 2221 - has `->tab( 'design' )`
4. `mobile_menu_overlay_color` - line 2238 - has `->tab( 'design' )`

**Reference:** The theme's `wpbf_mobile_menu_options` section defines tabs at:
`wp-content/themes/page-builder-framework/inc/customizer/settings/settings-header.php` (lines 75-82)

---

## Instructions

1. **Investigate** the rendering issue - verify the root cause by checking how tab assignments affect control visibility
2. **Fix** the `mobile_menu_overlay_separator` by adding appropriate `->tab()` call
3. **Verify** all related controls in the Mobile Navigation section have proper tab assignments
4. **Test** in Customizer that controls now appear correctly in their respective tabs

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
