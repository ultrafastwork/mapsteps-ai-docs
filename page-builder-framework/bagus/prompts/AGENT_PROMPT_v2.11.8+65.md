# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Refactor Footer Builder border-top controls to use "separator" terminology and improve field organization.

**Status**: Session v2.11.8+65 - Ready to start.

---

## Pending Tasks (v2.11.8+65)

Refactor border-top fields in Footer Builder's top, main, and bottom row sections (both desktop & mobile).

**Reference**: See `desktop/top-row-section.php` lines 126-203 as example. All 6 files have the same border control structure.

1. **Add "Top Separator" Headline**: Insert a headline field before the border controls (before priority 220).

2. **Swap Field Order**: Exchange priorities so Style comes before Width:
   - `border_top_style`: priority 225 → 220
   - `border_top_width`: priority 220 → 225

3. **Update Active Callbacks**:
   - Remove `activeCallback` from `border_top_style`.
   - Add `activeCallback` to `border_top_width`, `border_top_color`, and `border_top_scope` that depends on `border_top_style !== 'none'`.

4. **Rename Labels** (UI labels only):
   - "Border Top Width" → "Separator Width"
   - "Border Top Style" → "Separator Style"
   - "Border Top Color" → "Separator Color"
   - "Border Top Scope" → "Separator Scope"

**Note**: Keep field IDs (`border_top_*`) and CSS output unchanged.

---

## Recent Completed

- ✅ Border-Top Controls for Footer Builder Rows (v2.11.8+63)
  - 4 controls (Width, Style, Color, Scope) added to all 6 row sections
  - CSS output and postMessage live preview support
- ✅ Widget Title field for Menu 1, Menu 2, HTML 1, HTML 2 (v2.11.8+62)
- ✅ Widget Title layout fix - wrapper divs (v2.11.8+62)
- ✅ Footer Builder vertical alignment fix (v2.11.8+61)
- ✅ Footer Builder Menu widget styling (v2.11.8+61)
