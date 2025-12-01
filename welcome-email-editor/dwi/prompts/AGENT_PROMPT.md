# Agent Prompt: Convert Mailer Type to Image Toggle Integration Selector

**Status:** 🎯 Active
**Version:** v6.2.2+20
**Last Updated:** 2025-12-01

**Rules:**
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)
2. `.antigravityignore` (Forbidden files and directories that you MUST NOT access)
3. `ai-docs/welcome-email-editor/rules.md` (Project-specific rules)

## Objective

Transform the "Mailer Type" field into an "Integration" selector with an image toggle UI. Replace the current radio button interface with a modern image-based toggle showing an envelope icon (for SMTP) and the Mailjet logo (for Mailjet API).

## Background

Currently, the plugin uses a simple radio button selection for "Mailer Type" with two options:
- SMTP (Default)
- Mailjet API

This needs to be upgraded to a more visual, user-friendly interface with:
- **Label change:** "Mailer Type" → "Integration"
- **UI change:** Radio buttons → Image toggle buttons
- **Visual indicators:** Envelope icon for SMTP, Mailjet logo for Mailjet API

**Current Version:** 6.2.2

## Requirements

### 1. Change Field Label

**File:** `wp-content/plugins/welcome-email-editor/modules/settings/class-settings-module.php`

**Line 289:** Change the field label in `add_settings_field()` call:
```php
// FROM:
__( 'Mailer Type', 'welcome-email-editor' ),

// TO:
__( 'Integration', 'welcome-email-editor' ),
```

### 2. Update Template with Image Toggle UI

**File:** `wp-content/plugins/welcome-email-editor/modules/settings/templates/fields/smtp/mailer-type.php`

**Changes needed:**
- Replace radio button structure with image toggle structure
- Add envelope icon image for SMTP option
- Add Mailjet logo image for Mailjet API option
- Update classes for image toggle styling
- Maintain same input values: `smtp` and `mailjet_api`
- Keep the same input name: `weed_settings[mailer_type]`

**Expected UI Structure:**
```html
<div class="weed-fields weed-image-toggle-fields">
    <!-- SMTP Option with Envelope Icon -->
    <label for="weed_settings--mailer_type-smtp" class="image-toggle-label">
        <input type="radio" name="weed_settings[mailer_type]" 
               id="weed_settings--mailer_type-smtp"
               value="smtp" <?php checked( $value, 'smtp' ); ?> />
        <div class="image-toggle-container">
            <img src="[path-to-envelope-icon]" alt="SMTP (Default)" class="toggle-image" />
            <span class="toggle-label">SMTP (Default)</span>
        </div>
    </label>

    <!-- Mailjet API Option with Mailjet Logo -->
    <label for="weed_settings--mailer_type-mailjet_api" class="image-toggle-label">
        <input type="radio" name="weed_settings[mailer_type]" 
               id="weed_settings--mailer_type-mailjet_api"
               value="mailjet_api" <?php checked( $value, 'mailjet_api' ); ?> />
        <div class="image-toggle-container">
            <img src="[path-to-mailjet-logo]" alt="Mailjet API" class="toggle-image" />
            <span class="toggle-label">Mailjet API</span>
        </div>
    </label>
</div>
```

### 3. Add Image Assets

**Action required:** User will provide two images:
1. **Envelope icon** - For SMTP (Default) option
2. **Mailjet logo** - For Mailjet API option

**Recommended location:** `wp-content/plugins/welcome-email-editor/assets/images/integrations/`

Create directory if it doesn't exist, then:
- Save envelope icon as: `smtp-envelope.png` or `smtp-envelope.svg`
- Save Mailjet logo as: `mailjet-logo.png` or `mailjet-logo.svg`

### 4. Add CSS Styling

**File:** `wp-content/plugins/welcome-email-editor/assets/scss/settings.scss`

Add new styles for the image toggle interface:

```scss
.weed-image-toggle-fields {
    display: flex;
    gap: 20px;
    margin: 15px 0;

    .image-toggle-label {
        position: relative;
        cursor: pointer;
        flex: 1;
        max-width: 200px;

        input[type="radio"] {
            position: absolute;
            opacity: 0;
            pointer-events: none;
        }

        .image-toggle-container {
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
            transition: all 0.3s ease;
            background: #fff;

            &:hover {
                border-color: #0073aa;
                box-shadow: 0 2px 8px rgba(0, 115, 170, 0.1);
            }

            .toggle-image {
                width: 60px;
                height: 60px;
                object-fit: contain;
                display: block;
                margin: 0 auto 10px;
            }

            .toggle-label {
                display: block;
                font-size: 14px;
                font-weight: 500;
                color: #555;
            }
        }

        input[type="radio"]:checked + .image-toggle-container {
            border-color: #0073aa;
            background: #f0f8ff;
            box-shadow: 0 2px 12px rgba(0, 115, 170, 0.2);

            .toggle-label {
                color: #0073aa;
                font-weight: 600;
            }
        }
    }
}
```

