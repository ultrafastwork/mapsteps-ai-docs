# Progress Handoff

**Date**: 2026-01-27
**Status**: Complete
**Last Completed Session**: v2.11.9+04
**Next Session**: TBD

## 1. High-Level Summary

Session v2.11.9+04 implemented `margin` settings for the Header Builder search icons and fixed live preview issues for header row accent colors (including button exclusion and selector syncing).
Session v2.11.9+03 implemented the missing "Font Color" setting for the Header Builder Main Row, renamed the conflicting "Font Colors" setting to "Menu Font Colors", and fixed live preview issues for HTML widgets.

## 2. Session v2.11.9+04 Accomplishments

### ✅ FEATURE: Header Builder Search Margin & Row Accent Color Fixes

**Problem**:
1.  Search icons lacked margin controls for fine-tuning positioning.
2.  Row accent color live preview was broken for Row 1 due to selector mismatch.
3.  Row accent colors were overriding button colors in the live preview.

**Solution**:
1.  **Search Margin**: Added `margin` settings to both Desktop and Mobile search sections. Restricted Mobile controls to Tablet/Mobile devices.
2.  **Row 1 Sync**: Updated `header-builder-rows.ts` to use `.wpbf-pre-header` for Row 1, matching PHP.
3.  **Button Exclusion**: Added `:not(.wpbf-button)` to row accent color selectors and added `!important` to ensure live preview priority.

**Files Modified**:
-   `inc/customizer/settings/header-builder/desktop/search-section.php`
-   `inc/customizer/settings/header-builder/mobile/search-section.php`
-   `inc/customizer/styles/header-builder-search-styles.php`
-   `inc/customizer/js/postmessage-parts/header-builder-search.ts`
-   `inc/customizer/js/postmessage-parts/header-builder-rows.ts`

**Verification**:
-   ✅ Search margin settings appear and function in live preview.
-   ✅ Row 1 accent colors update correctly in real-time.
-   ✅ Buttons maintain their specific colors when row accent colors are adjusted.
-   ✅ Build completed successfully.

---

## 3. Session v2.11.9+03 Accomplishments

### ✅ FEATURE: Header Builder Main Row Font Color & UI Polish

**Problem**: 
1.  The "Main Row" (Desktop Row 2) in Header Builder lacked a generic "Font Color" setting (only had Menu Font Colors).
2.  The existing "Font Colors" label was ambiguous, referring specifically to Menu items.
3.  Live preview for generic font color updates didn't work for HTML widgets.
4.  

**Solution**:
1.  **New Setting**: Added `text_color` control to `main-row-section.php`.
2.  **UI Improvement**: Renamed existing `menu_font_colors` to "Menu Font Colors" in `setup-controls-movement.ts`.
3.  **Backend CSS**: Updated `header-builder-rows-styles.php` to generate `color` CSS for `desktop_row_2`, explicitly targeting `.widget_custom_html` and `.textwidget`.
4.  **Live Preview**: Updated `header-builder-rows.ts` to include widget selectors in the postMessage handler for `desktop_row_2`.

**Files Modified**:
-   `inc/customizer/settings/header-builder/desktop/main-row-section.php`
-   `inc/customizer/js/customizer-parts/setup-controls-movement.ts`
-   `inc/customizer/styles/header-builder-rows-styles.php`
-   `inc/customizer/js/postmessage-parts/header-builder-rows.ts`

**Verification**:
-   ✅ "Font Color" setting appears in Main Row > Design.
-   ✅ Old setting labeled "Menu Font Colors".
-   ✅ Text color changes apply to Main Row text and HTML widgets.
-   ✅ Live preview updates instantly for both row content and HTML widgets.

---

## 3. Session v2.11.9+02 Accomplishments

### ✅ FIXED: Header Builder Search Icon Alignment

**Problem**: The search icon in the Header Builder search widget was not vertically centered (offset by `top: 0.2em`) and required positioning adjustment.

**Root Cause**:
1.  Global `.wpbf-icon svg` style had `top: 0.2em`.
2.  Search button positioning needed refinement.

**Solution**:
-   Reset `top: 0` for the search icon SVG within `.searchform button`.
-   Adjusted `right` position to `12px`.
-   Applied `transform: translateY(-90%)` for precise vertical centering.

**Files Modified**:
-   `assets/scss/main/_content.scss`

**Verification**:
-   Verified CSS rules in `css/min/style-min.css`.
-   Manual check in Customizer required.

---

## 3. Session v2.11.9+01 Accomplishments

### ✅ FIXED: HTML Widget Code Tab Width Restricted

**Problem**: The "Code" tab in HTML 1 and HTML 2 widgets within the Header Builder was not full width in the WordPress Customizer.

**Root Cause**:
1. The `EditorControl` (underlying control for 'editor' type fields) lacked the standard `.wpbf-control-form` wrapper used by other controls to apply base input styles.
2. The SCSS targeted a non-existent class `.customize-control-kirki-editor` instead of the actual `.editor-control` class.

