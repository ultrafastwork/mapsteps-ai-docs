# Technical Issues Backlog (Extracted from Support Tickets)

This document contains actionable **technical issues requiring code fixes**, analyzed and extracted from support tickets in `ai-docs/support-tickets.md`.

---

## 📌 Issues Overview Matrix

| # | Title | Status | Priority | Target File(s) |
|---|---|---|---|---|
| 1 | WebP Image Support Missing in Login Customizer Sanitizer | `[x] Completed` | High | [`class-content-helper.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard/helpers/class-content-helper.php#L35-L66) |
| 2 | Elementor Theme Builder Compatibility & Access Denied Error | `[x] Completed` | High | [`class-admin-menu-output.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/class-admin-menu-output.php) |
| 3 | Admin Menu Hover Color Overridden by Elementor's CSS | `[ ] Open` | Medium | [`admin-styles-default.css.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/branding/inc/admin-styles-default.css.php) |
| 4 | Elementor & Element Pack Menus Bypassing Hide Settings | `[x] Completed` | Medium | [`class-admin-menu-output.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/class-admin-menu-output.php) |
| 5 | Admin Bar Visibility Settings Not Applying to Non-Admin Roles | `[ ] Open` | Medium | [`class-admin-bar-helper.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard/helpers/class-admin-bar-helper.php#L39-L72) |
| 6 | Custom Submenu Access Denied for Non-Admin Roles | `[ ] Open` | Medium | [`class-admin-menu-output.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/class-admin-menu-output.php) |

---

## 🛠️ Technical Issues Backlog

### 1. WebP Image Support Missing in Login Customizer Sanitizer
* **Status:** `[x] Completed ✅`
* **Severity/Priority:** High (Confirmed Bug / Quick Fix)
* **Source:** Ticket #7 (Part 1)
* **Target Files:** [`wp-content/plugins/ultimate-dashboard/helpers/class-content-helper.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard/helpers/class-content-helper.php#L35-L66)
* **Target Symbols:** `Udb\Helpers\Content_Helper::sanitize_image()`

#### 📋 Description & Root Cause
- **Symptom:** Selecting a `.webp` image for the Login Customizer background previews correctly, but saving the customizer wipes out the `udb_login['bg_image']` setting, resetting it to empty.
- **Root Cause:** `sanitize_image()` in `class-content-helper.php` checks against a MIME type whitelist that does not include `'webp' => 'image/webp'`.

#### 🛠️ Action Items
- [x] Add `'webp' => 'image/webp'` and `'avif' => 'image/avif'` to the base `$mimes` whitelist and dynamically merge site-allowed image MIME types inside `Content_Helper::sanitize_image()`.
- [x] Test saving a `.webp` background image in the Login Customizer.

#### ✅ Acceptance Criteria & Verification
- [x] `.webp` file URLs remain saved in `udb_login['bg_image']` option after saving in WP Customizer.
- [x] Login screen renders the `.webp` background image properly without fallback to empty string.

---

### 2. Elementor Theme Builder Compatibility & Access Denied Error
* **Status:** `[x] Completed ✅`
* **Severity/Priority:** High (Critical Compatibility Bug)
* **Source:** Tickets #3, #5, #6
* **Target Files:** 
  - [`wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/class-admin-menu-output.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/class-admin-menu-output.php)
  - [`wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/ajax/class-save-menu.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/ajax/class-save-menu.php)
* **Target Symbols:** `UdbPro\AdminMenu\Admin_Menu_Output`

#### 📋 Description & Root Cause
- **Symptom:** When Ultimate Dashboard PRO is active and Elementor menu items are customized or moved via Admin Menu Editor, accessing Elementor's Theme Builder triggers "Sorry, you are not allowed to access this page" or crashes the page even for Administrator users.
- **Root Cause:** Elementor dynamically registers Theme Builder submenus and routes with hash parameters (`admin.php?page=elementor-app#/site-editor`). Re-ordering, renaming, or hiding menu items altered `$submenu` structures and stripped original parent slug capabilities required by WP core's `$_parent_pages` permission validation.

#### 🛠️ Action Items
- [x] Inspect UDB Admin Menu Editor hook execution when processing dynamic menu structures like Elementor Theme Builder.
- [x] Preserve original capability callbacks, parent menu slugs, and query parameters for Elementor Theme Builder routes.
- [x] Ensure menu modifications do not corrupt dynamic submenu registrations from Elementor.

#### ✅ Acceptance Criteria & Verification
- [x] Navigating to Elementor -> Theme Builder works without "Access Denied" error when Admin Menu Editor module is enabled.
- [x] Saving custom menu order retains Elementor Theme Builder capabilities for Admin users.

---

### 3. Admin Menu Hover Color Overridden by Elementor's Sidebar Navigation CSS
* **Status:** `[ ] Open (Not Fixed) ❌`
* **Severity/Priority:** Medium
* **Source:** Ticket #7 (Part 2)
* **Target Files:** 
  - [`wp-content/plugins/ultimate-dashboard-pro/modules/branding/inc/admin-styles-default.css.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/branding/inc/admin-styles-default.css.php)
  - [`wp-content/plugins/ultimate-dashboard-pro/modules/branding/inc/admin-styles-modern.css.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/branding/inc/admin-styles-modern.css.php)
* **Target Symbols:** `#adminmenu li.menu-top:hover` CSS rules generator

#### 📋 Description & Root Cause
- **Symptom:** On Elementor admin screens, Elementor appends body class `.e-has-sidebar-navigation` which injects a CSS rule setting admin menu hover background to `transparent`. This overrides UDB's custom admin menu hover color.
- **Root Cause:** Elementor's CSS rule (`.e-has-sidebar-navigation #adminmenu li.menu-top:hover { background: transparent; }`) has higher CSS specificity than UDB's generated admin menu styles.

#### 🛠️ Action Items
- [ ] Increase specificity of UDB's generated admin menu hover CSS selectors (e.g., target `body.e-has-sidebar-navigation #adminmenu li.menu-top:hover` or add higher specificity rules).
- [ ] Ensure UDB admin menu styles take precedence regardless of third-party body classes.

#### ✅ Acceptance Criteria & Verification
- [ ] Custom menu hover color set in UDB Branding options is visibly applied on Elementor edit/settings pages.
- [ ] Hover background does not fallback to `transparent` on pages with `.e-has-sidebar-navigation` body class.

---

### 4. Elementor & Element Pack Menus Bypassing Hide Settings
* **Status:** `[x] Completed ✅`
* **Severity/Priority:** Medium
* **Source:** Ticket #2
* **Target Files:** 
  - [`wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/class-admin-menu-output.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/class-admin-menu-output.php)
* **Target Symbols:** Admin menu output filter priorities

#### 📋 Description & Root Cause
- **Symptom:** Hidden menu items for Elementor and Element Pack (by BDThemes) periodically re-appear on the WordPress admin sidebar menu despite being hidden in UDB.
- **Root Cause:** Third-party plugins re-inject or register admin menu items dynamically at late execution priorities (e.g., after standard `admin_menu` hooks), bypassing UDB's initial menu hiding filters.

#### 🛠️ Action Items
- [x] Lower the execution priority (run later) for UDB's admin menu filtering hooks (e.g., priority `99999` on `admin_menu` or late `admin_init`).
- [x] Add dynamic suppression/filtering during `parent_file` or `admin_head` if menu items are re-added late in the load cycle.

#### ✅ Acceptance Criteria & Verification
- [x] Hidden menu items for Elementor and Element Pack remain hidden regardless of plugin execution order.

---

### 5. Admin Bar Visibility Settings Not Applying to Non-Admin Roles
* **Status:** `[ ] Open (Not Fixed) ❌`
* **Severity/Priority:** Medium
* **Source:** Ticket #4
* **Target Files:** 
  - [`wp-content/plugins/ultimate-dashboard/helpers/class-admin-bar-helper.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard/helpers/class-admin-bar-helper.php#L39-L72)
  - [`wp-content/plugins/ultimate-dashboard/modules/setting/class-setting-output.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard/modules/setting/class-setting-output.php)
* **Target Symbols:** `Udb\Helpers\Admin_Bar_Helper::should_remove_admin_bar()`

#### 📋 Description & Root Cause
- **Symptom:** Configuring admin bar visibility settings to hide the admin bar for specific user roles (e.g., Editor, Author) does not hide the bar; it remains visible for those roles.
- **Root Cause:** Role evaluation logic in `Admin_Bar_Helper::should_remove_admin_bar()` fails to accurately evaluate user roles for multi-role or non-administrator users, or `show_admin_bar(false)` hook execution occurs after standard render initialization.

#### 🛠️ Action Items
- [ ] Audit `show_admin_bar` hook implementation and role verification in `Admin_Bar_Helper::should_remove_admin_bar()`.
- [ ] Ensure role checking accounts for custom and standard roles accurately and executes early enough on `init` or `wp_loaded`.

#### ✅ Acceptance Criteria & Verification
- [ ] Admin bar is hidden on frontend and backend for non-admin users matching configured role rules.
- [ ] Administrator users retain admin bar access when configured to only affect non-admin roles.

---

### 6. Custom Plugin Submenu Permission / Access Denied for Non-Admin User Roles
* **Status:** `[ ] Open (Not Fixed) ❌`
* **Severity/Priority:** Medium
* **Source:** Ticket #1
* **Target Files:** 
  - [`wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/class-admin-menu-output.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/class-admin-menu-output.php)
  - [`wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/ajax/class-save-menu.php`](file:///d:/projects/mapsteps/wp-content/plugins/ultimate-dashboard-pro/modules/admin-menu/ajax/class-save-menu.php)
* **Target Symbols:** `UdbPro\AdminMenu\Admin_Menu_Output`

#### 📋 Description & Root Cause
- **Symptom:** When a custom link to a third-party plugin page (e.g., SSW Quotes) is added via Menu Editor for a non-admin role (e.g., "Shop Manager"), clicking the menu link produces "Sorry, you are not allowed to access this page."
- **Root Cause:** The underlying target page requires specific capabilities (e.g., `manage_options`) that the target user role lacks, or UDB's custom menu link generator does not map required target capabilities for custom menu items.

#### 🛠️ Action Items
- [ ] Review how UDB handles capability checks when custom admin links or modified menu items are rendered for non-administrator user roles.
- [ ] Expose capability configuration options in the Admin Menu Editor or ensure custom link wrappers validate target capability requirements properly.

#### ✅ Acceptance Criteria & Verification
- [ ] Custom menu items configured for non-admin roles load target pages without "Access Denied" permissions error.
- [ ] Role capabilities are preserved or explicitly grant required permissions for configured menu items.
