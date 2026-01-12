# Agent Prompt: Manual Testing of Postmessage.ts Splitting

## Objective

Perform manual testing of the customizer live preview functionality to confirm the postmessage.ts splitting works correctly in the WordPress Customizer.

---

## Prerequisites

**1. Read the project rules:**
```
ai-docs/wpbf-premium/rules.md
```

**2. Read the progress handoff document:**
```
ai-docs/wpbf-premium/bagus/progress-handoffs/PROGRESS_HANDOFF.md
```

---

## Context

The postmessage.ts file has been split into 15 modular files and verified:
- ✅ All 75+ settings migrated correctly
- ✅ Build succeeds (`pnpm run build-postmessage`)
- ✅ Backup file deleted

**Remaining task:** Manual testing in WordPress Customizer

---

## Testing Instructions

### 1. Open WordPress Customizer
Navigate to: `Appearance > Customize`

### 2. Test Settings by Category

#### Theme Colors (Design > Theme Colors)
- [ ] Base color
- [ ] Brand color  
- [ ] Accent color

#### Typography (Design > Typography)
- [ ] Page font size (responsive)
- [ ] Heading sizes (H1-H6)
- [ ] Line heights
- [ ] Letter spacing

#### Navigation (Header > Navigation)
- [ ] Menu letter spacing
- [ ] Off-canvas settings
- [ ] Stacked menu settings

#### Transparent Header (Header > Transparent Header)
- [ ] Background color
- [ ] Font colors
- [ ] Logo colors

#### Sticky Navigation (Header > Sticky Navigation)
- [ ] Width/height
- [ ] Box shadow
- [ ] Colors

#### Mobile Navigation (Header > Mobile Navigation)
- [ ] Overlay color
- [ ] Off-canvas width

#### CTA Button (Header > Call to Action)
- [ ] Button text
- [ ] Colors (default/transparent/sticky)

#### Footer (Footer > Widget Footer)
- [ ] Width
- [ ] Colors

#### WooCommerce (if active)
- [ ] Cart label
- [ ] Quick view styles

### 3. Verify Live Preview
For each setting:
1. Change the value in Customizer
2. Confirm the preview updates immediately (no page refresh)
3. Check browser console for errors

---

## Success Criteria

- [ ] All settings update live preview correctly
- [ ] No JavaScript errors in console
- [ ] Responsive settings work on all breakpoints

---

## After Testing

If all tests pass:
1. Update PROGRESS_HANDOFF.md to mark as fully complete
2. This task is finished

If issues found:
1. Document the specific settings that fail
2. Debug and fix the relevant part file
3. Rebuild with `pnpm run build-postmessage`
4. Re-test
