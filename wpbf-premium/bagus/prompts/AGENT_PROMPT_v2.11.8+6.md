# Agent Prompt: Verify CLI Tooling Migration for WPBF Premium

## Objective

Verify the CLI tooling migration from Parcel to Vite. Compare the new `package.json` against the original backup and the theme's reference implementation. Test all build scripts and clean up test outputs.

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

**3. Study these reference files:**
```
wp-content/plugins/wpbf-premium/package-backup.json          # Original Parcel-based version
wp-content/plugins/wpbf-premium/package.json                 # New Vite-based version
wp-content/themes/page-builder-framework/package.json        # Theme reference
```

---

## Tasks

### Task 1: Verify package.json Changes
Compare the new `package.json` against:
1. **`package-backup.json`** - Ensure all original scripts are preserved (with Vite equivalents)
2. **Theme's `package.json`** - Ensure structure follows the same patterns

**Verification checklist:**
- [ ] All original build scripts have Vite equivalents
- [ ] Dependencies are correct (Parcel removed, Vite added)
- [ ] Alias configuration preserved
- [ ] Browserslist preserved

### Task 2: Test All Build Scripts
Run each build script and verify it completes successfully. Use `--` to pass through without manual confirmation where possible.

**Test commands (run these with `pnpm run`):**
```bash
# Interactive CLI menu (requires manual interaction - test separately)
pnpm run wpbf

# Generic build-asset command
pnpm run build-asset --path=assets/ts/site.ts

# Core scripts
pnpm run build-postmessage
pnpm run build-customizer
pnpm run build-theme-settings

# Site assets
pnpm run build-site-js
pnpm run build-site-jquery
pnpm run build-site-css
pnpm run build-wpbf-utils

# Infinite scroll
pnpm run build-infinite-scroll-js
pnpm run build-infinite-scroll-jquery

# WooCommerce
pnpm run build-woocommerce-jquery
pnpm run build-woo-infinite-scroll-jquery
pnpm run build-woocommerce-quick-view-jquery

# EDD
pnpm run build-edd-js
pnpm run build-edd-jquery

# Plugin distribution
pnpm run build-wp-plugin
```

**Note:** The `wpbf` command is an interactive CLI menu using `@clack/prompts`. It provides:
- Build Preset Asset (select from common assets)
- Build Custom Asset (enter file path manually)
- Build WP Plugin (production package)

### Task 3: Verify Build Outputs
Check that built files are created in correct locations:
- JS files → `js/` directory with `-min.js` suffix
- CSS files → `css/` directory with `-min.css` suffix
- Plugin build → `build/wpbf-premium/` directory

### Task 4: Clean Up Test Outputs
After testing, delete any generated files:
```bash
# Delete plugin build output
Remove-Item -Recurse -Force build

# Note: JS/CSS outputs overwrite existing files, no cleanup needed
```

### Task 5: Report Findings
Document any issues found:
- Scripts that fail
- Missing functionality compared to original
- Deviations from theme's patterns

---

## Notes

- Use `pnpm` for package management (not `npm`)
- Commands can be run with `Blocking: true` and `SafeToAutoRun: true` for automated testing
- SCSS builds generate a small JS file alongside CSS (Vite behavior - this is expected)
- Some original scripts referenced non-existent files - these were intentionally removed
