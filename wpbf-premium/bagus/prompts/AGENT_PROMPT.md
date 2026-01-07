# Agent Prompt

**Role**: Expert WordPress plugin developer and AI coding assistant.

**Context**: Working on "wpbf-premium" WordPress plugin.
**Source of Truth**: `ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/wpbf-premium/rules.md`
**Global Rules**: `.windsurfrules`

**Objective**: Add postmessage support for Footer Builder premium controls.

**Status**: Session v2.11.8+25 - Footer Builder postmessage.

---

## Background

### Footer Builder Integration (v2.11.8+24)

Created `settings-footer-builder.php` with premium controls for footer builder row sections:

- Added "Custom Content" controls to all 6 footer builder row sections (desktop and mobile)
- Control IDs: `wpbf_footer_builder_{row_key}_custom` (code field for shortcodes)

### Theme's Footer Builder Postmessage (v2.11.8+47)

The theme already has postmessage support for footer builder rows in:
- `inc/customizer/js/postmessage-parts/footer-builder-rows.ts`

This handles controls for rows 1 and 3 (desktop and mobile) - the NEW rows.
Row 2 (Main Row) uses moved controls that already have postmessage in `footer.ts`.

---

## Task: Add Postmessage Support for Footer Builder Premium Controls

### Important: Check Existing Postmessage First

The wpbf-premium plugin has existing postmessage scripts in `inc/customizer/js/postmessage-parts/`.

**Existing footer postmessage** in `postmessage-parts/footer.ts`:
- `footer_widgets_width`, `footer_widgets_bg_color`, `footer_widgets_headline_color`
- `footer_widgets_font_color`, `footer_widgets_accent_color`, `footer_widgets_font_size`

These are for the **Widget Footer** section, NOT the footer builder rows.

### Reference: Header Builder Postmessage Pattern

Study the theme's `header-builder-rows.ts` (lines 49-76) for how to handle existing vs new controls:

```typescript
/**
 * These fields are handled here for desktop_row_3 only
 * because desktop_row_3 didn't exist before the new header builder added.
 *
 * Max width:
 * - In desktop_row_1, the value is using the existing `pre_header_width` setting.
 * - In desktop_row_2, the value is using the existing `menu_width` setting.
 * ...
 */
if (rowKey === "desktop_row_3") {
    // Only add postmessage for NEW controls that don't have existing handlers
}
```

**Key insight**: Don't duplicate postmessage handlers for controls that already have them.

### Implementation Steps

1. **Analyze premium footer builder controls**:
   - The "Custom Content" controls (`wpbf_footer_builder_{row_key}_custom`) are code fields
   - Code fields typically use `partialRefresh` (server-side refresh), not postmessage
   - Check if any other premium controls need postmessage

2. **Check if postmessage is needed**:
   - Code fields with `partialRefresh` don't need postmessage (they refresh via AJAX)
   - Only controls with `transport: 'postMessage'` need postmessage handlers

3. **If postmessage is needed, create `footer-builder.ts`**:
   - Follow the pattern from theme's `footer-builder-rows.ts`
   - Import and call from `postmessage.ts`

4. **Build postmessage assets**: `pnpm build-postmessage`

### Premium Footer Builder Controls

| Control ID | Type | Transport | Needs Postmessage? |
|------------|------|-----------|--------------------|
| `wpbf_footer_builder_desktop_row_1_custom` | code | postMessage + partialRefresh | Likely NO (partialRefresh handles it) |
| `wpbf_footer_builder_desktop_row_2_custom` | code | postMessage + partialRefresh | Likely NO |
| `wpbf_footer_builder_desktop_row_3_custom` | code | postMessage + partialRefresh | Likely NO |
| `wpbf_footer_builder_mobile_row_1_custom` | code | postMessage + partialRefresh | Likely NO |
| `wpbf_footer_builder_mobile_row_2_custom` | code | postMessage + partialRefresh | Likely NO |
| `wpbf_footer_builder_mobile_row_3_custom` | code | postMessage + partialRefresh | Likely NO |

---

## Files Reference

| File | Purpose |
|------|---------|
| `inc/customizer/js/postmessage.ts` | Main entry point for premium postmessage |
| `inc/customizer/js/postmessage-parts/footer.ts` | Existing footer WIDGETS postmessage |
| `inc/customizer/settings/settings-footer-builder.php` | Premium footer builder controls |

### Theme Reference Files

| File | Purpose |
|------|---------|
| `themes/.../postmessage-parts/footer-builder-rows.ts` | Theme's footer builder rows postmessage |
| `themes/.../postmessage-parts/header-builder-rows.ts` | Pattern for handling existing vs new controls |

---

## Notes

- **Do NOT duplicate postmessage handlers** - check if controls already have handlers
- Code fields with `partialRefresh` typically don't need postmessage (AJAX refresh handles them)
- If no postmessage is needed, document this finding and move to next task
- Build with `pnpm build-postmessage` after any changes
