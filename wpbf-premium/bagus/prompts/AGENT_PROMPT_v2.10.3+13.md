# Agent Prompt: WPBF Premium Development

## Objective

Verify the styles.php refactoring by comparing split files against the backup version.

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

Previous session (v2.10.3+12) refactored `wp-content/plugins/wpbf-premium/inc/customizer/styles.php` (~1741 lines) into 12 smaller modular files.

**Backup file (original version):**
```
wp-content/plugins/wpbf-premium/inc/customizer/styles-backup.php
```

**Main file (refactored):**
```
wp-content/plugins/wpbf-premium/inc/customizer/styles.php
```

**Split files location:**
```
wp-content/plugins/wpbf-premium/inc/customizer/styles/
```

### Split Files Created
| File | Hook Function | Content |
|------|---------------|---------|
| `global-colors-styles.php` | `wpbf_premium_before_customizer_css` | CSS variables, color palette |
| `typography-styles.php` | `wpbf_premium_before_customizer_css` | Page & menu typography |
| `headings-styles.php` | `wpbf_premium_before_customizer_css` | H1-H6 heading styles |
| `blog-styles.php` | `wpbf_premium_after_customizer_css` | Blog layout styles |
| `mobile-navigation-styles.php` | `wpbf_premium_after_customizer_css` | Mobile menu styles |
| `off-canvas-menu-styles.php` | `wpbf_premium_after_customizer_css` | Off-canvas & full-screen nav |
| `transparent-header-styles.php` | `wpbf_premium_after_customizer_css` | Transparent header styles |
| `sticky-navigation-styles.php` | `wpbf_premium_after_customizer_css` | Sticky navigation styles |
| `cta-button-styles.php` | `wpbf_premium_after_customizer_css` | CTA button styles |
| `menu-effects-styles.php` | `wpbf_premium_after_customizer_css` | Navigation hover effects |
| `footer-styles.php` | `wpbf_premium_after_customizer_css` | Footer styles |
| `social-styles.php` | `wpbf_premium_after_customizer_css` | Social icons styles |

---

## Instructions

### 1. Verification Against Backup

Compare the backup file against the split files to ensure all code is preserved:

**Backup structure:**
- Lines 16-577: `wpbf_premium_before_customizer_css()` function
- Lines 582-1741: `wpbf_premium_after_customizer_css()` function

**Verification steps:**
1. Read `styles-backup.php` section by section
2. Verify each code block exists in the corresponding split file
3. Check that variable definitions and conditions are preserved
4. Ensure no code was accidentally omitted or duplicated

### 2. Functional Testing (Optional)

If time permits, test in WordPress Customizer:
1. Enable various customizer options (colors, typography, etc.)
2. Verify CSS is generated correctly on the frontend
3. Check browser console for any PHP errors

### 3. Cleanup After Verification

Once verification is complete:
- Delete `styles-backup.php` if all code is confirmed present
- Report any discrepancies found

---

## Key Code Sections to Verify

### In `wpbf_premium_before_customizer_css` (backup lines 16-577):
- [ ] CSS variables (`:root` selectors)
- [ ] Custom fonts (`wpbf_premium_font_face_css`)
- [ ] Page typography (line-height, letter-spacing)
- [ ] Menu font settings
- [ ] H1-H6 heading styles (desktop, tablet, mobile)

### In `wpbf_premium_after_customizer_css` (backup lines 582-1741):
- [ ] Blog layouts
- [ ] Mobile navigation (hamburger, off-canvas)
- [ ] Stacked menu advanced
- [ ] Off-canvas & full-screen navigation
- [ ] Transparent header
- [ ] Sticky navigation
- [ ] CTA button styles
- [ ] Navigation hover effects (underlined, boxed, modern)
- [ ] Footer (sticky, widgets)
- [ ] Social icons

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
- Split files use `require` (not `require_once`) to match theme pattern
- Variables like `$breakpoint_desktop`, `$breakpoint_medium`, `$breakpoint_mobile`, `$header_builder_enabled` are defined in main `styles.php` and available to split files
