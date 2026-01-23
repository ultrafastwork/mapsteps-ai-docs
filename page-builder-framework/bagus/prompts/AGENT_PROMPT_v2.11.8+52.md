# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`
**Known Issues**: `ai-docs/page-builder-framework/issues.md`

**Objective**: Resolve Issue #1 in `issues.md` - Footer Builder Preview & Settings.

**Status**: Session v2.11.8+52 completed. Starting v2.11.8+53.

---

## Current Task: Issue #1 - Footer Builder Preview & Settings

- **Problem**: Widget preview and row settings (e.g., `wpbf_footer_builder_desktop_row_1_section`) are currently non-functional in the Customizer when the Footer Builder is enabled.
- **Goal**: Investigate and fix the JS/PHP logic responsible for rendering the footer builder preview and handling row settings clicks.

### Technical Context
- **Feature**: Footer Builder (New Feature).
- **Core Files**:
    - `Customizer/Controls/Builder/src/responsive-builder-control.ts` (Shared builder logic)
    - `inc/customizer/settings/settings-footer-builder.php` (Footer builder settings)
    - `inc/customizer/styles/footer-builder-rows-styles.php` (CSS output)
- **Setting ID**: `wpbf_enable_footer_builder` (Toggle), `wpbf_footer_builder` (The builder control).

---

## Pending Tasks

1. **Debugging**: Identify why `wpbf_footer_builder` settings are not triggering the expected preview updates.
2. **Fix**: Ensure row settings clicks correctly open the associated Customizer sections.
3. **Verification**: Confirm that adding/moving widgets in the Footer Builder reflects instantly in the Customizer preview.

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
