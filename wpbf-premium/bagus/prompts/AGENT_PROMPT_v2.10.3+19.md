# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Verify Custom Sections refactoring against backup file.

**Status**: Session v2.10.3+19 - Verification task.

---

## Verification Task

Previous agent refactored `class-custom-sections.php` (2,377 lines) into modular components. Your task is to verify:

1. **No code loss**: All methods from backup exist in new modules
2. **No flow change**: Constructor hooks and initialization order preserved
3. **No logic change**: Method implementations are identical

### Files to Verify

**Backup file** (original):

- `wp-content/plugins/wpbf-premium/inc/class-custom-sections-backup.php`

**New files** (refactored):

- `inc/class-custom-sections.php` - Main class (~740 lines)
- `inc/custom-sections/trait-post-type-helpers.php` - Post type utilities
- `inc/custom-sections/class-display-rules-matcher.php` - Display rules matching
- `inc/custom-sections/class-display-rules-ui.php` - Admin UI
- `inc/custom-sections/class-frontend-renderer.php` - Frontend rendering

### Verification Steps

1. **List all methods** in backup file
2. **Map each method** to its new location in refactored files
3. **Compare method bodies** line-by-line for any changes
4. **Verify constructor** hooks are wired identically
5. **Check namespace changes**: `WPBF` → `Wpbf\Premium`, `WPBF\CustomSections` → `Wpbf\Premium\CustomSections`
6. **Verify backwards compatibility**: `class_alias` for `WPBF\Custom_Sections` exists

### Expected Deliverable

A verification report with:

- ✅/❌ status for each method
- Any discrepancies found
- Confirmation that refactoring is complete and correct

---

## Instructions

1. **Read** backup file to get complete method list
2. **Compare** each method against its new location
3. **Report** findings to user
