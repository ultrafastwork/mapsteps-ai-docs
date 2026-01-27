# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Implement a Bidirectional Synchronization Assistant for the Mobile Menu and Menu Trigger in the Header Builder.

**Status**: Session v2.11.8+82 - Ready to implement Smart Feedback and Highlighting.

---

## Instructions

1. **Implement Sidebar Warnings**: Add dynamic `custom` field notices in `inc/customizer/settings/header-builder/mobile/menu-trigger-section.php` and `inc/customizer/settings/header-builder/mobile/offcanvas-section.php`.
2. **Setup Auto-Focus Logic**: Add JS logic in `inc/customizer/js/customizer.ts` (or a new part) to handle focusing sections and highlighting drop-zones/widgets.
3. **Preview Communication**: Modify `assets/js/setup/mobile-menu.js` to detect if the menu is empty when clicked and communicate this to the Customizer sidebar.
4. **Validation Logic**: Implement the cross-validation logic that checks `wpbf_header_builder_layout` for both the Trigger widget and the Menu widgets.

---

## Recent Accomplishments (v2.11.8+81)

- ✅ **Issue Analysis**: Deeply analyzed the mobile menu/trigger disconnect in the Header Builder (Ghost Trigger & Missing Trigger).
- ✅ **Solution Design**: Proposed a Bidirectional Synchronization Assistant with Smart Feedback and Highlighting.

---

## Recent Completed

- ✅ Desktop Menu Trigger Conditional Display (v2.11.8+80)
- ✅ Row 2 Menu Style Decoupling Implementation (v2.11.8+79)
- ✅ Row 2 Menu Style Decoupling Analysis (v2.11.8+78)
- ✅ Custom Select2 DataAdapter Implementation (v2.11.8+77)
- ✅ Typography Controls Memory Analysis (v2.11.8+76)