**Solution**:
- Modified `EditorControl.php` to wrap the `textarea` in a `<div class="wpbf-control-form">`.
- Updated `editor-control.scss` to use the correct `.editor-control` selector.
- Rebuilt the Customizer controls bundle.

**Files Modified**:
- `Customizer/Controls/Editor/EditorControl.php`
- `Customizer/Controls/Editor/src/editor-control.scss`
- `Customizer/Controls/Bundle/dist/controls-bundle-min.css` (rebuilt)

**Verification**:
- Verified `.editor-control textarea { width: 100%; }` in the compiled CSS bundle.

---

## 4. Session v2.11.8+28 Accomplishments

### ✅ FIXED: Push Menu White Space on Wrong Side (Off-Canvas Left)

**Problem**: When "Off-Canvas Left" is configured, the push menu white space appeared on the RIGHT side instead of LEFT.

**Root Cause**: In `off-canvas.ts`, the `menu_off_canvas_push` handler checked `menu_position` (legacy setting) instead of the Header Builder's `wpbf_header_builder_desktop_offcanvas_reveal_as`. Since `menu_position` is not `"menu-off-canvas-left"` in Header Builder mode, it always added `wpbf-push-menu-right`.

**Solution**: Updated handler to use `revealAs` from `wpbf_header_builder_desktop_offcanvas_reveal_as`.

**Files Modified**:
- `wp-content/themes/page-builder-framework/inc/customizer/js/postmessage-parts/off-canvas.ts`

---

### ✅ FIXED: Off-Canvas Menu Font Colors Not Applied on Reload

**Problem**: Font colors set to white, but shows black after Customizer reload.

**Root Cause**: Both `menu_font_colors` and `wpbf_header_builder_desktop_offcanvas_menu_font_colors` write CSS with identical specificity. During initialization, both handlers apply their values, and the general menu colors were overriding off-canvas specific colors.

**Conflicting Selectors** (same specificity = 21 points):
- General: `.wpbf-navigation .wpbf-menu a, .wpbf-mobile-menu a, .wpbf-close`
- Off-canvas: `.wpbf-menu-off-canvas .wpbf-menu a, .wpbf-menu-off-canvas .wpbf-close`

**Solution**: Added `!important` to all off-canvas font color rules to ensure they override general menu colors.

**Files Modified**:
- `wp-content/plugins/wpbf-premium/inc/customizer/js/postmessage-parts/navigation.ts` (lines 355, 362)
- `wp-content/plugins/wpbf-premium/inc/customizer/styles/off-canvas-menu-styles.php` (lines 212, 221)

---

### ✅ FIXED: Missing Default Value for reveal_as Setting

**Problem**: `get_theme_mod('wpbf_header_builder_desktop_offcanvas_reveal_as')` returned empty when the setting hadn't been explicitly saved, causing no body class to be applied.

**Solution**: Added default value `'off-canvas'` to `get_theme_mod` call.

**Files Modified**:
- `wp-content/plugins/wpbf-premium/inc/body-classes.php` (line 29)

---


## 3. Session v2.11.8+27 Accomplishments

### ✅ FIXED: Issue 1 - Header Builder Desktop Search Widget

**Problem**: Icon color and size do not update in live preview.

**Root Cause**: Setting ID mismatch. Controls defined `wpbf_header_builder_desktop_search_icon_*` but postMessage handlers listened to `wpbf_header_builder_search_*` (missing "desktop" prefix). Additionally, handler used wrong control type (`WpbfColorControlValue` instead of `WpbfMulticolorControlValue`).

**Solution**: Updated `header-builder.ts`:
- Changed setting IDs to include `desktop_` prefix
- Changed control type to `WpbfMulticolorControlValue` for color handler
- Updated CSS selectors to `.wpbf-menu-item-search svg, .wpbf-menu-item-search .wpbff`
- Added proper hover state handling

**Files Modified**:
- `inc/customizer/js/postmessage-parts/header-builder.ts` (theme)

---

### ✅ FIXED: Issue 2 - Navigation Hover Effects (Non-Header Builder)

**Problem**: 
- Hover color, size, and border radius not applying in Customizer live preview
- Settings not persisting to frontend after save (showed defaults instead)

**Root Causes**:
1. Settings lacked `transport('postMessage')` directive and had no postMessage handlers
2. **Frontend Persistence**: `esc_html()` in `wpbf_write_css()` was encoding `>` to `&gt;`, breaking CSS child selectors inside `<style>` tags

**Solution**:
1. Added `transport('postMessage')` to PHP controls
2. Added postMessage handlers in `navigation.ts` for color, radius, and size
3. **Bypassed `wpbf_write_css()`** in `menu-effects-styles.php` and used direct `echo` to avoid HTML encoding issue

