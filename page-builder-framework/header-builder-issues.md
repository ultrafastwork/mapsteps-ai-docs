ISSUE #1: Inconsistent spacing between header widgets in the same column/slot [OPEN]

Context:
- Header Builder
- Widgets placed inside the same column/slot (Menu, Button, Search, HTML)

Current Behavior:
1. When a Menu widget and a Button widget are placed next to each other:
   - Spacing exists between them (expected).
2. When a Search widget or HTML widget is placed after a Button:
   - The Search/HTML widget touches the Button.
3. Button widgets have Margin controls (`margin-padding` type) under the Design tab.
4. Search widgets have Margin controls, but no Design tab (controls are in the main section).
5. HTML and Menu widgets **currently lack Margin controls** in their respective sections (e.g., `wpbf_header_builder_desktop_html_1_section`, `wpbf_header_builder_desktop_menu_1_section`).

Problem:
- Spacing is inconsistent because some widgets (Button, Search) have Margin controls while others (HTML, Menu) do not.
- Even when Margin controls exist, they are not always intuitively placed or discovered by users.
- Default layout appears broken (widgets touching) because there is no default "gap" or consistent margin implementation across all header widgets.

Constraints / Considerations:
- Default spacing on every widget may be conceptually wrong if the user wants them touching.
- Solution should improve usability and consistency without forcing fixed spacing.

Open Questions / Solution Exploration:
- Should all header widgets (HTML, Menu, etc.) have a consistent "Design" tab with Margin controls?
- Should the system provide better affordances instead of default spacing?
- Should newly added widgets automatically expose spacing (Margin) controls?
- Should widget settings (Customizer sections) auto-open when a widget is added to the header builder?
- Check whether auto-opening widget settings is already implemented in the `responsive-builder` control.

Expected Outcome:
- Consistent availability of Margin controls across ALL header widgets.
- Improve discoverability of Margin controls.
- Reduce user confusion when widgets touch by default.


ISSUE #2: Poor visual spacing in `margin-padding` unit controls [RESOLVED]

Context:
- `margin-padding` controls
- Includes responsive margin/padding controls

Current Behavior:
- Excessive horizontal distance between:
  - Numeric input fields
  - Unit selectors (px, %, em, etc.)

Problem:
- Control layout looks visually unpolished in the Customizer.
- Large spacing reduces UI clarity and compactness.

Expected Outcome:
- Reduce unnecessary spacing between inputs and units.
- Improve alignment and visual consistency within the `margin-padding` control type.
- Apply changes consistently across all Margin/Padding controls.


ISSUE #3: Search widget UX and behavior in Header Builder [OPEN]

Context:
- Header Builder
- Search widget (`wpbf_header_builder_desktop_search_section`) placed next to Menu widget

Clarification:
- The Search widget already includes Margin controls (id: `wpbf_header_builder_desktop_search_margin`).
- Users can manually adjust spacing to prevent icon collisions.

Current Behavior:
1. When clicking the Search icon:
   - Input expands (expected).
   - During expansion, the search icon visually shifts, creating a jarring effect.
2. When typing in the expanded input:
   - A browser-provided clear (X) button appears.
   - The search icon remains visible.
   - Result: two icons touch visually.
3. Hover behavior:
   - Menu items use smooth color transition animations.
   - Search icon hover effect (from `multicolor` control) is abrupt and not CSS-animated.

Problem:
- While spacing can be fixed manually via the Margin control, the default UX feels unpolished.
- Users may not realize Margin controls exist.
- Visual behavior (hover/transitions) is inconsistent with Menu items.

Open Questions / Solution Exploration:
- Should widget settings automatically open when a widget is added to the builder?
- Check if auto-open behavior already exists in `setup-builder-control.ts` or similar:
  - If yes, evaluate whether Margin controls are sufficiently visible.
  - If no, consider implementing auto-open for better onboarding.
- Should the browser clear (X) button be hidden (`::-webkit-search-cancel-button`) when the search is expanded?
- Should the search icon share the same transition duration and easing as menu items?
- Should additional styling controls be provided for the expanded search input?
  - Border color, width, and radius (currently only Icon Size and Color exist).

Expected Outcome:
- Smoother, more stable search expansion behavior.
- No visual collision between icons by default.
- Better alignment with menu animation behavior.
- Improved user guidance without removing manual control.


