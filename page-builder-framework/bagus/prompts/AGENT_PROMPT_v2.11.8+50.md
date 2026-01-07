# Agent Prompt

**Role**: Expert WordPress theme developer and AI coding assistant.

**Context**: Working on "page-builder-framework" WordPress theme.
**Source of Truth**: `ai-docs/page-builder-framework/bagus/progress-handoffs/PROGRESS_HANDOFF.md`
**Project Rules**: `ai-docs/page-builder-framework/rules.md`

**Objective**: Verify Footer Builder parity with Header Builder across all implementation aspects.

**Status**: Session v2.11.8+50 - Footer Builder verification against Header Builder.

---

## Task: Footer Builder vs Header Builder Verification

Verify that the Footer Builder implementation matches the Header Builder pattern across all aspects. Use Header Builder as the reference implementation.

### Verification Checklist

#### 1. Existing Controls Handling

Compare how existing controls are handled when builder is enabled:

| Aspect | Header Builder | Footer Builder | Status |
|--------|---------------|----------------|--------|
| Controls movement to builder sections | `header-builder.ts` | `footer-builder.ts` | ❓ Verify |
| Original controls behavior | Moved/hidden when builder enabled | Should match | ❓ Verify |

**Files to check**:
- Theme: `Customizer/Controls/Header/header-builder.ts`
- Theme: `Customizer/Controls/Footer/footer-builder.ts`
- Premium: `inc/customizer/js/customizer.ts` (controls movement)

#### 2. New Controls (if any)

Check if footer builder needs any new controls that header builder has:

| Control Type | Header Builder Has | Footer Builder Has | Status |
|--------------|-------------------|-------------------|--------|
| Row controls (bg, padding, etc.) | ✅ Yes | ✅ Yes (v2.11.8+46) | ❓ Verify |
| Widget controls | ✅ Yes | ✅ Yes | ❓ Verify |
| Visibility controls | Has (commented out) | ? | ❓ Verify |

**Files to check**:
- Theme: `Customizer/HeaderBuilder/HeaderBuilderConfig.php`
- Theme: `Customizer/FooterBuilder/FooterBuilderConfig.php`

#### 3. Fields Output (Frontend Rendering)

Compare output rendering patterns:

| Aspect | Header Builder | Footer Builder | Status |
|--------|---------------|----------------|--------|
| Output class | `HeaderBuilderOutput.php` | `FooterBuilderOutput.php` | ❓ Verify |
| Row rendering | `render_desktop_row()`, `render_mobile_row()` | `render_row()` | ❓ Verify |
| Widget rendering | `render_widget()` | `render_widget()` | ❓ Verify |
| CSS classes pattern | `.wpbf-header-row-{row_key}` | `.wpbf-footer-row-{row_key}` | ❓ Verify |

**Files to check**:
- Theme: `Customizer/HeaderBuilder/HeaderBuilderOutput.php`
- Theme: `Customizer/FooterBuilder/FooterBuilderOutput.php`

#### 4. Styles Output (CSS Generation)

Compare CSS output patterns:

| Aspect | Header Builder | Footer Builder | Status |
|--------|---------------|----------------|--------|
| Styles file | `header-builder-rows-styles.php` | `footer-builder-styles.php` | ❓ Verify |
| Included in `styles.php` | ✅ Yes | ✅ Yes (v2.11.8+48) | ❓ Verify |
| Row styling properties | max_width, padding, bg, colors, font | Should match | ❓ Verify |

**Files to check**:
- Theme: `inc/customizer/styles/header-builder-rows-styles.php`
- Theme: `inc/customizer/styles/footer-builder-styles.php`
- Theme: `inc/customizer/styles.php`

#### 5. Postmessage Scripts (Live Preview)

Compare postmessage implementation:

| Aspect | Header Builder | Footer Builder | Status |
|--------|---------------|----------------|--------|
| Postmessage file | `header-builder-rows.ts` | `footer-builder-rows.ts` | ❓ Verify |
| Row controls handlers | ✅ Yes | ✅ Yes (v2.11.8+47) | ❓ Verify |
| Widget controls handlers | ✅ Yes | ? | ❓ Verify |

**Files to check**:
- Theme: `Customizer/Controls/Header/header-builder-rows.ts`
- Theme: `Customizer/Controls/Footer/footer-builder-rows.ts`

#### 6. Premium Plugin Integration (wpbf-premium)

Compare premium plugin integration:

| Aspect | Header Builder | Footer Builder | Status |
|--------|---------------|----------------|--------|
| Controls movement | `setupHeaderBuilderControlsMovement()` | `setupFooterBuilderControlsMovement()` | ❓ Verify |
| Premium controls | Various | `footer_sticky` moved | ❓ Verify |
| Styles output | If any premium controls | If any premium controls | ❓ Verify |

**Files to check**:
- Premium: `inc/customizer/js/customizer.ts`
- Premium: `inc/customizer/customizer-functions.php`
- Premium: `inc/customizer/styles.php`

---

## Verification Process

1. **For each aspect above**, compare the header builder implementation with footer builder
2. **Document findings** in a table format showing what matches and what's missing
3. **Identify gaps** where footer builder doesn't match header builder pattern
4. **Implement fixes** for any gaps found
5. **Update handoff** with verification results

---

## Expected Outcome

After verification, the Footer Builder should:
- Handle existing controls the same way Header Builder does
- Have equivalent new controls (if applicable)
- Render output following the same patterns
- Generate CSS styles following the same patterns
- Have postmessage scripts for all relevant controls
- Integrate with wpbf-premium following the same patterns

---

## Reference Files Summary

### Theme (page-builder-framework)

| Category | Header Builder | Footer Builder |
|----------|---------------|----------------|
| Config | `Customizer/HeaderBuilder/HeaderBuilderConfig.php` | `Customizer/FooterBuilder/FooterBuilderConfig.php` |
| Output | `Customizer/HeaderBuilder/HeaderBuilderOutput.php` | `Customizer/FooterBuilder/FooterBuilderOutput.php` |
| Controls | `Customizer/Controls/Header/header-builder.ts` | `Customizer/Controls/Footer/footer-builder.ts` |
| Postmessage | `Customizer/Controls/Header/header-builder-rows.ts` | `Customizer/Controls/Footer/footer-builder-rows.ts` |
| Styles | `inc/customizer/styles/header-builder-rows-styles.php` | `inc/customizer/styles/footer-builder-styles.php` |

### Premium Plugin (wpbf-premium)

| Category | File |
|----------|------|
| Controls Movement | `inc/customizer/js/customizer.ts` |
| Output Hooks | `inc/customizer/customizer-functions.php` |
| Styles | `inc/customizer/styles.php` |