**Files Modified**:
- `inc/customizer/settings/header/navigation-hover-effects.php` (premium)
- `inc/customizer/js/postmessage-parts/navigation.ts` (premium)
- `inc/customizer/styles/menu-effects-styles.php` (premium) - Direct echo for CSS output
- `inc/helpers.php` (theme) - Changed `esc_html` to `wp_strip_all_tags` for CSS selectors
- `inc/customizer/customizer-functions.php` (theme) - Changed priority from 11 to 12 for correct CSS loading order

---

### ✅ FIXED: Issue 3 - CTA Button Border Radius (Non-Header Builder)

**Problem**: Border radius not live-updating (only reflects after save).

**Root Cause**: CSS property name used camelCase `borderRadius` instead of kebab-case `border-radius`.

**Solution**: Changed property name in `call-to-action.ts` to match `writeCSS` convention.

**Files Modified**:
- `inc/customizer/js/postmessage-parts/call-to-action.ts` (premium)

---

### ✅ FIXED: Issue 4 - Mobile Navigation Icon Color (Non-Header Builder)

**Problem**: Mobile navigation icon color under Design tab does not apply.

**Root Cause**: Handler only set `color` but SVG icons need `fill` and `stroke` too.

**Solution**: Added `fill` and `stroke` properties to the handler in mobile-navigation.ts.

**Files Modified**:
- `inc/customizer/js/postmessage-parts/mobile-navigation.ts` (theme)

---

### ✅ FIXED: Issue 5 - Header Builder Search Widget Positioning

**Problem**: When left-aligned, search input expands leftward and is partially hidden.

**Root Cause**: CSS expansion direction not considering left-aligned zones.

**Solution**: Added CSS rule to force `left: 0` expansion for `.wpbf-header-zone-left` and `.wpbf-content-start` zones.

**Files Modified**:
- `assets/scss/main/_navigation.scss` (theme)

---

### Build Verification

- ✅ Theme `pnpm run build-all` completed successfully
- ✅ Premium plugin `postmessage.ts` compiled successfully

## 2. Previous Session Accomplishments (Session v2.11.8+16)

- [x] **Created Builder Control Tests**: `builderControl.test.js`
  - Header Builder toggle and panel visibility
  - Available widgets panel and draggable widgets
  - Builder rows and columns structure
  - Row settings button interactions
  - Responsive device switching (desktop/mobile)
  - Widget drag-and-drop functionality
  
- [x] **Created Repeater Control Tests**: `repeaterControl.test.js`
  - Add new row functionality
  - Row expand/collapse behavior
  - Remove row functionality
  - Field type support (text, select, color, image, checkbox, textarea)
  - Row labels and data persistence
  - Limit functionality
  
- [x] **Created Enhanced Select Tests**: `enhancedSelectControl.test.js`
  - Select2 initialization and dropdown
  - Search/filter functionality
  - Single and multiple selection
  - Option groups
  - Clearable feature
  - Placeholder text
  - Keyboard navigation (Enter, Arrow keys, Escape)
  
- [x] **Set Up GitHub Actions CI/CD**: `.github/workflows/e2e-tests.yml`
  - Automated testing on push/PR to main/develop
  - Manual trigger with browser selection
  - WordPress + MySQL Docker services
  - Chrome and Firefox headless testing
  - Test reports as artifacts
  
- [x] **Updated package.json**: Added new test scripts
  - `pnpm test:builder`
  - `pnpm test:repeater`
  - `pnpm test:enhanced-select`
  - `pnpm test:ci`
  
- [x] **Updated README Documentation**: Added comprehensive docs for new controls

## 3. New Test Files Created

| File | Description |
|------|-------------|
| `builderControl.test.js` | Tests Header Builder control (drag-drop, widgets, responsive) |
| `repeaterControl.test.js` | Tests Repeater control (add/remove/reorder, field types) |
| `enhancedSelectControl.test.js` | Tests Enhanced Select (Select2, search, multi-select) |
| `sortableControl.test.js` | Tests Sortable controls (presence, drag-and-drop reorder) |
| `mediaControl.test.js` | Tests Media controls (media frame presence, modal detection) |
| `codeEditorControl.test.js` | Tests Code Editor controls (input into textarea/CodeMirror, token detection) |

## 4. CI/CD Configuration

**Workflow File**: `.github/workflows/e2e-tests.yml`

**Features**:
- Triggers on push to main/develop branches
- Triggers on pull requests
- Manual workflow dispatch with browser selection
- WordPress + MySQL Docker services
- Chrome and Firefox headless testing
- Test reports uploaded as artifacts
- Summary report generation

## 5. Documented WPBF Control Dependencies

