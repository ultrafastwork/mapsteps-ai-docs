# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Date**: 2026-03-19
**Last Completed Session**: v2.11.8+89
**Current Session**: v2.11.8+90
**Status**: ✅ COMPLETED

**Objective**: Answer the questions below about `desktop_menu_trigger` and `mobile_menu_trigger` widgets in Header Builder through deep codebase analysis.

---

## ✅ COMPLETED: Questions Answered (v2.11.8+89)

All questions have been answered with detailed code evidence. See `PROGRESS_HANDOFF.md` for the summary.

### Q1: Are desktop and mobile menu_trigger using the same setting fields?
**NO** — They use different setting IDs but similar field types.

### Q2: Are they partially using the same?
**YES** — Hybrid approach:
- **Shared (different IDs)**: icon, text, style, padding, margin
- **Mobile reuses legacy**: icon_color, icon_size, bg_color, border_radius use `mobile_menu_hamburger_*` controls

### Q3: Do frontend rendering/styles share the same setting fields?
**NO for setting IDs, YES for rendering logic** — Both use `render_menu_trigger_button_widget()` with device parameter. CSS output uses conditional setting IDs.

### Q4: What happens in classic mode?
- **Mobile**: Uses legacy controls in original section (not moved)
- **Desktop**: No menu trigger; uses traditional layouts or premium off-canvas
- **Guards**: postMessage handlers check `headerBuilderEnabled()` to prevent conflicts

### Q5: Any bugs or inconsistencies?
**No obvious bugs** — Guards work correctly. Minor concerns:
- Cross-dependency between legacy and new controls
- Inconsistent control locations (PHP-defined vs JS-moved)

---

## Background

The Header Builder feature (enabled via `wpbf_enable_header_builder` control) provides desktop and mobile modes with draggable widgets. The `desktop_menu_trigger` and `mobile_menu_trigger` widgets open connected customizer sections when clicked.

---

## Reference Material (Starting Context)

**NOTE: This section provides initial context to help you start. You must still perform your own deep analysis to answer the questions above with full evidence and code references.**

### Initial Findings (Verify and Expand)

#### Shared Settings (same field types, different setting IDs)

| Setting | Desktop | Mobile |
|---------|---------|--------|
| Icon | `wpbf_header_builder_desktop_menu_trigger_icon` | `wpbf_header_builder_mobile_menu_trigger_icon` |
| Label | `wpbf_header_builder_desktop_menu_trigger_text` | `wpbf_header_builder_mobile_menu_trigger_text` |
| Style | `wpbf_header_builder_desktop_menu_trigger_style` | `wpbf_header_builder_mobile_menu_trigger_style` |
| Padding | `wpbf_header_builder_desktop_menu_trigger_padding` | `wpbf_header_builder_mobile_menu_trigger_padding` |
| Margin | `wpbf_header_builder_desktop_menu_trigger_margin` | `wpbf_header_builder_mobile_menu_trigger_margin` |

#### Different Settings (mobile reuses legacy controls)

| Setting | Desktop (new) | Mobile (legacy, moved) |
|---------|---------------|------------------------|
| Icon Color | `wpbf_header_builder_desktop_menu_trigger_icon_color` | `mobile_menu_hamburger_color` |
| Icon Size | `wpbf_header_builder_desktop_menu_trigger_icon_size` | `mobile_menu_hamburger_size` |
| BG/Border Color | `wpbf_header_builder_desktop_menu_trigger_bg_color` | `mobile_menu_hamburger_bg_color` |
| Border Radius | `wpbf_header_builder_desktop_menu_trigger_border_radius` | `mobile_menu_hamburger_border_radius` |

### Key Architecture

1. **Mobile reuses legacy controls**: The mobile menu trigger reuses controls from `wpbf_mobile_menu_options` section that existed before header builder was introduced.

2. **Controls movement**: When header builder is enabled, legacy controls are moved via `setup-controls-movement.ts` from `wpbf_mobile_menu_options` to `wpbf_header_builder_mobile_menu_trigger_section`.

3. **Desktop has dedicated controls**: Desktop menu trigger has its own controls defined in `inc/customizer/settings/header-builder/desktop/menu-trigger-section.php`.

4. **Shared rendering**: Both use `HeaderBuilderOutput::render_menu_trigger_button_widget()` with device parameter.

5. **Shared postMessage handlers**: `menu-triggers.ts` handles both devices with parameterized functions.

6. **CSS output**: `header-builder-menu-styles.php` conditionally uses different setting IDs based on device.

### Behavior When Header Builder is Disabled (Classic Mode)

When `wpbf_enable_header_builder` is **false**:

1. **Desktop menu trigger**: Not available. Desktop uses traditional menu layouts (horizontal menu, off-canvas via premium plugin, etc.).

2. **Mobile menu trigger**: Uses the legacy `mobile_menu_hamburger_*` controls in their original section (`wpbf_mobile_menu_options`). These controls are NOT moved.

3. **CSS output**: `header-styles.php` handles mobile hamburger styling using the legacy control values directly.

4. **postMessage handlers**: `mobile-navigation.ts` handles the legacy controls. The `menu-triggers.ts` handlers check `headerBuilderEnabled()` and skip execution when disabled to avoid conflicts.

5. **Premium plugin**: When header builder is disabled, the premium plugin's off-canvas menu feature uses its own controls (`menu_off_canvas_hamburger_color`, `menu_off_canvas_hamburger_size`, etc.) for the desktop off-canvas trigger, handled in `off-canvas-menu-styles.php`.

### Relevant Files

- `inc/customizer/settings/header-builder/desktop/menu-trigger-section.php` — Desktop controls
- `inc/customizer/settings/header-builder/mobile/menu-trigger-section.php` — Mobile controls (partial, reuses legacy)
- `inc/customizer/settings/header/mobile-navigation.php` — Legacy mobile controls
- `inc/customizer/js/customizer-parts/setup-controls-movement.ts` — Controls movement logic
- `inc/customizer/js/postmessage-parts/menu-triggers.ts` — postMessage handlers
- `inc/customizer/styles/header-builder-menu-styles.php` — CSS output
- `Customizer/HeaderBuilder/HeaderBuilderOutput.php` — Frontend rendering
- `Customizer/HeaderBuilder/HeaderBuilderConfig.php` — Widget configuration

---

## Instructions for AI Agent

1. **DO NOT** just update documentation or mark this as complete.
2. **DO** perform deep codebase analysis to answer each question above.
3. **DO** provide code snippets and file references as evidence.
4. **DO** test your understanding by tracing the full flow from control → postMessage → CSS output.
5. **AFTER** answering all questions, summarize findings and recommend next steps.

## After Answering Questions

Once all questions are answered with evidence:

1. **Determine if unification is needed**: Should mobile menu trigger have its own dedicated controls like desktop, or is the current approach (reusing legacy) acceptable?

2. **Identify potential issues**: Are there any bugs or inconsistencies caused by the mixed approach?

3. **Document any refactoring needs**: If unification is desired, outline the changes required.

---

## Recent Completed

- ✅ Menu trigger widget investigation and documentation (v2.11.8+89)
- ✅ Visual QA and refinement of margin-padding spacing fix (v2.11.8+87)
- ✅ Improved visual spacing in `margin-padding` unit controls (v2.11.8+86)
- ✅ Context Handoff Preparation for Issue #2 (v2.11.8+85)
