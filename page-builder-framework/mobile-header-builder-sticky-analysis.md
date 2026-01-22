# Mobile Header Builder Row Sticky Fix - Analysis for Next Agent

## Problem Statement

The mobile sticky row settings (`wpbf_header_builder_mobile_row_1_sticky`, `wpbf_header_builder_mobile_row_2_sticky`) are not working correctly. Setting one row to "disable" still makes it sticky if another row is set to "inherit" from an enabled desktop sticky setting.

## Test Cases

### Condition 1 (Current Bug)
- Mobile Top Row (row_1): `disable`
- Mobile Main Row (row_2): `inherit` (desktop sticky is ON)
- **Expected**: Mobile top row should NOT be sticky
- **Actual**: Mobile top row IS sticky (because `data-sticky="true"` is on wrapper)

### Condition 2 (Works)
- Mobile Top Row (row_1): `disable`
- Mobile Main Row (row_2): `disable`
- **Result**: Works correctly - no sticky

## Root Cause

The sticky attributes are added to the `.wpbf-navigation` wrapper element, not to individual rows. The current logic is:

```php
// If ANY row is sticky, add data-sticky="true" to wrapper
if ( ! empty( $sticky_classes ) ) {
    $attributes .= ' data-sticky="true"';
    // ...
}
```

This means is ANY mobile row is sticky, the ENTIRE navigation (including all rows) becomes sticky.

## Current Implementation

### Files Modified in This Session

1. **Theme**: [helpers.php](file:///c:/www/mapsteps/wp-content/themes/page-builder-framework/inc/helpers.php#L37-L102)
   - Function: `mobile_header_builder_sticky_rows()`
   - Filter: `wpbf_navigation_attributes` (priority 15)
   - Change: Added header builder enabled check

2. **Premium Plugin**: [helpers.php](file:///c:/www/mapsteps/wp-content/plugins/wpbf-premium/inc/helpers.php#L593-L630)
   - Function: `wpbf_sticky_navigation_attributes()`
   - Filter: `wpbf_navigation_attributes` (priority 10)
   - Change: Added check to skip when header builder is enabled

3. **Premium Plugin**: [settings-header-builder.php](file:///c:/www/mapsteps/wp-content/plugins/wpbf-premium/inc/customizer/settings/settings-header-builder.php)
   - Fixed duplicate partial refresh keys (`mobile_row_1_sticky`, `mobile_row_2_sticky`)

### Current Function Logic

```php
function mobile_header_builder_sticky_rows( $attributes = '' ) {
    if ( ! wpbf_header_builder_enabled() ) return $attributes;

    $rows = [
        'mobile_row_1' => ['setting' => 'wpbf_header_builder_mobile_row_1_sticky', 'desktop_setting' => 'pre_header_sticky'],
        'mobile_row_2' => ['setting' => 'wpbf_header_builder_mobile_row_2_sticky', 'desktop_setting' => 'menu_sticky'],
    ];

    $sticky_classes = [];
    foreach ( $rows as $row_key => $row_config ) {
        $mobile_sticky_value = get_theme_mod( $row_config['setting'], 'inherit' );
        
        if ( 'inherit' === $mobile_sticky_value ) {
            $is_sticky = (bool) get_theme_mod( $row_config['desktop_setting'], false );
        } elseif ( 'enable' === $mobile_sticky_value ) {
            $is_sticky = true;
        } else {
            $is_sticky = false;
        }

        if ( $is_sticky ) {
            $sticky_classes[] = $row_config['class'];
        }
    }

    // BUG: This adds sticky to ENTIRE navigation, not per-row
    if ( ! empty( $sticky_classes ) ) {
        $attributes .= ' data-sticky="true"';
        // ...
    }
    return $attributes;
}
```

## Correct Solution: Move Rows Into/Out of Sticky Wrapper

The existing architecture does NOT use "per-row sticky". Instead, it **moves sticky rows INTO the `.wpbf-navigation` wrapper** and keeps non-sticky rows OUTSIDE.

### Desktop Header Builder Example

In `wpbf-premium/inc/theme-mods.php`:

```php
// When header builder is enabled and pre_header_sticky is ON:
function wpbf_premium_after_header_builder_hooks() {
    if ( ! get_theme_mod( 'wpbf_enable_header_builder', false ) ) return;
    if ( ! get_theme_mod( 'pre_header_sticky' ) ) return;

    // MOVE pre-header FROM outside TO inside navigation
    remove_action( 'wpbf_pre_header', [..., 'do_desktop_pre_header'] );
    add_action( 'wpbf_navigation', [..., 'do_desktop_pre_header'], 9 );
}
```

### How It Works

1. **Non-sticky rows** are rendered in `wpbf_pre_header` action (OUTSIDE `.wpbf-navigation`)
2. **Sticky rows** are moved to `wpbf_navigation` action (INSIDE `.wpbf-navigation`)
3. When scrolling, entire `.wpbf-navigation` becomes fixed (with everything inside it)
4. Non-sticky rows stay in place (outside the sticky wrapper)

### What's Missing for Mobile

The mobile header builder needs similar logic:
1. Render mobile rows OUTSIDE `.wpbf-navigation` by default
2. When a mobile row's sticky = "enable" or "inherit" (from enabled desktop), MOVE it INSIDE
3. The sticky JS doesn't need changes - just which rows are inside/outside the wrapper

### Files to Modify

1. **Theme's `HeaderBuilderOutput.php`**: `do_mobile_navigation()` method
   - Currently renders ALL mobile rows inside `.wpbf-mobile-header-rows`
   - Need to separate: sticky rows inside `.wpbf-navigation`, non-sticky outside

2. **Premium's `theme-mods.php`**: Add similar logic for mobile rows
   - Check `wpbf_header_builder_mobile_row_1_sticky` and `wpbf_header_builder_mobile_row_2_sticky`
   - Move sticky rows into navigation via action hooks

3. **Theme's `helpers.php`**: `mobile_header_builder_sticky_rows()` 
   - May need to be removed or significantly changed
   - The sticky attributes are added by premium's `wpbf_sticky_navigation_attributes()` based on desktop `menu_sticky`

## Mapping Table

| Mobile Row | Mobile Setting | Desktop Setting to Inherit | Row HTML Class |
|------------|----------------|---------------------------|----------------|
| Top Row (1) | `wpbf_header_builder_mobile_row_1_sticky` | `pre_header_sticky` | `.wpbf-header-row-mobile_row_1` |
| Main Row (2) | `wpbf_header_builder_mobile_row_2_sticky` | `menu_sticky` | `.wpbf-header-row-mobile_row_2` |

## Files to Review

1. Theme helpers.php - `mobile_header_builder_sticky_rows()`
2. Premium helpers.php - `wpbf_sticky_navigation_attributes()` 
3. Premium site.ts/js - Sticky navigation JavaScript
4. Premium settings-header-builder.php - Customizer settings

## Next Steps

1. Modify PHP to output `data-mobile-sticky-rows` attribute with comma-separated row keys
2. Update JavaScript to handle per-row sticky instead of entire navigation
3. Test all combinations of settings
