# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Resolve Issue #2 in `issues.md` - Sticky Footer Field Placement (Footer Builder Enabled).

**Status**: Session v2.11.8+54 - Ready to start.

---

## Completed: Issue #1 - Footer Builder Preview & Settings ✅

Fixed in v2.11.8+53. See `PROGRESS_HANDOFF_v2.11.8+53_COMPLETE.md` for details.

---

## Current Task: Issue #2 - Sticky Footer Field Placement (Footer Builder Enabled)

- **Condition**: Footer Builder Enabled (`wpbf_enable_footer_builder` is true)
- **Problem**: When Footer Builder is enabled, the "Sticky Footer" field (`footer_sticky`) is currently located inside the Footer Builder main row settings. Desired behavior is to have it shown directly under the Footer Builder toggle field or moved into a dedicated section.
- **Goal**: When Footer Builder is enabled, show `footer_sticky` either:
	- Directly under the Footer Builder toggle field, or
	- In a separate Customizer section using section type `wpbf-expanded`, placed directly under the Footer Builder toggle.

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
