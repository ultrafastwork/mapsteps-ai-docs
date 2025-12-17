# Agent Prompt - v2.11.8+32 (Archived)

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Implement Desktop Off-Canvas premium feature restrictions.

**Status**: Completed.

## Task: Desktop Off-Canvas Premium Feature Restrictions

### Problem

Desktop Off-Canvas features were present in the free theme while they are premium features:
1. The expanded "Desktop Off-Canvas" section in left panel had premium fields
2. The "Desktop Off-Canvas" panel could receive widget drag-and-drop while Premium Add-On is disabled

### Solution Implemented

1. **Left Panel Section**: Show premium notice banner when Premium Add-On is not active
2. **Header Builder Panel**: Block drag-and-drop and show lock overlay when Premium Add-On is not active
3. **Move Fields**: "Reveal as" field moved to Premium Add-On

### Files Modified

#### Theme (page-builder-framework):
- `inc/customizer/settings/header-builder/desktop/offcanvas-section.php`
- `Customizer/Controls/Builder/ResponsiveBuilderControl.php`
- `Customizer/Controls/Builder/src/builder-interface.ts`
- `Customizer/Controls/Builder/src/responsive-builder-control.ts`
- `Customizer/Controls/Builder/src/builder-control.scss`
- `Customizer/Controls/Base/src/base-control.scss`

#### Premium Add-On (wpbf-premium):
- `inc/customizer/controls/settings-header-builder.php`
