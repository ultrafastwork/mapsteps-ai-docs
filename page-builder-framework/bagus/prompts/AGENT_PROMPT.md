# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Resolve Issue #2 in `issues.md` - Sticky Footer Toggle Visibility.

**Status**: Session v2.11.8+54 - Ready to start.

---

## Completed: Issue #1 - Footer Builder Preview & Settings ✅

Fixed in v2.11.8+53. See `PROGRESS_HANDOFF_v2.11.8+53_COMPLETE.md` for details.

---

## Current Task: Issue #2 - Sticky Footer Toggle Visibility

- **Condition**: Enable Footer Builder, then disable it, then navigate to Footer Bar.
- **Problem**: The "Sticky Footer" toggle (`footer_sticky`) appears in the "Footer Bar" section even though it should be hidden or integrated with the Builder logic when the Builder is active or recently toggled.
- **Goal**: Fix visibility logic for `footer_sticky` toggle.

### Technical Context
- **Setting ID**: `footer_sticky`
- **Related Setting**: `wpbf_enable_footer_builder`

---

## Builder Control Reference

### Key Files

| Category | File |
|----------|------|
| Responsive Builder | `Customizer/Controls/Builder/src/responsive-builder-control.ts` |
| Builder Control | `Customizer/Controls/Builder/src/builder-control.ts` |
| Bundle Output | `Customizer/Controls/Bundle/dist/controls-bundle-min.js` |

### Build Command

```bash
pnpm run build-controls-bundle
```
