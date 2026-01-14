# Known Issues - Page Builder Framework

## Footer Issues

### 1. Footer Builder Preview & Settings
- **Status**: ✅ Resolved
- **Condition**: Footer Builder Enabled (`wpbf_enable_footer_builder` is true)
- **Problem**: Widget preview and row settings (e.g., `wpbf_footer_builder_desktop_row_1_section`) are currently non-functional in the Customizer.
- **Fix**: Restructured Footer Builder to use a template file (`inc/template-parts/footer-builder.php`) with the `<footer id="footer">` wrapper always rendered, and content hooked via `wpbf_footer_builder_content` action. Updated partialRefresh callbacks to use the new template.

### 2. Sticky Footer Field Placement (Footer Builder Enabled)
- **Status**: ✅ Resolved
- **Condition**: Footer Builder Enabled (`wpbf_enable_footer_builder` is true)
- **Problem**: In old non-Footer Builder mode, the "Sticky Footer" field is located in the "Footer Bar" section. Currently when Footer Builder is enabled, the "Sticky Footer" field (`footer_sticky`) is shown inside the Footer Builder main row settings, which is not desired.
- **Fix**: Modified `wpbf-premium/inc/customizer/js/customizer.ts` to move `footer_sticky` to `wpbf_footer_builder_main_section` (directly under the Footer Builder toggle) instead of `wpbf_footer_builder_desktop_row_2_section`.

## Header Issues

### 3. Hamburger Icon Customization of "Full Screen" Menu in NON Header Builder
- **Status**: ✅ Resolved
- **Condition**:
  - Use non-header builder (header builder disabled)
  - In customizer, navigate to "Header" -> "Navigation"
  - Set "Menu" field to "Full Screen" (a wpbf-premium feature).
- **Problem**: "Icon Color" (`menu_off_canvas_hamburger_color`) and "Icon Size" (`menu_off_canvas_hamburger_size`) settings under the Design Tab do not have any visual effect when the menu is in Full Screen mode.
- **Fix**:
  - **Icon Color**: The `menu_off_canvas_hamburger_color` setting was targeting wrong selector `.wpbf-nav-item` instead of `.wpbf-menu-toggle`. Updated both PHP styles (`wpbf-premium/inc/customizer/styles/off-canvas-menu-styles.php`) and postMessage handler (`wpbf-premium/inc/customizer/js/postmessage-parts/navigation.ts`) to use correct selector.
  - **Icon Size**: The theme's postMessage handler for `wpbf_header_builder_desktop_menu_trigger_icon_size` was creating a style tag that overrode the premium plugin's `menu_off_canvas_hamburger_size` styles due to CSS cascade order. Fixed by adding `removeStyleTag()` call when header builder is disabled, and added a listener for the header builder toggle to clean up the style tag when disabled mid-session. Modified `page-builder-framework/inc/customizer/js/postmessage-parts/menu-triggers.ts`.

### 4. Mobile Navigation Padding
- **Status**: ✅ Resolved
- **Condition**: Header Builder is disabled, and Menu field set to "Hamburger" or "Off Canvas"
- **Problem**: Adjusting the "Padding" setting (`mobile_menu_padding`) does not affect the actual mobile menu items both in the customize preview and in the front-end CSS output.
- **Fix**: The premium plugin's `mobile-navigation-styles.php` was only applying padding to the close button (`.wpbf-close`), not to menu items. Added CSS output for `.wpbf-mobile-menu-hamburger .wpbf-mobile-menu a` and `.wpbf-mobile-menu-off-canvas .wpbf-mobile-menu a` selectors. Also added postMessage handler in `mobile-navigation.ts` for live preview support.

### 5. Menu Font Size Implementation (Header Builder)
- **Status**: ✅ Resolved
- **Condition**:
  - The header builder's "HTML 1" or "HTML 2" widget added to main row (second row) at the first column.
  - The "Menu 1" OR "Menu 2" widget added to main row (second row) as well. "Menu 1" has `menu_font_size` field, "Menu 2" has `wpbf_header_builder_desktop_menu_2_menu_font_size` field.
  - Set the `wpbf_header_builder_desktop_row_2_font_size` field in Main Row's settings section to `14px` or other value. It will affect the font size for elements inside Main Row unless those element has their own font size setting.
  - The "Menu 1" or "Menu 2" has their own font size settings.
- **Expected Behavior**: The HTML widget will inherit main row's font size settings which is 14px, while Menu widget will use its own font size setting which is 16px.
- **Problem**:
  - The expected behavior works in customize preview, but not in frontend (sure, I already saved/pusblished the customizer). In frontend, the Menu widget is using 14px, inheriting row's value (which is fine), but doesn't use its own value.
- **Fix**: When header builder is enabled, always output menu font size (defaulting to 16px) to prevent inheriting row's font size. Added block comments explaining the architectural issue.

### 6. Footer Builder Issues
- **Status**: ✅ Resolved (v2.11.8+57)
- **Condition**: Footer Builder Enabled
- **Fixed Issues**:
  - **Main Row Settings**: ✅ Added controls (Container Width, Vertical Padding, Background Color, Font Color, Accent Color, Font Size) to desktop and mobile main-row-section.php files. (v2.11.8+56)
  - **Logo Widget**: ✅ Added Logo Width control to both desktop and mobile logo-section.php files. (v2.11.8+56)
  - **Copyright Widget**: ✅ Updated `wpbf_parse_template_tags()` to support `[year]` and `[blogname]` placeholders. (v2.11.8+56)
  - **Live Preview (HTML Widget)**: ✅ Implemented postMessage-based live preview for HTML widgets. Changed from partialRefresh to postMessage transport, added unique CSS classes to each HTML widget for targeting, and added postMessage handlers in `footer-builder-rows.ts`. (v2.11.8+57)
