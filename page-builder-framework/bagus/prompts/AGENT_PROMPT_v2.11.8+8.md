# Agent Prompt

**Role**: You are an expert WordPress developer and AI coding assistant.

**Context**:
You are working on the "page-builder-framework" WordPress theme.
Your primary source of truth for the current state and tasks is the file:
`ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)
2. `.antigravityignore` (Forbidden files and directories that you MUST NOT access)
3. `ai-docs/page-builder-framework/rules.md` (Project-specific rules)

**Objective**:
Extract remaining sections from `styles.php` into dedicated module files to further improve maintainability and AI-friendliness.

**Instructions**:

1. **Read Context**: Read `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md` to understand what was completed in the previous session.

2. **Analyze Remaining Sections**: The current `styles.php` still has ~700 lines of content in the following sections:
   - Breadcrumbs (~60 lines)
   - Pagination (~80 lines)
   - Blog (~200 lines)
   - Header (old, non-builder) (~300 lines)
   - Footer (~80 lines)

3. **Plan**: Create an implementation plan for extracting these sections:
   - Determine which sections to group together (if any)
   - Define module file names (e.g., `breadcrumbs-styles.php`, `pagination-styles.php`, `blog-styles.php`, `header-styles.php`, `footer-styles.php`)
   - Identify any dependencies between sections

4. **Execute**: Implement the refactoring following the same pattern as v2.11.8+7:
   - Create new module files with proper docblocks and security checks
   - Extract code sections logically
   - Update main file with `require_once` statements
   - Verify syntax with `php -l`

5. **Verify**: Test that no syntax errors exist

6. **Document**: Update `PROGRESS_HANDOFF.md` with results and next steps
