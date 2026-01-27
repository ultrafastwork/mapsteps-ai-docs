# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Implement auto-open widget settings section after drag-drop in Header Builder.

**Status**: Session v2.11.8+84

---

## Problem

After drag-and-dropping a widget (e.g., Menu 1, Menu 2) to the builder area, users often forget they need to click on the widget button to open its settings section and configure it (e.g., select a menu from the "Select Menu" dropdown).

## Task

Implement auto-open of the widget's settings section when a widget is dropped into the builder area.

---

## Implementation Approach

1. **Locate drop event handling** in `Customizer/Controls/Builder/src/responsive-builder-control.ts`
2. **After widget drop**, automatically expand the corresponding Customizer section
3. **Section ID pattern**: `wpbf_header_builder_{widget_key}_section`

## Considerations

- Should this apply to all widgets or only specific ones (like menu widgets)?
- Should there be a slight delay before opening to let the user see the widget was placed?
- What if the user is rapidly dragging multiple widgets? (debounce?)

---

## Recent Completed

- ✅ Menu Trigger Sync - Builder Area Highlighting (v2.11.8+83)
- ✅ Bidirectional Synchronization Assistant (v2.11.8+82)
- ✅ Desktop Menu Trigger Conditional Display (v2.11.8+80)
- ✅ Row 2 Menu Style Decoupling Implementation (v2.11.8+79)
