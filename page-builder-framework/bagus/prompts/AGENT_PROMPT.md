# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Add border-top controls to Footer Builder rows.

**Status**: Session v2.11.8+63 - Ready to start.

---

## Pending Tasks (v2.11.8+63)

- **Add Border-Top Controls to Footer Builder Rows**:
  - Add customizer fields to all footer builder rows (desktop and mobile):
    - Desktop: Top Row, Main Row, Bottom Row (`desktop_row_1`, `desktop_row_2`, `desktop_row_3`)
    - Mobile: Top Row, Main Row, Bottom Row (`mobile_row_1`, `mobile_row_2`, `mobile_row_3`)
  - **Controls to add**:
    - Border Width (slider, px)
    - Border Style (select: solid, dashed, dotted, none)
    - Border Color (color picker with alpha)
    - Border Scope (select: Container / Fullwidth) - whether border applies to container or full-width row
  - **Implementation Requirements**:
    - Add customizer fields to row section files in `inc/customizer/settings/footer-builder/{desktop,mobile}/`
    - Update CSS output in `inc/customizer/styles/footer-builder-styles.php`
    - Add postMessage handlers in `inc/customizer/js/postmessage-parts/footer-builder-rows.ts`
    - Build postMessage bundle after TypeScript changes
  - **Reference**: Look at existing row section files for the pattern (e.g., `desktop/top-row-section.php`)

---

## Recent Completed

- ✅ Widget Title field for Menu 1, Menu 2, HTML 1, HTML 2 (desktop and mobile) (v2.11.8+62)
- ✅ Widget Title layout fix - wrapper divs for proper stacking (v2.11.8+62)
- ✅ Footer Builder vertical alignment fix (v2.11.8+61)
- ✅ Footer Builder Menu widget styling - vertical layout (v2.11.8+61)
