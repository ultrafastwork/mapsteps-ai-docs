# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Verify General settings refactoring against backup file.

**Status**: Session v2.11.8+40 - Verification task.

---

## Verification Task

Previous agent split `settings-general.php` into modular components. Your task is to verify:

1. **No code loss**: All settings from backup exist in new modules
2. **No flow change**: Settings registration order preserved
3. **No logic change**: Setting implementations are identical

### Files to Verify

**Backup file** (original):

- `wp-content/themes/page-builder-framework/inc/customizer/settings/settings-general-backup.php`

**New files** (refactored):

- `wp-content/themes/page-builder-framework/inc/customizer/settings/settings-general.php`
- Files in `inc/customizer/settings/general/` directory

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
