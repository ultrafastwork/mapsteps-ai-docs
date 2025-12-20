# Agent Prompt: WPBF Premium Development

## Objective

Awaiting new instructions from the user.

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

The styles.php refactoring has been completed and verified:
- Original file (~1741 lines) split into 12 modular files
- All code verified against backup
- Backup file deleted

**Main file:**
```
wp-content/plugins/wpbf-premium/inc/customizer/styles.php
```

**Split files location:**
```
wp-content/plugins/wpbf-premium/inc/customizer/styles/
```

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
- CLI tooling uses Vite (migrated from Parcel in v2.11.8+5)
- Interactive `wpbf` CLI available for common build tasks