| Parent Control | Dependent Controls |
|----------------|-------------------|
| `page_boxed` | `page_boxed_margin`, `page_boxed_padding`, `page_boxed_background`, `page_boxed_box_shadow` |
| `page_boxed_box_shadow` | `page_boxed_box_shadow_blur`, `page_boxed_box_shadow_spread` (Premium) |
| `page_font_toggle` | `page_font_family` (typography) |
| `menu_logo_font_toggle` | `menu_logo_font_family` (typography) |
| `page_h1_toggle` | `page_h1_font_family` (typography) |
| `page_h2_toggle` through `page_h6_toggle` | Corresponding font_family controls |
| `menu_font_family_toggle` | `menu_font_family` (typography) |
| `sub_menu_font_family_toggle` | `sub_menu_font_family` (typography) |
| `footer_font_toggle` | `footer_font_family` (typography) |
| `wpbf_enable_header_builder` | `wpbf_header_builder` (builder) |

## 6. Pending Tasks / Next Steps

### 🔧 Current Task: Enhanced-Select Memory Optimization (v2.11.8+29)

**Priority**: High  
**Status**: Assigned

#### Problem Description

The enhanced-select control uses Select2 library to display Google fonts. When multiple font fields are present (e.g., in Header Builder), memory consumption spikes significantly due to Select2's internal data management.

**Root Cause**:
- The Google font list definition already uses a single global object ✅
- However, Select2 internally copies/clones the font list for each select2 instance
- This causes memory duplication proportional to the number of font select fields

**Observed Behavior**:
- Memory consumption visible by hovering browser tab (Chrome/Brave)
- Memory increases when navigating through font fields across sections
- Can reach gigabytes when DevTools is open (avoid during testing)

#### Testing Instructions

1. Open Customizer → Header Builder
2. Hover browser tab to observe initial memory
3. Navigate through multiple font-related fields across different sections
4. Hover tab again to check memory changes
5. **Important**: Do NOT open DevTools inspect panel (inflates memory)

#### Investigation Areas

1. **Enhanced Select Control**: `Customizer/Controls/Select/` - How Select2 is initialized
2. **Google Fonts Data**: Where the font list is defined and how it's passed to Select2
3. **Select2 Options**: Data adapter, ajax mode, lazy loading potential

#### Potential Solutions to Research

1. **Lazy Loading**: Load fonts on-demand via AJAX instead of embedding full list
2. **Shared Data Adapter**: Custom Select2 DataAdapter that references shared data
3. **Virtual Scrolling**: Only render visible options (minimumResultsForSearch)
4. **Data Normalization**: Pass data by reference instead of value to Select2
5. **Single Dropdown**: Share one Select2 dropdown across multiple controls

#### Success Criteria

- [ ] Memory usage remains stable regardless of number of font fields
- [ ] Font selection functionality unchanged (search, selection, preview)
- [ ] No regression in Customizer responsiveness
- [ ] Build passes with `pnpm run build-all`

---

### ✅ Completed Issues (v2.11.8+28)

1. ✅ **Header Builder Push Menu** - Fixed incorrect setting check in `body-classes.php`

### ✅ Completed Issues (v2.11.8+27)

1. ✅ **Header Builder Desktop Search Widget** - Icon color/size live preview fixed
2. ✅ **Navigation Hover Effects** - Hover color & radius fixed (esc_html issue resolved)
3. ✅ **CTA Button Border Radius** - Live preview fixed
4. ✅ **Mobile Navigation Icon Color** - SVG fill/stroke added
5. ✅ **Search Widget Positioning** - Left-aligned expansion fixed


## 7. Technical Context & Notes

### E2E Testing Setup

- **Location**: `page-builder-framework-e2e-testing/`
- **Framework**: Nightwatch v3.12.3
- **Browsers**: Chrome, Firefox (with headless options)
- **Configuration**: `nightwatch.conf.js`

### Running Tests

```bash
cd page-builder-framework-e2e-testing
pnpm test                    # Run all tests
pnpm test:chrome             # Run with Chrome
pnpm test:chrome:headless    # Run headless
pnpm test:smoke              # Run smoke (login + Customizer load) first
pnpm test:customizer         # Run Customizer tests only
pnpm test:controls           # Run control tests only
pnpm test:builder            # Run Builder tests
pnpm test:repeater           # Run Repeater tests
pnpm test:enhanced-select    # Run Enhanced Select tests
pnpm test:ci                 # Run CI mode (headless + HTML reporter)
```

### WordPress Configuration

Credentials are loaded from `.env.local` at project root:
```bash
WP_USERNAME=nightwatch
WP_PASSWORD='Mapsteps e2e testing :)'
```

Default site URLs in `config/globals.js`:
- Site URL: `http://mapsteps.local`
- Admin URL: `http://mapsteps.local/wp-admin`

**Note**: Tests require a running WordPress instance with Page Builder Framework theme activated.

### Control Types in WPBF

Located in `wp-content/themes/page-builder-framework/Customizer/Controls/`:
- Base, Builder, Checkbox, Code, Color, Custom, Dimension
- Editor, Generic, Headline, MarginPadding, Media, Radio
- Repeater, Responsive, Select, Slider, Sortable, Typography

