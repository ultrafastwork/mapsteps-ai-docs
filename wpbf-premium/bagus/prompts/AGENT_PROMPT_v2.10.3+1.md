# Agent Prompt: Verify Postmessage.ts Splitting

## Objective

Verify that the splitting of `wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage.ts` into smaller modular files was done correctly and completely.

---

## Prerequisites

**1. Read the project rules:**
```
ai-docs/wpbf-premium/rules.md
```

**2. Read the progress handoff document:**
```
ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md
```

This document contains:
- Summary of what was done
- List of all created files with purposes
- Key implementation details
- Known expected lint errors

---

## Context

The original `postmessage.ts` file (~1871 lines) has been split into 15 smaller files in a `postmessage-parts` directory. A backup of the original file exists for comparison.

---

## Files to Review

### Backup (Original)
```
wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage-backup.ts
```

### New Implementation
```
wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage.ts
wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage-parts/
├── utils.ts
├── theme-colors.ts
├── social.ts
├── text.ts
├── menu.ts
├── sub-menu.ts
├── headings.ts
├── navigation.ts
├── transparent-header.ts
├── sticky-navigation.ts
├── mobile-navigation.ts
├── call-to-action.ts
├── footer.ts
├── woocommerce.ts
└── mobile-offcanvas-handler.ts
```

### Reference (Theme Pattern)
```
wp-content/themes/page-builder-framework/inc/customizer/js/postmessage.ts
wp-content/themes/page-builder-framework/inc/customizer/js/postmessage-parts/
```

---

## Verification Tasks

### 1. Compare Settings Coverage
Compare the backup file against all part files to ensure every `listenToCustomizerValueChange` call from the original is present in the new implementation.

**Settings to verify exist in parts:**

#### theme-colors.ts
- `base_color_global`
- `base_color_alt_global`
- `brand_color_global`
- `brand_color_alt_global`
- `accent_color_global`
- `accent_color_alt_global`

#### social.ts
- `social_background_color`
- `social_color`
- `social_font_size`

#### text.ts
- `page_font_size`
- `page_line_height`
- `page_bold_color`

#### menu.ts
- `menu_letter_spacing`

#### sub-menu.ts
- `sub_menu_letter_spacing`

#### headings.ts
- `page_h1_font_size`, `page_h1_line_height`, `page_h1_letter_spacing`
- `page_h2_font_size`, `page_h2_font_color`, `page_h2_line_height`, `page_h2_letter_spacing`
- `page_h3_font_size`, `page_h3_font_color`, `page_h3_line_height`, `page_h3_letter_spacing`
- `page_h4_font_size`, `page_h4_font_color`, `page_h4_line_height`, `page_h4_letter_spacing`
- `page_h5_font_size`, `page_h5_font_color`, `page_h5_line_height`, `page_h5_letter_spacing`
- `page_h6_font_size`, `page_h6_font_color`, `page_h6_line_height`, `page_h6_letter_spacing`

#### navigation.ts
- `menu_stacked_bg_color`
- `menu_stacked_wysiwyg`
- `menu_stacked_logo_height`
- `menu_off_canvas_hamburger_size`
- `menu_position` (2 listeners)
- `menu_off_canvas_push`
- `menu_off_canvas_width`
- `menu_off_canvas_hamburger_color`
- `menu_off_canvas_bg_color`
- `menu_off_canvas_submenu_arrow_color`
- `menu_overlay`
- `menu_overlay_color`

#### transparent-header.ts
- `menu_transparent_width`
- `menu_transparent_background_color`
- `menu_transparent_font_color`
- `menu_transparent_font_color_alt`
- `menu_transparent_logo_color`
- `menu_transparent_logo_color_alt`
- `menu_transparent_tagline_color`
- `menu_transparent_hamburger_color`
- `menu_transparent_hamburger_color_mobile`
- `menu_transparent_hamburger_bg_color_mobile`

#### sticky-navigation.ts
- `menu_active_width`
- `menu_active_height`
- `menu_active_box_shadow`
- `menu_active_box_shadow_blur`
- `menu_active_box_shadow_color`
- `menu_active_stacked_bg_color`
- `menu_active_bg_color`
- `menu_active_font_colors`
- `menu_active_logo_color`
- `menu_active_logo_color_alt`
- `menu_active_logo_size`
- `menu_active_off_canvas_hamburger_color`
- `menu_padding` (for full screen menu)
- `mobile_menu_active_hamburger_color`
- `mobile_menu_active_hamburger_bg_color`

#### mobile-navigation.ts
- `mobile_menu_overlay_color`
- `mobile_menu_width`

#### call-to-action.ts
- `cta_button_text`
- `cta_button_border_radius`
- `cta_button_background_color`
- `cta_button_background_color_alt`
- `cta_button_font_color`
- `cta_button_font_color_alt`
- `cta_button_transparent_background_color`
- `cta_button_transparent_background_color_alt`
- `cta_button_transparent_font_color`
- `cta_button_transparent_font_color_alt`
- `cta_button_sticky_background_color`
- `cta_button_sticky_background_color_alt`
- `cta_button_sticky_font_color`
- `cta_button_sticky_font_color_alt`

#### footer.ts
- `footer_widgets_width`
- `footer_widgets_bg_color`
- `footer_widgets_headline_color`
- `footer_widgets_font_color`
- `footer_widgets_accent_color`
- `footer_widgets_font_size`

#### woocommerce.ts
- `woocommerce_menu_item_custom_label`
- `woocommerce_loop_quick_view_font_size`
- `woocommerce_loop_quick_view_font_color`
- `woocommerce_loop_quick_view_background_color`
- `woocommerce_loop_off_canvas_sidebar_font_color`
- `woocommerce_loop_off_canvas_sidebar_background_color`
- `woocommerce_loop_off_canvas_sidebar_overlay_color`

#### mobile-offcanvas-handler.ts
- `wpbfMobileRevealTypeHandlers["off-canvas"]` handler registration

---

### 2. Verify Utility Functions
Check that `utils.ts` contains all necessary utility functions:
- [ ] `breakpoints` constant
- [ ] `mediaQueries` constant
- [ ] `emptyNotZero()`
- [ ] `valueHasUnit()`
- [ ] `maybeAppendSuffix()`
- [ ] `toStringColor()`
- [ ] `headerBuilderEnabled()`
- [ ] `getStyleTag()`
- [ ] `removeStyleTag()`
- [ ] `writeCSS()`
- [ ] `listenToCustomizerValueChange()`

---

### 3. Build Verification
Run the TypeScript build to ensure no compilation errors:
```bash
pnpm run build
```

Or check for TypeScript errors:
```bash
pnpm tsc --noEmit
```

---

### 4. Functional Testing
Test in WordPress Customizer:
1. Open Customizer
2. Test live preview for settings from each category
3. Verify CSS is applied correctly in real-time

---

## Expected Lint Errors (Acceptable)

These errors are expected and resolve at build time:
- `Cannot find name 'JQueryStatic'`
- `Property 'wp' does not exist on type 'Window & typeof globalThis'`
- `Property 'WpbfTheme' does not exist on type 'Window & typeof globalThis'`

---

## Success Criteria

- [ ] All settings from backup exist in new part files
- [ ] No missing functionality
- [ ] TypeScript builds successfully
- [ ] Customizer live preview works correctly
- [ ] Code follows existing patterns from theme

---

## After Verification

If verification passes:
1. Delete the backup file: `wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage-backup.ts`
2. Update this document to mark as verified

If issues found:
1. Document the issues
2. Fix the affected part files
3. Re-verify
