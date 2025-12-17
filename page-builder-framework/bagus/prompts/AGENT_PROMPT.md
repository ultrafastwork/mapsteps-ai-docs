# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Test Desktop Off-Canvas premium restrictions and address deferred CSS issues.

**Status**: Desktop Off-Canvas premium feature restrictions have been implemented and committed.

## Task 1: Test Desktop Off-Canvas Premium Restrictions

### What Was Implemented

Desktop Off-Canvas is now properly restricted as a premium feature:
- Premium notice banner shows in the section when Premium Add-On is not active
- Drag-and-drop is blocked on the Desktop Off-Canvas panel with a lock overlay
- "Reveal as" field moved to Premium Add-On

### What to Test

1. **Without Premium Add-On**:
   - Go to WordPress Customizer → Header panel → Enable Header Builder
   - Click Desktop Off-Canvas settings icon
   - Verify premium notice banner appears in the section
   - Verify the Desktop Off-Canvas panel shows a lock overlay
   - Verify drag-and-drop is blocked on the Desktop Off-Canvas panel

2. **With Premium Add-On**:
   - Activate Premium Add-On plugin
   - Verify "Reveal as" field appears in Desktop Off-Canvas section
   - Verify drag-and-drop works normally on the Desktop Off-Canvas panel

## Task 2: Visual CSS Issues (Deferred)

See `PROGRESS_HANDOFF_v2.11.8+30_PENDING.md` for details:
- Grey line above "Header Builder" section title
- Toggle position slightly off when toggled off

### Instructions

1. **Read Context**: Read `PROGRESS_HANDOFF.md` for full details.
2. **Read Rules**: Check `ai-docs/page-builder-framework/rules.md` for project-specific guidelines.
3. **Test**: Verify the Desktop Off-Canvas premium restrictions work correctly.
4. **Document**: Update `PROGRESS_HANDOFF.md` with results.
