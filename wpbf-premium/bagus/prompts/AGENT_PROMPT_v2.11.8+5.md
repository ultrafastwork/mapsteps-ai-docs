# Agent Prompt: CLI Tooling Modernization for WPBF Premium

## Objective

Modernize the CLI tooling for `wpbf-premium` plugin to match the theme's (`page-builder-framework`) CLI structure. This includes migrating from Parcel to Vite, creating a unified `build-asset` command, and implementing an interactive `wpbf` CLI menu.

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

**3. Study the theme's CLI implementation:**
```
wp-content/themes/page-builder-framework/package.json
wp-content/themes/page-builder-framework/wpbf.mjs
wp-content/themes/page-builder-framework/build-scripts/build-asset.mjs
wp-content/themes/page-builder-framework/build-scripts/build-wp-theme.mjs
```

---

## Context

### Current State (wpbf-premium)
- Uses **Parcel** for building assets
- Has many individual build scripts in `package.json`:
  - `build-wpbf-utils`, `build-site-jquery`, `build-site-css`, `build-site-js`
  - `build-infinite-scroll-jquery`, `build-infinite-scroll-js`
  - `build-woocommerce-jquery`, `build-woocommerce-js`
  - `build-woo-infinite-scroll-jquery`, `build-woo-infinite-scroll-js`
  - `build-edd-jquery`, `build-edd-js`
  - `build-woocommerce-quick-view-jquery`, `build-woocommerce-quick-view-js`
  - `build-theme-settings`, `build-customizer`, `build-postmessage`
- No interactive CLI menu
- No cleaned-up plugin build command

### Target State (like page-builder-framework)
- Uses **Vite** for building assets
- Has a unified `build-asset` command that accepts `--path` and optional `--output` parameters
- Has preset shortcuts like `build-postmessage`, `build-customizer` that use `build-asset`
- Has an interactive `wpbf` CLI menu using `@clack/prompts`
- Has a `build-wp-plugin` command for creating cleaned-up distribution

---

## Tasks

### Phase 1: Migrate to Vite
1. Update `package.json` dependencies (remove Parcel, add Vite)
2. Create `build-scripts/build-asset.mjs` based on theme's implementation
3. Test building existing assets with Vite

### Phase 2: Create Unified Build Commands
1. Create `build-asset` command with `--path` and optional `--output` parameters
2. Update preset commands (`build-postmessage`, `build-customizer`, etc.) to use `build-asset`
3. Identify which assets are entry points vs partials (developer should know which to build)

### Phase 3: Interactive CLI Menu
1. Create `wpbf.mjs` interactive menu using `@clack/prompts`
2. Provide options:
   - Build specific preset (postmessage, customizer, site-js, etc.)
   - Build custom path (manual file path input with optional output path)
   - Build cleaned-up plugin
3. Make it user-friendly with clear descriptions

### Phase 4: Build Cleaned-Up Plugin
1. Create `build-scripts/build-wp-plugin.mjs` based on theme's `build-wp-theme.mjs`
2. Should create a distribution-ready plugin without dev files

---

## Key Files to Create/Modify

| File | Action |
|------|--------|
| `package.json` | Update dependencies and scripts |
| `build-scripts/build-asset.mjs` | Create (based on theme) |
| `build-scripts/build-wp-plugin.mjs` | Create (based on theme's build-wp-theme.mjs) |
| `wpbf.mjs` | Create interactive CLI menu |

---

## Reference Files (Theme)

| File | Purpose |
|------|---------|
| `page-builder-framework/package.json` | Reference for scripts structure |
| `page-builder-framework/wpbf.mjs` | Reference for interactive CLI |
| `page-builder-framework/build-scripts/build-asset.mjs` | Reference for Vite build script |
| `page-builder-framework/build-scripts/build-wp-theme.mjs` | Reference for cleaned-up build |

---

## Success Criteria

- [ ] Parcel replaced with Vite
- [ ] `build-asset` command works with `--path` parameter
- [ ] Preset commands (`build-postmessage`, etc.) work correctly
- [ ] Interactive `wpbf` CLI menu is functional
- [ ] `build-wp-plugin` creates cleaned-up distribution
- [ ] All existing assets build successfully with new tooling
- [ ] No breaking changes to existing functionality
