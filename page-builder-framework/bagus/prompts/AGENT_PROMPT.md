# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Fix the HTML 2 Widget WYSIWYG editor toolbar issue.

**Issue (from `ai-docs/page-builder-framework/ISSUES.md`)**:
> The WYSIWYG editor in the HTML 2 Widget is too simple, make it to have same amount of toolbar items like in HTML 1 Widget.

**Problem Description**:
The HTML 2 Widget's WYSIWYG editor has fewer toolbar items compared to HTML 1 Widget. Both should have the same toolbar configuration.

**Instructions**:

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for current state.

2. **Investigate & Fix**:
   - Find the HTML Widget settings files in `inc/customizer/settings/header-builder/`
   - Compare HTML 1 and HTML 2 widget configurations
   - Identify the WYSIWYG/editor control and its toolbar settings
   - Make HTML 2 match HTML 1's toolbar configuration

3. **Verify**: Test in Customizer that both HTML widgets have identical toolbar items.

4. **Document**: Update `PROGRESS_HANDOFF.md` and mark issue fixed in `ISSUES.md`.
