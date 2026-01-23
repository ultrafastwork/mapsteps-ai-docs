# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Refactor customizer control CSS class naming to reduce markup size.

**Status**: Session v2.11.8+43 - Refactoring task.

---

## Refactoring Task

Simplify CSS class naming for customizer controls.

### Current State (Too Verbose)

```html
<li
	class="customize-control wpbf-customize-control wpbf-customize-control-generic"
></li>
```

### Target State (Simplified)

```html
<li class="customize-control wpbf-customize-control generic-control"></li>
```

Pattern: `wpbf-customize-control {controlType}-control`

---

## Scope

All files in `wp-content/themes/page-builder-framework/Customizer/`:

### PHP Files

- Start with `Controls/Base/BaseControl.php` - Main class generation logic
- Search for `wpbf-customize-control-` pattern

### TS/TSX Files

- Class references often in string concatenations
- Search for both literal and concatenated patterns

### CSS/SCSS Files

- Selector updates needed
- Search for `.wpbf-customize-control-` pattern

---

## Instructions

1. **Analyze** `BaseControl.php` to understand class generation
2. **Search** all files for `wpbf-customize-control` patterns
3. **Plan** changes (create implementation plan)
4. **Implement** PHP changes first
5. **Update** CSS/SCSS selectors
6. **Update** TS/TSX references
7. **Test** customizer to verify no regressions
