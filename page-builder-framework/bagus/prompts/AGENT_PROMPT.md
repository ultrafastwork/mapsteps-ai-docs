# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Continue Footer Builder development or address new tasks.

**Status**: Session v2.11.8+66 - Ready to start.

---

## Previous Session Summary (v2.11.8+65)

✅ Footer Separator Controls Refactor completed:
- Added "Top Separator" headline field to all 6 row sections
- Swapped Style/Width order (Style first, priority 220; Width second, priority 225)
- Updated activeCallbacks to use `border_top_style !== 'none'`
- Renamed labels: "Border Top X" → "Separator X"
- Field IDs and CSS output unchanged (backward compatible)

✅ "Sticky Footer" Field Reordering completed:
- Moved "Sticky Footer" after "Footer Builder" toggle and widget list
- Updated toggle priority to `1` and widget list to `10` in theme
- Updated sticky footer movement priority to `20` in premium plugin

---

## Pending Tasks (v2.11.8+67)

1. **Continue Footer Builder development or address next request.**

---

## Recent Completed

- ✅ "Sticky Footer" Field Reordering (v2.11.8+66)
- ✅ Footer Separator Controls Refactor (v2.11.8+65)
- ✅ Border-Top Controls for Footer Builder Rows (v2.11.8+63)
- ✅ Widget Title field for Menu/HTML widgets (v2.11.8+62)
- ✅ Widget Title layout fix (v2.11.8+62)
- ✅ Footer Builder vertical alignment & menu styling (v2.11.8+61)