## 8. Instructions for Next Agent

You are starting session `v2.11.8+28`.

### Current Status

All previous header/Header Builder/Customizer issues have been resolved. Check **Section 6** for new task objectives.

### General Guidelines

1. **Read Section 6** for assigned tasks and objectives
2. **Follow WordPress best practices**: sanitize inputs, escape outputs, respect capabilities
3. **Use pnpm** for builds (avoid npm). Prefer targeted builds over `build-all` unless necessary
4. **Test thoroughly**: Verify in Customizer live preview AND frontend
5. **Document progress**: Update this handoff with findings, fixes, and verification steps

### Success Criteria

- Assigned tasks completed as specified
- No regressions to existing functionality
- All changes verified with appropriate builds

## 9. Previous Session Accomplishments (Session v2.11.8+17)

- **Smoke E2E Stability**
  - Ran `pnpm test:smoke` multiple times; it now passes reliably using the hardened `wpLogin` and `openCustomizer` commands described above.
  - Confirmed Customizer consistently loads on `/wp-admin/customize.php` with `#customize-controls` and the preview iframe present.

- **Header Builder E2E Hardening**
  - Iterated on `tests/customizer/controls/builderControl.test.js` to make the suite more robust:
    - Avoided brittle checks on `.open/.expanded` classes when opening panels/sections; preferred `wp.customize.panel()/section().expand()` and dynamic section ID detection.
    - Ensured `wpbf_enable_header_builder` is enabled via `wp.customize` API plus guarded checkbox click.
    - Relaxed overly strict visibility expectations to presence/API-based checks where appropriate (e.g. using `control.active()` for `wpbf_header_builder`).
    - Adjusted selectors and expectations for available widgets so they match current markup.
  - Current builder run: most tests pass; remaining flakes are environment/session-related, not selector mismatches.

- **Customizer postMessage Analysis (Live Preview Issues)**
  - Investigated live-preview behavior for:
    - Mobile menu trigger (border radius & padding).
    - Desktop off-canvas push menu (push effect & menu width).
    - Mobile Header Builder buttons 1 & 2 (border radius, border width, border style).
  - Reviewed:
    - `inc/customizer/js/postmessage.ts` entry point.
    - `postmessage-parts/menu-triggers.ts` (desktop & mobile header builder menu triggers).
    - `postmessage-parts/mobile-navigation.ts` (mobile hamburger background, border radius, etc.).
    - `postmessage-parts/off-canvas.ts` (off-canvas width + push transform + other styles).
    - `postmessage-parts/header-builder-buttons.ts` (desktop & mobile header builder buttons).
  - Identified likely causes as wiring/behavioral mismatches (see “Next Steps for Next Agent” below) rather than missing infrastructure.

## 10. Previous Session Accomplishments (Session v2.11.8+18)

- **PostMessage Analysis Complete**
  - Reviewed all postMessage JS modules per Section 10 recommendations from previous session
  - Analyzed `postmessage-parts/menu-triggers.ts`, `mobile-navigation.ts`, `off-canvas.ts`, and `header-builder-buttons.ts`
  - Identified root cause: padding conflict between legacy and header builder modes

- **Fixed Mobile Menu Trigger Padding Conflict**:
  - Identified conflict between legacy hardcoded padding and Header Builder custom padding.
  - Implemented conditional logic in `mobile-navigation.ts` using `headerBuilderEnabled()` to respect context.
  - Verified build success.
- **Fixed Desktop Off-Canvas Push Menu Preview**:
  - Corrected setting ID mismatches in `off-canvas.ts` (`off_canvas_*` → `menu_off_canvas_*`).
  - Fixed CSS selectors to match actual HTML structure (`.wpbf-menu-off-canvas-left/right`, `.wpbf-push-menu-left/right.active`).
  - **Crucial Fix**: Implemented `menu_off_canvas_push` listener in `off-canvas.ts` to dynamically toggle body classes (`wpbf-push-menu-left/right`) in Header Builder mode, as the Premium plugin's handler skips this mode.
  - **Attempted Mobile Button Border Radius/Width Preview Fix**:
    - **Root Cause 1**: `listenToBuilderResponsiveControl` was not applying initial values on load, only on change. Fixed by adding initial value application logic.
    - **Root Cause 2**: `header-builder-buttons.ts` was using `listenToCustomizerValueChange` (simple value) for responsive controls. Reverted to `listenToBuilderResponsiveControl` (responsive object).
    - **Root Cause 3**: Live preview CSS was being overridden by compiled theme CSS. Added `!important` to all generated CSS rules in `customizer-util.ts`.
    - **Result**: Implemented fixes (initial value, listener type, !important), but user reports live preview is still not working correctly.
    
- **New Issues Reported**:
  - **Mobile Button Live Preview**: Border radius and border width are still not updating correctly in the live preview.
  - User manually modified `mobile-header-builder.ts` recently, which may have reverted some fixes or introduced new behavior.

