# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Fix reported visual CSS issues, then continue with heavy work items.

**Status**: Customizer asset optimization completed in v2.11.8+29. Visual CSS issues reported.

**Immediate Task - Visual CSS Issues**:
1. **Grey line above "Header Builder" section title** - Thin grey border appeared
2. **Toggle position slightly off when toggled off** - Alignment issue

These issues are NOT from the bundling changes (bundle imports original SCSS unchanged). May be pre-existing or from earlier commits. Investigate CSS in:
- `Customizer/Controls/Headline/src/headline-toggle-control.scss`
- `Customizer/Controls/Checkbox/src/` (toggle styles)

**Remaining Heavy Works (from `ai-docs/page-builder-framework/ISSUES.md`)**:
1. Move "Premium" and "Theme Settings" options into Desktop Menu section
2. Hide "Menu Items Spacing" control when menu type doesn't support spacing
3. Enabling "Main Row Sticky Header" should automatically hide Top Row sticky toggle
4. "Top Row Sticky Header" should function as single toggle, inheriting from main row
5. Sticky navigation is currently not functioning
6. Default layout presets need improvement when adding widgets

**Instructions**:

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for current state and recent changes.

2. **Fix CSS Issues**: Investigate and fix the grey line and toggle position issues first.

3. **Select Task**: Then choose one of the heavy work items above to work on.

4. **Document**: Update `PROGRESS_HANDOFF.md` and `ISSUES.md` accordingly.
