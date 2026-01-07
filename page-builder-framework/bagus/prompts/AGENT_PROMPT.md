# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Verify CSS class refactoring - test customizer controls.

**Status**: Session v2.11.8+44 - Testing task.

---

## Background

CSS class naming for customizer controls was refactored in v2.11.8+43:

- **Before**: `wpbf-customize-control wpbf-customize-control-{type}`
- **After**: `wpbf-customize-control {type}-control`

Files modified: 8 PHP, 17 SCSS, 2 TS/TSX files.
Build: Controls bundle rebuilt successfully.

---

## Testing Task

Verify all customizer controls render correctly with new class names.

### Instructions

1. **Open WordPress Customizer** and navigate through sections
2. **Verify Control Types**:
   - Color controls
   - Slider controls
   - Toggle/Switch controls
   - Responsive controls
   - Margin/Padding controls
   - Radio/Checkbox controls
   - Select controls
   - Headline controls
   - Builder controls
3. **Check for Styling Issues**: Report any CSS regressions
4. **Document Findings**: Update handoff with test results
