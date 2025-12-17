# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Test and commit the Sub Menu fix, then address deferred CSS issues.

**Status**: Sub Menu fix has been implemented but needs testing and commit.

## Task 1: Test and Commit Sub Menu Fix

### What Was Fixed

CSS in `Customizer/Controls/Builder/src/builder-control.scss` was updated to exclude Sub Menu sections from being hidden when Header Builder is enabled.

### What to Do

1. **Test in Customizer**:
   - Go to WordPress Customizer → Header panel
   - Enable Header Builder toggle
   - Verify **Sub Menu** and **Mobile Sub Menu** sections are visible
   - Test that controls work correctly

2. **Commit Changes**:
   - Files: `Customizer/Controls/Builder/src/builder-control.scss`, `Customizer/Controls/Bundle/dist/controls-bundle-min.css`
   - Message: "Fix: Show Sub Menu sections when Header Builder is enabled"

## Task 2: Visual CSS Issues (Deferred)

See `PROGRESS_HANDOFF_v2.11.8+30_PENDING.md` for details:
- Grey line above "Header Builder" section title
- Toggle position slightly off when toggled off

### Instructions

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for full details.
2. **Read Rules**: Check `ai-docs/page-builder-framework/rules.md` for project-specific guidelines.
3. **Test**: Verify the Sub Menu fix works correctly.
4. **Commit**: Commit the changes.
5. **Document**: Update `PROGRESS_HANDOFF.md` with results.
