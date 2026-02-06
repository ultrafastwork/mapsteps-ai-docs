# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Date**: 2026-02-06
**Last Completed Session**: v2.11.8+85
**Current Session**: v2.11.8+86
**Status**: Active

**Objective**: Fix Issue #2 in `ai-docs/page-builder-framework/header-builder-issues.md` - Poor visual spacing in `margin-padding` unit controls.

---

## Instructions

1. **Locate `margin-padding` control styles**:
   - Find the CSS/SCSS files responsible for rendering the `margin-padding` control in the Customizer.
   - Look for elements related to numeric inputs and unit selectors (px, %, em, etc.).

2. **Reduce horizontal spacing**:
   - Adjust margins/paddings to bring the unit selectors closer to the numeric inputs.
   - Ensure the layout remains responsive and looks good across different screen sizes.

3. **Improve alignment and consistency**:
   - Ensure all input fields and unit selectors are properly aligned.
   - Apply the changes globally to all `margin-padding` controls.

4. **Verify changes**:
   - Build the assets if necessary (e.g., `pnpm build-controls-bundle`).
   - (Optional/If possible) Check the Customizer UI to ensure the visual spacing is improved.

---

## Recent Completed

- ✅ Context Handoff Preparation for Issue #2 (v2.11.8+85)
- ✅ Auto-Open Widget Settings Section After Drag-Drop (v2.11.8+84)
- ✅ Menu Trigger Sync - Builder Area Highlighting (v2.11.8+83)
