# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Add postmessage support for Footer Builder.

**Status**: Session v2.11.8+47 - Footer Builder postmessage.

---

## Background

The **Footer Builder** feature was implemented in session v2.11.8+45, and controls movement was added in session v2.11.8+46. The implementation includes:

- `Customizer/FooterBuilder/FooterBuilderConfig.php` - Widget and slot definitions
- `Customizer/FooterBuilder/FooterBuilderOutput.php` - Frontend rendering
- `inc/customizer/settings/settings-footer-builder.php` - Main settings
- `inc/customizer/settings/footer-builder/desktop/*.php` - 10 desktop section files
- `inc/customizer/settings/footer-builder/mobile/*.php` - 10 mobile section files
- `inc/customizer/js/customizer-parts/setup-controls-movement.ts` - Controls movement (header + footer)

---

## Task: Add Postmessage Support for Footer Builder

The header builder has postmessage scripts for live preview. Footer builder should have similar support.

### Important: Existing Footer Postmessage Scripts

**The existing footer controls already have postmessage scripts** in `inc/customizer/js/postmessage-parts/footer.ts`:

```typescript
// Existing postmessage handlers in footer.ts:
- footer_width
- footer_height
- footer_bg_color
- footer_font_color
- footer_accent_color
- footer_accent_color_alt
- footer_font_size
```

These controls are **moved** to footer builder row sections when footer builder is enabled, but they still use the same setting IDs. So the existing postmessage scripts should continue to work.

### Reference: Header Builder Postmessage Pattern

Study `inc/customizer/js/postmessage-parts/header-builder-rows.ts` (lines 49-76) for the pattern:

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

**Key insight**: Header builder reuses existing settings (and their postmessage handlers) for row 1 and row 2. Only row 3 (which is new) needs new postmessage handlers.

### Implementation Steps

1. **Analyze footer builder controls**:
   - Which controls are moved from existing footer settings? (already have postmessage)
   - Which controls are NEW to footer builder? (need new postmessage)

2. **Create `footer-builder-rows.ts`** (if needed):
   - Add postmessage handlers for NEW footer builder row controls only
   - Follow the pattern from `header-builder-rows.ts`

3. **Create other footer builder postmessage files** (if needed):
   - `footer-builder.ts` - for general footer builder controls
   - Consider widget-specific postmessage if needed

4. **Update `postmessage.ts`**:
   - Import and call new footer builder postmessage setup functions

5. **Build postmessage assets**: `pnpm build-postmessage`

### Footer Builder Row Sections

| Row | Section ID | Notes |
|-----|------------|-------|
| Row 1 (Top) | `wpbf_footer_builder_desktop_row_1_section` | NEW - may need postmessage |
| Row 2 (Main) | `wpbf_footer_builder_desktop_row_2_section` | Receives moved controls |
| Row 3 (Bottom) | `wpbf_footer_builder_desktop_row_3_section` | NEW - may need postmessage |

### Controls Analysis

**Moved controls** (already have postmessage in `footer.ts`):
- `footer_width`, `footer_height`, `footer_bg_color`, `footer_font_color`
- `footer_accent_color`, `footer_accent_color_alt`, `footer_font_size`

**Potentially NEW controls** (may need postmessage):
- Row 1 and Row 3 specific controls (max_width, vertical_padding, bg_color, text_color, accent_colors)
- Row visibility controls
- Widget-specific controls

---

## Postmessage Files Reference

| File | Purpose |
|------|---------|
| `postmessage.ts` | Main entry point, imports all postmessage modules |
| `postmessage-parts/footer.ts` | Existing footer postmessage (7 controls) |
| `postmessage-parts/header-builder.ts` | Header builder general controls |
| `postmessage-parts/header-builder-rows.ts` | Header builder row controls (pattern to follow) |

---

## Notes

- **Do NOT duplicate postmessage handlers** - if a control already has a handler in `footer.ts`, don't add another
- Footer builder rows may need visibility toggle postmessage (like header builder)
- Check if CSS selectors need updating for footer builder context
- Build with `pnpm build-postmessage` after changes