ISSUE #4: Logo width settings have no live preview on mobile/tablet views [RESOLVED v2.11.9+11]

Context:
- Header Builder & Legacy Header
- Logo section (`title_tagline`), setting: `menu_logo_size`
- Control type: `responsive-input-slider` with `postMessage` transport

Current Behavior:
1. The `menu_logo_size` setting is a responsive control with desktop/tablet/mobile values.
2. The postMessage handler in `inc/customizer/js/postmessage-parts/logo.ts` uses `writeResponsiveCSSMultiSelector` to write CSS with media queries for tablet (`@media (max-width: {desktop-1}px)`) and mobile (`@media (max-width: {tablet-1}px)`).
3. When the user switches the Customizer to tablet or mobile preview, the preview iframe resizes visually but the iframe's actual viewport width may not shrink below the media query breakpoints.
4. As a result, changing the tablet or mobile logo width value produces no visible live preview — the CSS is written correctly but the media queries don't activate inside the preview iframe.

Problem:
- Desktop logo width live preview works fine (no media query wrapper).
- Tablet and mobile logo width changes show no visual feedback until the user publishes and views the site at actual device widths.
- The same `writeResponsiveCSSMultiSelector` approach is used in `header-styles.php` for server-side rendering (which works correctly on the frontend), so the issue is isolated to the Customizer live preview.

Relevant Files:
- `inc/customizer/settings/header/logo.php` — defines `menu_logo_size` (line ~38-57)
- `inc/customizer/js/postmessage-parts/logo.ts` — postMessage handler using `writeResponsiveCSSMultiSelector` (line ~16-35)
- `inc/customizer/js/customizer-util.ts` — `writeResponsiveCSSMultiSelector` function (line ~411) and `mediaQueries` definition (line ~5-14)
- `inc/customizer/styles/header-styles.php` — server-side CSS output for logo width (line ~143-185)

Open Questions / Solution Exploration:
- Should the postMessage handler detect the currently previewed device (via `wp.customize.previewedDevice`) and write CSS without media query wrappers for the active device?
- Should the responsive control emit per-device change events that write non-media-query CSS when that device is being previewed?
- Check if other responsive controls (e.g., tagline font size, layout padding) have the same issue.

Expected Outcome:
- Changing logo width for tablet or mobile in the Customizer should produce immediate visual feedback in the preview iframe.


ISSUE #5: SVG hamburger icon and text label are visually misaligned in Menu Trigger widget [RESOLVED v2.11.9+10, refined v2.11.9+14]

Context:
- Header Builder
- Menu Trigger widget (both desktop and mobile)
- SVG icon variants (`variant-1`, `variant-2`, `variant-3`) — NOT the `wpbff` icon font version

Current Behavior:
1. The menu trigger button renders an SVG icon followed by a text label (`<span class="menu-trigger-button-text">`).
2. The SVG icons use `width="1em" height="1em"` sizing (in `HeaderBuilderConfig::menuTriggerButtonSvg()`).
3. The button uses `display: inline-flex; align-items: center; column-gap: 3px;` (in `_navigation.scss`, line ~372-375).
4. Despite `align-items: center`, the SVG icon and text label appear visually misaligned — the icon sits at a different vertical position than the text.

Problem:
- The SVG's `viewBox="0 0 32 28"` has the hamburger bars starting at `y="4"` with the last bar ending at `y="23"`, leaving uneven whitespace within the viewBox. This internal padding causes the SVG to not visually center with adjacent text even though the flex container aligns their bounding boxes.
- The `1em` sizing ties the SVG dimensions to `font-size`, but the visual content within the SVG doesn't fill the viewBox evenly, creating a perceived offset.
- The `column-gap: 3px` is quite small and may not provide enough visual separation.

Relevant Files:
- `Customizer/HeaderBuilder/HeaderBuilderConfig.php` — `menuTriggerButtonSvg()` method (line ~309-338), SVG viewBox and rect positions
- `Customizer/HeaderBuilder/HeaderBuilderOutput.php` — `render_menu_trigger_button_widget()` (line ~658-731), HTML structure
- `assets/scss/main/_navigation.scss` — `.use-header-builder .wpbf-menu-toggle` flex styles (line ~370-376)

