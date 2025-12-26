# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Verify Typography settings refactoring against backup file.

**Status**: Session v2.11.8+23 - Verification task.

---

## Verification Task

Previous agent split `settings-typography.php` into modular components. Your task is to verify:

1. **No code loss**: All settings from backup exist in new modules
2. **No flow change**: Settings registration order preserved
3. **No logic change**: Setting implementations are identical

### Files to Verify

**Backup file** (original):

- `wp-content/plugins/wpbf-premium/inc/customizer/settings/settings-typography-backup.php`

**New files** (refactored):

- `wp-content/plugins/wpbf-premium/inc/customizer/settings/settings-typography.php`
- Files in `inc/customizer/settings/typography/` directory (if any)

### Verification Steps

1. **Read backup file** to get complete settings list
2. **List all files** in refactored structure
3. **Map each setting** to its new location in refactored files
4. **Compare implementations** line-by-line for any changes
5. **Verify loop structures** - ensure loop variables are in scope

### Expected Deliverable

A verification report with:

- ✅/❌ status for each setting
- Any discrepancies found
- Confirmation that refactoring is complete and correct

---

## Instructions

1. **Read** backup file to get complete settings list
2. **Compare** each setting against its new location
3. **Report** findings to user
4. **Delete** backup file if verification passes
