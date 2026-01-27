# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Test and refine the Bidirectional Synchronization Assistant for Mobile Menu and Menu Trigger.

**Status**: Session v2.11.8+83 - Testing the implementation from v2.11.8+82.

---

## Instructions

1. **Test Ghost Trigger Warning**: Enable Header Builder, add Menu Trigger to a mobile row without menu widgets in Mobile Menu area. Verify warning appears and "Setup Mobile Menu" button works.

2. **Test Missing Trigger Warning**: Add Menu 1/2 to Mobile Menu area without Menu Trigger in rows. Verify warning appears and "Add Menu Trigger" button works.

3. **Test Preview Communication**: Create Ghost Trigger scenario, click trigger in preview, verify Customizer receives notification.

4. **Refine if Needed**: Adjust styling, timing, or logic based on test results.

---

## Recent Accomplishments (v2.11.8+82)

- ✅ Created `setup-menu-trigger-sync.ts` module for validation logic
- ✅ Integrated sync module in `customizer.ts`
- ✅ Added CSS styles for warnings and highlighting
- ✅ Added empty menu detection in `mobile-menu.js`
- ✅ Added PHP localization for warning messages

---

## Recent Completed

- ✅ Bidirectional Synchronization Assistant (v2.11.8+82)
- ✅ Desktop Menu Trigger Conditional Display (v2.11.8+80)
- ✅ Row 2 Menu Style Decoupling Implementation (v2.11.8+79)
- ✅ Row 2 Menu Style Decoupling Analysis (v2.11.8+78)
- ✅ Custom Select2 DataAdapter Implementation (v2.11.8+77)
