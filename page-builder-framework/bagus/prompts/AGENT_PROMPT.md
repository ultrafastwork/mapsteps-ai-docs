# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Test and verify Header Builder regression fix.

**Status**: Session v2.11.8+52 - Header Builder regression fix applied, awaiting verification.

---

## Previous Session Summary (v2.11.8+51)

Fixed **Header Builder regression** caused by Footer Builder introduction:

1. **Hardcoded Section Prefix** - Changed `wpbf_header_builder_` to dynamic `${this.params.id}_` in `handleRowSettingClick()` and `bindCustomizeSection()`

2. **Global Sortable Selectors** - Scoped `initSortable()` to specific builder panel using `$builderPanel.find()` instead of global `jQuery(".active-widgets")`

### Files Modified

| File | Changes |
|------|---------|
| `Customizer/Controls/Builder/src/responsive-builder-control.ts` | Fixed section prefix and sortable scoping |
| `Customizer/Controls/Builder/src/builder-control.ts` | Fixed section prefix and sortable scoping |

---

## Pending Tasks

1. **Manual Testing** - Verify Header Builder widget movement works in Customizer:
   - Add widgets to rows
   - Move widgets between columns (e.g., menu1 from column 1 to column 3)
   - Verify instant preview updates
   - Save and verify frontend renders correctly

2. **Footer Builder Testing** - Verify Footer Builder still works correctly after fix

3. **Regression Testing** - Ensure no other builder functionality was affected

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
