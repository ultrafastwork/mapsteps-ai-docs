# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Date**: 2026-02-06
**Last Completed Session**: v2.11.8+87
**Current Session**: v2.11.8+88
**Status**: Completed

**Objective**: Fix Issue #3 in `ai-docs/page-builder-framework/header-builder-issues.md` — Search widget UX and behavior in Header Builder.

---

## Instructions

1. **Investigate search widget expansion behavior**:
   - Locate the CSS/JS responsible for the search widget expansion in the Header Builder.
   - Look for the search icon click handler and the input expand/collapse animation.
   - Identify why the search icon visually shifts during expansion.

2. **Smooth the search expansion**:
   - Fix the jarring icon shift during input expansion.
   - Ensure the expansion animation is smooth and stable.

3. **Hide browser clear (X) button**:
   - When the search input is expanded, hide the browser-provided clear button using `::-webkit-search-cancel-button` and equivalent selectors.
   - This prevents visual collision between the clear button and the search icon.

4. **Match hover transitions with menu items**:
   - The search icon hover effect (from `multicolor` control) is abrupt and not CSS-animated.
   - Add a smooth color transition matching the menu items' transition duration and easing.

5. **Build and verify**:
   - Build the necessary assets.
   - Verify changes in the Customizer/frontend.

---

## Recent Completed

- ✅ Visual QA and refinement of margin-padding spacing fix (v2.11.8+87)
- ✅ Improved visual spacing in `margin-padding` unit controls (v2.11.8+86)
- ✅ Context Handoff Preparation for Issue #2 (v2.11.8+85)
