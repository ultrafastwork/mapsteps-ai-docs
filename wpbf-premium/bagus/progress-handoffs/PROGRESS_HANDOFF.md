# Progress Handoff: CLI Tooling Modernization for WPBF Premium

**Current Session:** v2.11.8+5
**Date:** December 19, 2024
**Status:** Active

---

## Project Rules

See `ai-docs/wpbf-premium/rules.md` for project-specific guidelines and workflows.

---

## Summary

Modernize the CLI tooling for `wpbf-premium` plugin to match the theme's (`page-builder-framework`) CLI structure. Migrate from Parcel to Vite, create unified build commands, and implement an interactive CLI menu.

---

## Recent Accomplishments (v2.11.8+4)

### Fixed menu_overlay PostMessage
- ✅ Updated handler to dynamically create/remove overlay element via JavaScript
- ✅ Works for both Header Builder and legacy modes
- ✅ Shows overlay immediately if menu is already open

---

## Pending Tasks

### Phase 1: Migrate to Vite
- [ ] Update `package.json` dependencies (remove Parcel, add Vite)
- [ ] Create `build-scripts/build-asset.mjs` based on theme's implementation
- [ ] Test building existing assets with Vite

### Phase 2: Create Unified Build Commands
- [ ] Create `build-asset` command with `--path` and optional `--output` parameters
- [ ] Update preset commands to use `build-asset`
- [ ] Document which assets are entry points vs partials

### Phase 3: Interactive CLI Menu
- [ ] Create `wpbf.mjs` interactive menu using `@clack/prompts`
- [ ] Provide preset options and custom path input
- [ ] Make it user-friendly

### Phase 4: Build Cleaned-Up Plugin
- [ ] Create `build-scripts/build-wp-plugin.mjs`
- [ ] Should create distribution-ready plugin without dev files

---

## Current State Analysis

### wpbf-premium (Current)
- Uses **Parcel** for building
- Individual build scripts:
  - `build-wpbf-utils`, `build-site-jquery`, `build-site-css`, `build-site-js`
  - `build-infinite-scroll-jquery`, `build-infinite-scroll-js`
  - `build-woocommerce-jquery`, `build-woocommerce-js`
  - `build-woo-infinite-scroll-jquery`, `build-woo-infinite-scroll-js`
  - `build-edd-jquery`, `build-edd-js`
  - `build-woocommerce-quick-view-jquery`, `build-woocommerce-quick-view-js`
  - `build-theme-settings`, `build-customizer`, `build-postmessage`

### page-builder-framework (Target Reference)
- Uses **Vite** for building
- Unified `build-asset` command with `--path` parameter
- Interactive `wpbf` CLI menu using `@clack/prompts`
- `build-wp-theme` for cleaned-up distribution

---

## Reference Files

| File | Purpose |
|------|---------|
| `page-builder-framework/package.json` | Scripts structure |
| `page-builder-framework/wpbf.mjs` | Interactive CLI |
| `page-builder-framework/build-scripts/build-asset.mjs` | Vite build script |
| `page-builder-framework/build-scripts/build-wp-theme.mjs` | Cleaned-up build |

---

## Notes

- Use `pnpm` for package management (not `npm`)
- Maintain backward compatibility during migration
- Test each phase before moving to next
