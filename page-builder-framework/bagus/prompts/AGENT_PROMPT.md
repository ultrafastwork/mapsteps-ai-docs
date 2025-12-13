# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Fix the Button Widget automatic centering issue.

**Issue (from `ai-docs/page-builder-framework/ISSUES.md`)**:
> The Button Widget is automatically centered across all desktop row layouts, even when it should follow row alignment.

**Problem Description**:
The Button Widget is always centered in desktop rows regardless of the row's alignment settings. It should follow the row's alignment configuration instead.

**Instructions**:

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for current state.

2. **Investigate & Fix**:
   - Find the Button Widget settings files in `inc/customizer/settings/header-builder/desktop/`
   - Check the Button Widget output/rendering in `HeaderBuilderOutput.php` or related files
   - Investigate CSS that may be forcing center alignment on button widgets
   - Identify why button widget ignores row alignment
   - Apply appropriate fix to make button follow row alignment

   **Files to Check**:
   - `Customizer/HeaderBuilder/HeaderBuilderOutput.php` - Button widget rendering logic
   - `assets/scss/main/_navigation.scss` - Navigation/header CSS that may affect button alignment

3. **Verify**: Test in Customizer that Button Widget respects row alignment settings (left, center, right).

4. **Document**: Update `PROGRESS_HANDOFF.md` and mark issue fixed in `ISSUES.md`.
