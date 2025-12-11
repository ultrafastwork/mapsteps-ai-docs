# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Fix the Button Size default value issue.

**Issue (from `ai-docs/page-builder-framework/ISSUES.md`)**:
> The default Button Size field appears empty instead of showing a default value.

**Problem Description**:
The Button Size customizer control in the Header Builder Button Widget shows an empty field instead of displaying a default value.

**Instructions**:

1. **Read Context**: Read `PROGRESS_HANDOFF.md` Section 2 for investigation steps.

2. **Investigate & Fix**:
   - Find the Button Widget settings file in `inc/customizer/settings/header-builder/`
   - Check the `button_size` or similar control definition
   - Verify if `defaultValue()` is set correctly
   - Check if the control type supports default value display

3. **Verify**: Run `pnpm run build-asset -- --path=<specific-file-path>` (only build the specific file that was changed) and test in Customizer.

4. **Document**: Update `PROGRESS_HANDOFF.md` and mark issue fixed in `ISSUES.md`.