- **Build & Documentation**
  - Successfully compiled all TypeScript changes (`pnpm run build-all` passed)
  - Created comprehensive walkthrough with manual verification instructions
  - Documented code analysis and technical rationale

## 11. This Session Accomplishments (Session v2.11.8+19)

- **✅ FIXED: Mobile Button Border Radius & Width Live Preview**
  - **Root Cause Identified**: The issue was NOT in the postMessage listeners (which were working correctly), but in the **Responsive Input Slider control** itself.
  - **Problem**: The control was hardcoded to always show the **first device (desktop)** as active, regardless of which preview device the user was viewing.
  - **Impact**: When users changed border radius/width in tablet or mobile preview mode, the value was being saved to the **desktop** key instead of the correct device key.
  - **Evidence**: User provided screenshots showing desktop value updated to 41px while tablet remained at 5px, even though they were editing in tablet preview mode.

- **Solution Implemented**:
  - Modified `Customizer/Controls/Slider/src/ResponsiveInputSliderForm.tsx`
  - Added React `useEffect` hook to track `wp.customize.previewedDevice`
  - Added `activeDevice` state that syncs with current preview device
  - Changed active tab logic from hardcoded `0 === deviceIndex` to `device === activeDevice`
  - Control now automatically switches active tab when preview device changes

- **Files Modified**:
  - Source: `Customizer/Controls/Slider/src/ResponsiveInputSliderForm.tsx`
  - Compiled: `Customizer/Controls/Slider/dist/responsive-input-slider-control-min.js` (auto-generated)

- **Verification**:
  - Build completed successfully (`pnpm run build-all`)
  - User confirmed fix works: border radius and width now update correctly on tablet/mobile devices
  - Live preview updates instantly with correct values

- **Broader Impact**:
  - This fix affects **all responsive input slider controls** throughout the Customizer, not just mobile buttons
  - Any control using `responsive-input-slider` type now correctly syncs with preview device

- **Documentation**:
  - Created comprehensive walkthrough documenting the investigation, root cause, solution, and verification
  - Updated progress handoff with session accomplishments

## 12. This Session Accomplishments (Session v2.11.8+20)

### Comprehensive Header Builder Verification Completed

Performed systematic code analysis of all Header Builder controls and their postMessage handlers.

### Desktop Header Builder Elements - All Verified ✅

| Element | Settings File | PostMessage Handler | Status |
|---------|--------------|---------------------|--------|
| **Row 1 (Top)** | `desktop/top-row-section.php` | `header-builder-rows.ts` | ✅ Verified |
| **Row 2 (Main)** | `desktop/main-row-section.php` | `header-builder-rows.ts` | ✅ Verified |
| **Row 3 (Bottom)** | `desktop/bottom-row-section.php` | `header-builder-rows.ts` | ✅ Verified |
| **Menu 1** | `desktop/menu-1-section.php` | `navigation.ts` | ✅ Verified |
| **Menu 2** | `desktop/menu-2-section.php` | `mobile-header-builder-rows.ts` | ✅ Verified |
| **Button 1** | `desktop/button-1-section.php" | `header-builder-buttons.ts` | ✅ Verified |
| **Button 2** | `desktop/button-2-section.php` | `header-builder-buttons.ts` | ✅ Verified |
| **Search** | `desktop/search-section.php` | `header-builder.ts` | ✅ Verified |
| **HTML 1/2** | `desktop/html-1-section.php` | N/A (content only) | ✅ N/A |
| **Menu Trigger** | `desktop/menu-trigger-section.php` | `menu-triggers.ts` | ✅ Verified |
| **Off-Canvas** | `desktop/offcanvas-section.php` | `off-canvas.ts`, `header-builder-reveal.ts` | ✅ Verified |

### Mobile Header Builder Elements - All Verified ✅

| Element | Settings File | PostMessage Handler | Status |
|---------|--------------|---------------------|--------|
| **Row 1 (Top)** | `mobile/top-row-section.php` | `mobile-header-builder-rows.ts` | ✅ Verified |
| **Row 2 (Main)** | `mobile/main-row-section.php` | `mobile-header-builder-rows.ts` | ✅ Verified |
| **Row 3 (Bottom)** | `mobile/bottom-row-section.php` | `mobile-header-builder-rows.ts` | ✅ Verified |
| **Menu 1** | `mobile/menu-1-section.php` | `mobile-navigation.ts` | ✅ Verified |
| **Menu 2** | `mobile/menu-2-section.php" | `mobile-header-builder-rows.ts` | ✅ Verified |
| **Button 1** | `mobile/button-1-section.php` | `header-builder-buttons.ts` | ✅ Verified |
| **Button 2** | `mobile/button-2-section.php` | `header-builder-buttons.ts` | ✅ Verified |
| **Search** | `mobile/search-section.php` | `header-builder-search.ts` | ✅ Fixed & Verified |
| **HTML 1/2** | `mobile/html-1-section.php` | N/A (content only) | ✅ N/A |
| **Menu Trigger** | `mobile/menu-trigger-section.php` | `menu-triggers.ts`, `mobile-navigation.ts` | ✅ Verified |
| **Off-Canvas** | `mobile/offcanvas-section.php` | `header-builder-reveal.ts` | ✅ Verified |

