# Agent Prompt: Fix menu_overlay PostMessage in Header Builder Mode

## Objective

Debug and fix the instant preview (postMessage) for `menu_overlay` and `menu_overlay_color` settings when Header Builder is enabled. These settings work correctly in non-header builder (legacy) mode but fail in Header Builder mode.

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

The `menu_overlay` (toggle) and `menu_overlay_color` (color picker) settings control the overlay that appears behind the desktop off-canvas menu. In Header Builder mode, changing these values in the Customizer does NOT update the preview instantly - a page refresh is required.

**Expected behavior:** Changes should reflect immediately in the preview (like in non-header builder mode).

---

## Investigation Steps

### 1. Understand the Current Implementation

**Legacy (non-header builder) handlers location:**
```
wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage-parts/navigation.ts
```
- Lines 285-302: `menu_overlay` handler (skips if header builder enabled)
- Lines 305-317: `menu_overlay_color` handler (skips if header builder enabled)

**Theme postmessage files to check:**
```
wp-content/themes/page-builder-framework/inc/customizer/js/postmessage-parts/
```

### 2. Compare with Working Implementation

Look at how the non-header builder version handles these settings:
- What selectors are used?
- What DOM manipulation is done?

### 3. Find or Create Header Builder Handlers

Options:
1. Check if handlers exist in theme postmessage files but aren't working
2. If missing, add new handlers for Header Builder mode
3. Ensure the overlay element (`.wpbf-menu-overlay`) exists in the DOM when Header Builder is enabled

### 4. Test the Fix

1. Enable Header Builder
2. Add Desktop Off-Canvas panel with a menu
3. Go to Desktop Off-Canvas settings
4. Toggle "Overlay" on/off - should update instantly
5. Change "Overlay Background Color" - should update instantly

---

## Key Files

| File | Purpose |
|------|---------|
| `wpbf-premium/inc/customizer/js/postmessage-parts/navigation.ts` | Legacy handlers (reference) |
| `page-builder-framework/inc/customizer/js/postmessage-parts/*.ts` | Theme postmessage files |
| `wpbf-premium/inc/customizer/js/customizer.ts` | Control movement config |

---

## Build Command

After making changes:
```bash
pnpm run build-postmessage
```
(Run from `wp-content/plugins/wpbf-premium/`)

---

## Success Criteria

- [ ] `menu_overlay` toggle updates preview instantly in Header Builder mode
- [ ] `menu_overlay_color` updates preview instantly in Header Builder mode
- [ ] No JavaScript errors in console
- [ ] Non-header builder mode still works correctly
