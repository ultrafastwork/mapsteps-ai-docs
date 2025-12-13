# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Fix the Mobile Widget Positioning issue.

**Issue (from `ai-docs/page-builder-framework/ISSUES.md`)**:
> Mobile widget positioning breaks due to flex: auto applied on the selector: `.wpbf-header-column.wpbf-column-grow`.

**Context from v2.11.8+28**:
In the previous session, we fixed logo centering with mixed widget types by applying `wpbf-column-grow` to ALL columns with widgets (not just specific widget types). This may have affected mobile widget positioning.

**Instructions**:

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for current state and recent changes.

2. **Investigate & Fix**:
   - Analyze how the `wpbf-column-grow` class affects mobile header columns
   - Check if mobile rows need different flex behavior than desktop rows
   - Consider if mobile columns should have `flex: 0 0 auto` instead of `flex: 1 1 auto`

   **Files to Check**:
   - `Customizer/HeaderBuilder/HeaderBuilderOutput.php` - Mobile column class logic (lines 400-404)
   - `assets/scss/main/_navigation.scss` - Header column CSS (lines 583-611)

3. **Verify**: Test in Customizer with various mobile widget configurations.

4. **Document**: Update `PROGRESS_HANDOFF.md` and mark issue fixed in `ISSUES.md`.
