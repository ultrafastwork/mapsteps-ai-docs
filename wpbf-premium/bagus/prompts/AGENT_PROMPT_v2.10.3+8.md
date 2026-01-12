# Agent Prompt: WPBF Premium Development

## Objective

Continue development on WPBF Premium plugin.

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

## Current Status

- ✅ CLI tooling migration from Parcel to Vite complete
- ✅ Customizer control dependencies fix applied (v2.10.3+8)

---

## Key Principles

- **Output filenames MUST match original Parcel output** to avoid breaking enqueue functionality
- Theme patterns are for reference only, not to implement as-is in the plugin
- **Control dependencies require `wpbf-controls-bundle` script handle** (not `wpbf-base-control`)

---

## Available Build Commands

```bash
pnpm run wpbf                    # Interactive CLI menu
pnpm run build-asset --path=...  # Build any asset
pnpm run build-wp-plugin         # Build plugin distribution
```

---

## Optional Cleanup Tasks

- [ ] Delete `package-backup.json` (no longer needed)
- [ ] Migrate SCSS from `@import` to `@use` (Sass deprecation warning)

---

## Notes

- Use `pnpm` for package management (not `npm`)
- Spurious JS files from CSS builds are cleaned up during `build-wp-plugin`