Open Questions / Solution Exploration:
- Should the SVG viewBox be adjusted so the visual content is vertically centered with minimal internal padding?
- Should the SVG use `vertical-align` or a negative margin to compensate for the viewBox offset?
- Should the `column-gap` between icon and text be increased for better visual separation?
- Check if the issue also affects the Customizer radio-buttonset previews (which use different SVG dimensions: `width="18" height="14" viewBox="0 0 18 14"`).

Expected Outcome:
- The SVG hamburger icon and text label should appear visually aligned on the same baseline/center.
- Consistent alignment across all three SVG variants.


ISSUE #6: Menu Trigger "Style" setting should be under the "Design" tab [RESOLVED v2.11.9+09]

Context:
- Header Builder
- Menu Trigger widget sections (both desktop and mobile)
- Desktop: `wpbf_header_builder_desktop_menu_trigger_section`
- Mobile: `wpbf_header_builder_mobile_menu_trigger_section`

Current Behavior:
1. The Menu Trigger section has two tabs: "General" and "Design".
2. The "Style" radio-buttonset control (`_style`) with options Simple/Outlined/Solid is currently placed under the "General" tab (`->tab('general')`).
3. The "Design" tab contains: Button Settings (padding, background/border color, border radius) and Icon Settings (icon color, icon size) — all of which are conditional on the Style selection.

Problem:
- The "Style" control determines the visual appearance of the menu trigger button (simple vs outlined vs solid). This is a design/styling concern, not a general/content concern.
- Placing it in the "General" tab separates it from its dependent controls in the "Design" tab, making the UX less intuitive.
- Users must switch between tabs to understand the relationship between Style and its dependent design controls.
- Other header builder widgets (e.g., Button 1/2) should be checked for consistency in tab placement of similar style controls.

Relevant Files:
- `inc/customizer/settings/header-builder/desktop/menu-trigger-section.php` — Style control at line ~92-103, placed in `->tab('general')`
- `inc/customizer/settings/header-builder/mobile/menu-trigger-section.php` — Style control at line ~93-105, placed in `->tab('general')`

Expected Outcome:
- Move the "Style" radio-buttonset control to the "Design" tab in both desktop and mobile menu trigger sections.
- Ensure dependent controls (padding, colors, border radius) remain logically grouped with the Style control.
- Review other widget sections for similar tab placement inconsistencies.


ISSUE #7: Mobile Menu Trigger Padding postMessage conflict [RESOLVED v2.11.9+13]

Context:
- Header Builder
- Menu Trigger widget (mobile), padding setting
- `mobile_menu_trigger_padding` postMessage handler in `menu-triggers.ts`
- Conflicting logic in `mobile-navigation.ts`

Problem:
- `mobile-navigation.ts` contained logic that hardcoded `padding: 10px !important` on `.wpbf-mobile-menu-toggle` when Header Builder was enabled and style was solid/outline.
- The `wpbf_header_builder_mobile_menu_trigger_style` listener also forced `padding: 10px !important` or `padding: 0`, overriding user-defined padding.
- This prevented `menu-triggers.ts` from applying the user's custom padding values in the live preview.

Solution:
1. Removed `padding: "unset"` from the "simple" style reset block in `mobile_menu_hamburger_bg_color` listener.
2. Removed the `else` block that forced `padding: "10px !important"` for solid/outline.
3. Removed the entire `wpbf_header_builder_mobile_menu_trigger_style` listener that hardcoded padding.
4. `menu-triggers.ts` is now the sole controller for menu trigger padding in Header Builder mode.

Relevant Files:
- `inc/customizer/js/postmessage-parts/mobile-navigation.ts`
- `inc/customizer/js/postmessage-parts/menu-triggers.ts`


ISSUE #8: Duplicate postMessage listener for mobile header builder row 1 vertical padding [RESOLVED v2.11.9+12]

Context:
- Header Builder
- Mobile Header Builder rows
- `wpbf_header_builder_mobile_row_1_vertical_padding` setting

Problem:
- `mobile-header-builder-rows.ts` contained a duplicate `listenToCustomizerValueChange` call for the `wpbf_header_builder_mobile_row_1_vertical_padding` setting.
- This caused the style writing logic to execute twice for every value change, potentially leading to conflicts or redundant DOM operations.

Solution:
- Removed the redundant event listener block, keeping only one unique listener for the setting.

Relevant Files:
- `inc/customizer/js/postmessage-parts/mobile-header-builder-rows.ts`
