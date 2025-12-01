# Integration Image Toggle - Design Reference

This document contains the visual mockup for the new Integration selector UI.

## Current Design (Radio Buttons)

The current implementation uses simple radio buttons with text labels for selecting the mailer type.

## New Design (Image Toggle)

The new design will use image-based toggle buttons with icons for a more modern, visual interface.

### Mockup Reference

![Integration Toggle Mockup](C:/Users/YOKO/.gemini/antigravity/brain/9f21f9a2-c460-4732-aa64-ed64854488f6/uploaded_image_1764548998887.png)

### Design Specifications

**Layout:**
- Two side-by-side toggle options
- Each toggle contains an icon and label
- Visual feedback on hover and selection

**Option 1: SMTP (Default)**
- Icon: Envelope (to be provided by user)
- Label: "SMTP (Default)"
- Default selected state

**Option 2: Mailjet API**
- Icon: Mailjet logo (to be provided by user)
- Label: "Mailjet API"

**Visual States:**
- **Default:** Light border, white background
- **Hover:** Blue border, subtle shadow
- **Selected:** Blue border, light blue background, bold label

### User-Provided Assets

The user will provide two image assets:
1. **Envelope icon** - For SMTP option
2. **Mailjet logo** - For Mailjet API option

These should be saved in: `assets/images/integrations/`

## Implementation Notes

- Field label changes from "Mailer Type" to "Integration"
- Radio input values remain the same: `smtp` and `mailjet_api`
- No functionality changes, only UI/UX improvements
- Fully responsive design