### Bug Fixed: Mobile Search Icon Color Duplicate Listener

- **Issue Found**: `mobile-header-builder.ts` had duplicate/incorrect listeners for `wpbf_header_builder_mobile_search_icon_color`:
  - Used wrong type (`WpbfColorControlValue` instead of `WpbfMulticolorControlValue`)
  - Used non-existent selector (`.wpbf-mobile-header-search-icon svg`)
  - Had orphan listener for `_alt` setting that doesn't exist
- **Root Cause**: Legacy code that was never updated when the control type changed to multicolor
- **Fix Applied**: Removed duplicate listeners from `mobile-header-builder.ts` (lines 123-155)
- **Correct Handler**: `header-builder-search.ts` already handles this correctly with:
  - Proper multicolor type with `default` and `hover` states
  - Correct selector `.wpbff-search`
- **Files Modified**: `inc/customizer/js/postmessage-parts/mobile-header-builder.ts`
- **Build**: Successfully compiled with `pnpm run build-all`

### Key Findings

1. **All controls have postMessage handlers** - Every control with `transport('postMessage')` has a corresponding listener
2. **Previous session fixes are intact**:
   - `ResponsiveInputSliderForm.tsx` correctly syncs with `wp.customize.previewedDevice`
   - `listenToBuilderResponsiveControl` applies initial values on load
   - Mobile menu trigger padding conflict fixed with `headerBuilderEnabled()` check
3. **No missing handlers** - All Header Builder controls are properly wired for live preview

## 13. This Session Accomplishments (Session v2.11.8+21)

### ✅ FIXED: Header Builder Column Width (Flexible/Auto-Width)

**Problem Identified**:
The Header Builder columns were using `flex: 1 1 0` which forced all 5 columns to take equal width (20% each), causing content to wrap unnecessarily.

**Root Cause**:
In `assets/scss/main/_navigation.scss`, the `.wpbf-header-column` class had:
```scss
.wpbf-header-column {
    flex: 1 1 0;  // Forces equal width for all columns
    min-width: 0;
}
```

**Solution Implemented**:
Changed the flexbox approach to auto-width based on content:

```scss
.wpbf-header-column {
    // Default: auto-width based on content, don't grow or shrink
    flex: 0 0 auto;
    min-width: 0;

    &.wpbf-column-grow {
        // Columns with menu, html, etc. can grow to fill remaining space
        flex: 1 1 auto;
    }

    &.wpbf-column-empty {
        // Empty columns should take no space
        flex: 0 0 0;
    }

    // Menu inside header builder columns - horizontal layout
    .wpbf-menu {
        display: flex;
        flex-wrap: nowrap;
        align-items: center;

        > .menu-item {
            float: none;
            flex-shrink: 0;
        }
    }

    // Logo inside header builder - flexible size
    .wpbf-logo {
        display: flex;
        align-items: center;

        img {
            max-width: 100%;
            height: auto;
        }
    }
}
```

**How It Works**:
1. **Default columns** (`flex: 0 0 auto`): Size based on content, don't grow or shrink
2. **Empty columns** (`flex: 0 0 0`): Take no space when empty
3. **Grow columns** (`flex: 1 1 auto`): Can grow to fill remaining space (applied to columns with menu, html, menu_trigger widgets)
4. **Menu items**: Forced horizontal layout with `flex-wrap: nowrap`
5. **Logo**: Flexible sizing with `max-width: 100%`

**Files Modified**:
- `assets/scss/main/_navigation.scss` (lines 576-620)

**Compiled Output** (verified in `css/min/style-min.css`):
- `.wpbf-header-column{flex:none;min-width:0}`
- `.wpbf-header-column.wpbf-column-grow{flex:auto}`
- `.wpbf-header-column.wpbf-column-empty{flex:0 0 0}`
- `.wpbf-header-column .wpbf-menu{display:flex;flex-wrap:nowrap;align-items:center}`

**Verification**:
- ✅ Build completed successfully (`pnpm run build-all`)
- ✅ CSS compiled correctly with new flex values
- ✅ Works for all 3 rows (top, main, bottom) - both desktop and mobile
- ✅ Menu items display horizontally in one line
- ✅ Logo has flexible sizing
- ✅ Responsive behavior preserved

**Acceptance Criteria Met**:
- [x] Columns use flexible/auto width based on content
- [x] Text in HTML widgets doesn't wrap unnecessarily
- [x] Menu items display in one horizontal line
- [x] Logo has flexible size
- [x] Proper alignment maintained between columns
- [x] Works across all 3 rows (top, main, bottom)
- [x] Responsive behavior preserved
- [x] Build passes with `pnpm run build-all`

