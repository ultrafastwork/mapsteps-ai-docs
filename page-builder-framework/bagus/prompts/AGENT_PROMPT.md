# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Fix the Font Size live preview bug in Header Builder rows.

**Issue (from `ai-docs/page-builder-framework/ISSUES.md`)**:
> The Font Size setting in the second row does not update in the live preview, though it applies after saving — and incorrectly affects the third row as well.

**Instructions**:

1. **Read Context**: Read `PROGRESS_HANDOFF.md` Section 2 for investigation steps and key files.

2. **Investigate & Fix**:
   - Find PHP settings in `Customizer/Controls/HeaderBuilder/settings/desktop/`
   - Find JS handlers in `inc/customizer/js/postmessage-parts/header-builder-rows.ts`
   - Check CSS output in `inc/customizer/styles/header-builder-styles.php`
   - Fix setting ID mismatches or incorrect CSS selectors

3. **Verify**: Run `pnpm run build-all` and test in Customizer.

4. **Document**: Update `PROGRESS_HANDOFF.md` and mark issue fixed in `ISSUES.md`.
