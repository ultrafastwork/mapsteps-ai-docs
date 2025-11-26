# Progress Handoff

**Date**: 2025-11-26
**Status**: Active
**Current Session**: v2.11.8+17

## 1. High-Level Summary

**Nightwatch v3 E2E testing suite has been significantly expanded** with Builder, Repeater, and Enhanced Select control tests, plus CI/CD integration. The test suite now includes:

- Nightwatch v3 configuration for WordPress Customizer testing
- Custom commands for WordPress login and Customizer interactions
- Custom assertions for control validation
- Page objects for Customizer and login pages
- Basic control tests (text, checkbox, select, slider, color)
- WPBF-specific control tests (Typography, MarginPadding, Responsive)
- **NEW: Builder Control Tests** - Header Builder drag-and-drop, widget placement, responsive views
- **NEW: Repeater Control Tests** - Add/remove/reorder rows, field types, expand/collapse
- **NEW: Enhanced Select Tests** - Select2 dropdowns, search, multi-select, keyboard navigation
- **NEW: GitHub Actions CI/CD Workflow** - Automated testing with Chrome/Firefox
- Control dependency tests with documented WPBF dependencies
- Preview update tests for postMessage and refresh transport modes
- Comprehensive documentation with control dependency mappings

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

### Additional Test Coverage

1. **Customizer Navigation Stability**:
   - Fix issue where Chrome remains on `data:,` and `#customize-controls` never appears.
   - Verify logs from `wpLogin` and `openCustomizer` (URL, redirects) and ensure post-login navigation to Customizer.
   - Add a minimal sanity test: assert `#wpadminbar`, then `#customize-controls`.

2. **Header Builder Coverage**:
   - Validate `wpbf_enable_header_builder` toggles visibility of `wpbf_header_builder`.
   - Assert builder rows/columns and widget drag/drop across desktop/mobile.


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

You are starting session `v2.11.8+17`.

### Task Steps

1. **Focus: Header Builder**
   - Add robust tests for enabling/disabling Header Builder (`wpbf_enable_header_builder`).
   - Interact with Header Builder rows/columns, add/move/remove widgets, and test responsive device switcher.
   - Assert panel visibility toggles and builder state changes (e.g., presence of `.wpbf-builder-panel`, widgets in active areas).
2. **Verify Test Suite Locally**
   - Run targeted suite while iterating:
     - `pnpm test:builder`
3. **CI/CD (Manual Only for Now)**
   - CI workflow triggers are disabled (manual `workflow_dispatch` only) to prioritize local development.
   - When ready, consider adding seeded data and visual regression.
6. **Documentation**
   - Keep README and this handoff updated with Header Builder test patterns.

### Important Notes

- Tests are in `d:/www/mapsteps/page-builder-framework-e2e-testing/`
- Update WordPress credentials in `config/globals.js` if needed
- Use custom commands for common operations
- Follow existing test patterns in `tests/customizer/controls/`
- See README.md for WPBF control types and dependency documentation
- CI/CD workflow is in `.github/workflows/e2e-tests.yml`
