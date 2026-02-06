# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Date**: 2026-02-06
**Last Completed Session**: v2.11.8+86
**Current Session**: v2.11.8+87
**Status**: Active

**Objective**: Visual QA of margin-padding spacing fix, then address remaining header builder issues.

---

## Instructions

1. **Visual QA of margin-padding spacing fix**:
   - Open the Customizer and verify that all `margin-padding` controls (Header Builder margins, responsive padding controls, etc.) display correctly.
   - Confirm the unit selector (px, %, em) sits close to the numeric inputs without excessive spacing.
   - If any visual regressions are found, fix them in `Customizer/Controls/MarginPadding/src/margin-padding-control.scss`.

2. **Address Issue #1** (if time permits):
   - Inconsistent spacing between header widgets in the same column/slot.
   - Add Margin controls to HTML and Menu widgets that currently lack them.
   - See `ai-docs/page-builder-framework/header-builder-issues.md` for full details.

3. **Address Issue #3** (if time permits):
   - Search widget UX improvements — smooth expansion, icon collision, hover transitions.
   - See `ai-docs/page-builder-framework/header-builder-issues.md` for full details.

---

## Recent Completed

- ✅ Improved visual spacing in `margin-padding` unit controls (v2.11.8+86)
- ✅ Context Handoff Preparation for Issue #2 (v2.11.8+85)
- ✅ Auto-Open Widget Settings Section After Drag-Drop (v2.11.8+84)
