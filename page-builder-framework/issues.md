# Known Issues - Page Builder Framework

## Footer Issues

### 1. Footer Builder Preview & Settings
- **Status**: 🔴 Pending
- **Condition**: Footer Builder Enabled (`wpbf_enable_footer_builder` is true)
- **Problem**: Widget preview and row settings (e.g., `wpbf_footer_builder_desktop_row_1_section`) are currently non-functional in the Customizer.

### 2. Sticky Footer Toggle Visibility
- **Status**: 🔴 Pending
- **Condition**: Enable Footer Builder, then disable it, then navigate to Footer Bar.
- **Problem**: The "Sticky Footer" toggle (`footer_sticky`) appears in the "Footer Bar" section even though it should be hidden or integrated with the Builder logic when the Builder is active or recently toggled.

## Header Issues

### 3. Hamburger Icon Customization (Full Screen)
- **Status**: 🔴 Pending
- **Condition**: Menu set to "Full Screen"
- **Problem**: "Icon Color" (`mobile_menu_hamburger_color`) and "Icon Size" (`mobile_menu_hamburger_size`) settings under the Design Tab for mobile navigation do not have any visual effect when the menu is in Full Screen mode.

### 4. Mobile Navigation Padding
- **Status**: 🔴 Pending
- **Condition**: Menu set to "Hamburger" or "Off Canvas"
- **Problem**: Adjusting the "Padding" setting (`mobile_menu_padding`) does not affect the actual mobile menu items as expected in the front-end CSS output.

### 5. Menu Font Size Implementation (Header Builder)
- **Status**: 🔴 Pending
- **Condition**: Header Builder Menu widget (e.g., `wpbf_header_builder_desktop_menu_1_menu_font_size`) added to a row.
- **Problem**: The Font Size settings saved in the Header Builder are not correctly implemented or rendered on the Front End, possibly due to priority issues in `header-builder-menu-styles.php`.
