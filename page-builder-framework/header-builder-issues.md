ISSUE #1: Inconsistent spacing between header widgets in the same column/slot

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


ISSUE #2: Poor visual spacing in `margin-padding` unit controls

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


ISSUE #3: Search widget UX and behavior in Header Builder

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
