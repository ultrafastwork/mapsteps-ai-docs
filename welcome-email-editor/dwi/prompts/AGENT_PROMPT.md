# Agent Prompt: Prepare Plugin for Release

**Status:** 🎯 Active
**Version:** v6.2.2+17
**Last Updated:** 2025-12-01

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)
2. `.antigravityignore` (Forbidden files and directories that you MUST NOT access)
3. `ai-docs/welcome-email-editor/rules.md` (Project-specific rules)

## Objective

Prepare the Welcome Email Editor (Swift SMTP) plugin for release with the newly implemented Mailjet API feature. This will be version **6.3.0** (new feature warrants minor version bump).

## Background

The plugin has been enhanced with a complete Mailjet API integration:
- ✅ Mailjet API sender implementation (alternative to SMTP)
- ✅ Full attachment support using `wp_mail()` pluggable function
  - Uses `pre_wp_mail` filter hook to intercept emails (line 80 in `class-smtp-output.php`)
  - Accepts same parameters as `wp_mail()` including attachments array
  - Supports regular attachments (up to 14MB total) and inline attachments for HTML emails
  - No breaking changes - any code using `wp_mail($to, $subject, $message, $headers, $attachments)` works automatically
- ✅ Complete UI with settings and test email functionality
- ✅ All E2E tests passing (22/22 assertions)
- ✅ WordPress core email integration verified
- ✅ Documentation updated with technical implementation details

**Current Version:** 6.2.2
**Target Version:** 6.3.0

## Requirements

### 1. Update Version Numbers
Update version in the following files:

#### Main Plugin File
**File:** `wp-content/plugins/welcome-email-editor/sb_welcome_email_editor.php`
- Line 5: `Version: 6.3.0`
- Line 20: `define( 'WEED_PLUGIN_VERSION', '6.3.0' );`

#### Readme File
**File:** `wp-content/plugins/welcome-email-editor/readme.txt`
- Line 6: `Stable tag: 6.3.0`
- Update "Tested up to" if needed (currently 6.8)

### 2. Update Changelog

**File:** `wp-content/plugins/welcome-email-editor/readme.txt`

Add new changelog entry after line 63:

```
= 6.3.0 | December 1, 2025 =
* New: Mailjet API integration as alternative to SMTP
* New: Send emails via Mailjet API (bypasses SMTP, prevents auto-adding contacts to lists)
* New: Mailer type selector (SMTP or Mailjet API)
* New: Mailjet API settings section with API Key and Secret Key fields
* New: Test email functionality for Mailjet API (with and without attachments)
* New: Full attachment support for Mailjet API (up to 14MB)
* New: Inline attachment support for HTML emails with embedded images
* New: Uses wp_mail() pluggable function for full WordPress compatibility
* Tweak: Improved settings page UI with dynamic field visibility
* Tweak: Enhanced email logging for Mailjet API
* Tested: Comprehensive E2E test coverage for all email functionality
```

### 3. Verify Files and Implementation

Ensure the following are in place:
- ✅ `modules/mailjet-api/class-mailjet-api-sender.php` - Main API sender class
- ✅ `modules/mailjet-api/class-mailjet-api-module.php` - Module initialization
- ✅ Mailjet API settings fields in settings module
- ✅ Test email metabox for Mailjet API
- ✅ Visibility logic for showing/hiding settings based on mailer type
- ✅ JavaScript for dynamic UI updates
- ✅ `pre_wp_mail` filter integration for email routing

### 4. Optional: Create Release Notes

Create a release notes document summarizing:
- What's new in 6.3.0
- Why users should update
- Migration notes (if any)
- Known issues (if any)

### 5. Validation Steps

After updating version numbers:
1. Verify version number displays correctly in WordPress admin (Plugins page)
2. Check that settings page loads without errors
3. Confirm Mailjet API functionality still works
4. Optionally run E2E tests to ensure nothing broke

## Implementation Steps

### Step 1: Update Main Plugin File
Update version number and constant in `sb_welcome_email_editor.php`

### Step 2: Update Readme Changelog
Add new 6.3.0 changelog entry in `readme.txt`

### Step 3: Update Stable Tag
Update stable tag in `readme.txt` to 6.3.0

### Step 4: Verify Changes
Review all changes to ensure accuracy and completeness

### Step 5: Optional Testing
Run manual or E2E tests to ensure version update didn't break anything

## Expected Output

After completion:
- ✅ Plugin version updated to 6.3.0 in all relevant files
- ✅ Changelog updated with comprehensive 6.3.0 entry
- ✅ All version references consistent across codebase
- ✅ Changes verified and ready for distribution

## Success Criteria

✅ Version updated to 6.3.0 in main plugin file
✅ WEED_PLUGIN_VERSION constant updated to 6.3.0
✅ Stable tag updated in readme.txt
✅ Comprehensive changelog entry added
✅ No syntax errors or warnings
✅ Plugin ready for WordPress.org submission or distribution

## Resources

- **Plugin Directory:** `c:\laragon\www\mapsteps\wp-content\plugins\welcome-email-editor\`
- **Main File:** `sb_welcome_email_editor.php`
- **Readme:** `readme.txt`
- **Previous Changelog:** Lines 64-108 in readme.txt
- **Technical Documentation:** `ai-docs/welcome-email-editor/dwi/mailjet_attachment_technical_docs.md`

## Notes

- This is a **minor version bump (6.2.2 → 6.3.0)** due to new feature (Mailjet API)
- The Mailjet API implementation is fully tested and production-ready
- All E2E tests passing (22/22 assertions)
- No breaking changes - backward compatible with existing SMTP setup
- **wp_mail() compatibility confirmed** - uses pluggable function approach via `pre_wp_mail` filter

---

**Ready to prepare plugin release v6.3.0**