**After editing SCSS:** Compile to CSS:
```bash
npm run build:styles
# Or manually if needed
```

## Implementation Steps

### Step 1: Wait for Image Assets
User will provide the envelope icon and Mailjet logo images.

### Step 2: Create Images Directory
Create `wp-content/plugins/welcome-email-editor/assets/images/integrations/` directory.

### Step 3: Save Image Assets
Place the provided images in the integrations directory with appropriate names.

### Step 4: Update Field Label
Modify `class-settings-module.php` line 289 to change "Mailer Type" to "Integration".

### Step 5: Update Template
Rewrite `mailer-type.php` template with the new image toggle structure.

### Step 6: Add CSS Styling
Add image toggle styles to `settings.scss` and compile.

### Step 7: Test the UI
Verify the image toggle works correctly and settings are saved properly.

## Expected Output

After completion:
- ✅ Field label changed from "Mailer Type" to "Integration"
- ✅ Radio buttons replaced with image toggle UI
- ✅ Envelope icon displayed for SMTP option
- ✅ Mailjet logo displayed for Mailjet API option
- ✅ Visual feedback on hover and selection
- ✅ Settings save and load correctly
- ✅ Existing functionality preserved

## Files to Modify

### Primary (Required)
| File | Lines | Action |
|------|-------|--------|
| `modules/settings/class-settings-module.php` | 289 | Change label "Mailer Type" to "Integration" |
| `modules/settings/templates/fields/smtp/mailer-type.php` | All | Rewrite with image toggle structure |
| `assets/scss/settings.scss` | New section | Add image toggle styles |

### New Files/Directories
| Path | Type | Purpose |
|------|------|---------|
| `assets/images/integrations/` | Directory | Store integration icons/logos |
| `assets/images/integrations/smtp-envelope.[png\|svg]` | Image | SMTP envelope icon |
| `assets/images/integrations/mailjet-logo.[png\|svg]` | Image | Mailjet logo |

## Success Criteria

✅ Field label displays "Integration" instead of "Mailer Type"
✅ Image toggle UI replaces radio buttons
✅ Envelope icon visible for SMTP option
✅ Mailjet logo visible for Mailjet API option
✅ Hover effects work smoothly
✅ Selected state clearly indicated
✅ Settings save correctly with same values (`smtp` or `mailjet_api`)
✅ Settings load correctly on page refresh
✅ Responsive design works on different screen sizes
✅ No JavaScript console errors
✅ CSS compiled successfully

## Resources

- **Plugin Directory:** `c:\\laragon\\www\\mapsteps\\wp-content\\plugins\\welcome-email-editor\\`
- **Current Template:** `modules/settings/templates/fields/smtp/mailer-type.php`
- **Settings Module:** `modules/settings/class-settings-module.php`
- **Styles:** `assets/scss/settings.scss`
- **Compiled CSS:** `assets/css/settings.css`
- **Reference Mockup:** User-provided screenshot showing desired UI

## Visual Reference

**Current UI:** Simple radio buttons with text labels
```
○ SMTP (Default)
○ Mailjet API
```

**New UI:** Image toggle with icons and labels
```
┌─────────────┐     ┌─────────────┐
│   [📧]      │     │   [MAILJET] │
│             │     │             │
│ SMTP        │     │ Mailjet API │
│ (Default)   │     │             │
└─────────────┘     └─────────────┘
```

## Testing Checklist

After making changes:
- [ ] Navigate to plugin settings page
- [ ] Verify "Integration" label is displayed (not "Mailer Type")
- [ ] Confirm both image toggles are visible
- [ ] Check envelope icon displays correctly for SMTP
- [ ] Check Mailjet logo displays correctly for Mailjet API
- [ ] Click SMTP toggle - verify visual selection feedback
- [ ] Click Mailjet API toggle - verify visual selection feedback
- [ ] Save settings with SMTP selected
- [ ] Reload page - confirm SMTP is still selected
- [ ] Save settings with Mailjet API selected
- [ ] Reload page - confirm Mailjet API is still selected
- [ ] Test hover effects on both toggles
- [ ] Verify no console errors
- [ ] Check responsive behavior on smaller screens

## Notes

- **No functionality changes** - Only UI/UX improvements
- The underlying values (`smtp` and `mailjet_api`) remain the same
- All existing visibility logic for SMTP/Mailjet settings sections remains unchanged
- This is a visual enhancement to improve user experience
- Compatible with existing settings and won't affect saved configurations

---

**Ready to modernize the Integration selector with image toggle UI**