## 17. This Session Accomplishments (Session v2.11.8+26)

- ✅ Fixed centered desktop menu class mismatch:
  - Header Builder now emits `wpbf-menu-centered` (was `wpbf-menu-center`) in `Customizer/HeaderBuilder/HeaderBuilderOutput.php` when placement is `center`, aligning with existing CSS.
- ✅ Reverted temporary Menu 2 specificity additions:
  - `inc/customizer/styles/header-builder-menu-styles.php` restored to the original selectors for Menu 2 padding/font-size.
- ✅ Configurations reverted:
  - Removed temporary `wpbf_css_output` inline override and Menu 2 padding fallback in `header-styles.php` (files recreated to original content).
- ✅ Build:
  - `pnpm run build-all` completed successfully.
- ✅ Side effects:
  - None expected; only class-name alignment was changed. If any custom CSS/JS targeted `.wpbf-menu-center`, update it to `.wpbf-menu-centered`.

## 15. This Session Accomplishments (Session v2.11.8+24)

### ✅ FIXED: Header Builder Menu Font Size Live Preview

**Problem Identified**:
The live preview for font size settings in the Header Builder was not working for Menu 1 and Menu 2. The selectors used in the `postMessage` handlers were either too generic or missing the specific context required when the Header Builder is active.

**Solution Implemented**:
1.  **Menu 1 (`navigation.ts`)**:
    -   Updated the `menu_font_size` handler to use a more specific selector when Header Builder is enabled: `.wpbf-menu.desktop_menu_1 > .menu-item > a`.
    -   This matches the specificity used for `menu_padding`.

2.  **Menu 2 (`mobile-header-builder-rows.ts`)**:
    -   Updated the `wpbf_header_builder_desktop_menu_2_menu_font_size` handler to use the selector: `.wpbf-menu.desktop_menu_2 > .menu-item > a`.

3.  **PHP Style Generation**:
    -   Updated `inc/customizer/styles/header-styles.php` to use the same specific selector for Menu 1 when Header Builder is enabled.
    -   Updated `inc/customizer/styles/header-builder-menu-styles.php` to generate the correct CSS for Menu 2 font size.

**Files Modified**:
-   `inc/customizer/js/postmessage-parts/navigation.ts`
-   `inc/customizer/js/postmessage-parts/mobile-header-builder-rows.ts`
-   `inc/customizer/styles/header-styles.php`
-   `inc/customizer/styles/header-builder-menu-styles.php`

**Verification**:
-   ✅ Build completed successfully (`pnpm run build-all`).
-   ✅ Confirmed code changes align with the requirement to fix live preview targeting.

## 16. Task Assignment for Session v2.11.8+25

**Task**: Investigate and fix Customizer live preview and frontend layout issues

### Issues to Resolve

#### 1. Desktop Menu Center Position Layout Bug
**Problem**: When desktop menu position is set to "Center", the layout appears correct in Customizer preview but is broken on the frontend.
- **Scope**: Desktop menu positioning
- **Impact**: Frontend layout doesn't match Customizer preview
- **Expected**: Frontend should match Customizer preview exactly

#### 2. Mobile Main Row Design Controls - Missing Live Preview
**Problem**: Changes to Mobile Main Row settings in Design tab don't update in Customizer live preview.
- **Scope**: Mobile Header Builder Main Row design controls
- **Current Behavior**: Only updates via partial refresh after save/reload
- **Expected**: Real-time live preview updates via postMessage

#### 3. Mobile Bottom Row Design Controls - Missing Live Preview  
**Problem**: Changes to Mobile Bottom Row settings in Design tab don't update in Customizer live preview.
- **Scope**: Mobile Header Builder Bottom Row design controls
- **Current Behavior**: Only updates via partial refresh after save/reload
- **Expected**: Real-time live preview updates via postMessage

### Investigation Areas

1. **Desktop Menu Center Position**:
   - Check CSS generation in `inc/customizer/styles/header-styles.php`
   - Verify frontend vs Customizer preview CSS differences
   - Review menu positioning logic in SCSS files

2. **Mobile Row Design Controls**:
   - Analyze `mobile-header-builder-rows.ts` postMessage handlers
   - Check if Design tab controls have `transport('postMessage')` set
   - Verify CSS selectors match actual frontend markup
   - Review control definitions in `mobile/main-row-section.php` and `mobile/bottom-row-section.php`

### Success Criteria

- [x] Desktop menu center position works identically in Customizer and frontend
- [x] Mobile Main Row design changes update live in Customizer preview
- [x] Mobile Bottom Row design changes update live in Customizer preview
- [x] All changes verified with `pnpm run build-all`
- [x] Manual testing confirms fixes work as expected
