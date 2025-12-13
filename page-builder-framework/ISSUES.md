### Bugfixing works:
- [x] The Font Size setting in the second row does not update in the live preview, though it applies after saving — and incorrectly affects the third row as well. *(Fixed in v2.11.8+23)*
- [x] The default Button Size field appears empty instead of showing a default value. *(Fixed in v2.11.8+24)*
- [x] The WYSIWYG editor in the HTML 2 Widget is too simple, make it to have same amount of toolbar items like in HTML 1 Widget. *(Fixed in v2.11.8+25)*
- [x] The Button Widget is automatically centered across all desktop row layouts, even when it should follow row alignment. *(Fixed in v2.11.8+26)*
- [x] In desktop mode with only Logo + Menu widgets (logo left, menu right), the logo appears visually stuck to the left regardless of column placement. The markup is correct, but right-side widgets with `wpbf-column-grow` stretch full width, pushing left content to the edge. *(Partially fixed in v2.11.8+27)*
- [x] Logo not visually centered when using mixed widget types: Button 1 (left) + Logo (center) + Menu 2 (right). The logo appears off-center because columns with `wpbf-column-grow` (menu) take more space than non-grow columns (button). Works correctly when both left and right columns have grow widgets (e.g., Menu 1 + Logo + Menu 2). *(Fixed in v2.11.8+28)*
- [ ] Mobile widget positioning breaks due to flex: auto applied on the selector: `.wpbf-header-column.wpbf-column-grow.`
- [ ] Widget positioning on desktop is currently unstable and behaves inconsistently.
- [ ] The default layout applied when adding a widget to a row is visually poor — consider using improved presets or more suitable default values.


### Heavy works:
- [ ] Move the “Premium” and “Theme Settings” options into the Desktop Menu section.
- [ ] Hide the “Menu Items Spacing” control when the selected menu type does not support spacing.
- [ ] Enabling “Main Row Sticky Header” should automatically hide the Top Row sticky toggle/checkbox.
- [ ] “Top Row Sticky Header” should function as a single toggle, inheriting its behavior from the main row sticky settings.
- [ ] Sticky navigation is currently not functioning at all.
