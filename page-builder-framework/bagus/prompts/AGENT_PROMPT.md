# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Fix reported visual CSS issues.

**Status**: Customizer asset optimization completed in v2.11.8+29. Visual CSS issues reported.

**Task - Visual CSS Issues**:
1. **Grey line above "Header Builder" section title** - Thin grey border appeared
2. **Toggle position slightly off when toggled off** - Alignment issue

These issues are NOT from the bundling changes (bundle imports original SCSS unchanged). May be pre-existing or from earlier commits. Investigate CSS in:
- `Customizer/Controls/Headline/src/headline-toggle-control.scss`
- `Customizer/Controls/Checkbox/src/` (toggle styles)

**Instructions**:

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for current state and recent changes.

2. **Fix CSS Issues**: Investigate and fix the grey line and toggle position issues.

3. **Document**: Update `PROGRESS_HANDOFF.md` accordingly.
