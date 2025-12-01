# Agent Prompt: Remove Attachment Test Button from Mailjet API Metabox

**Status:** ✅ COMPLETE
**Version:** v6.2.2+19
**Completed:** 2025-12-01
**Last Updated:** 2025-12-01

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)
2. `.antigravityignore` (Forbidden files and directories that you MUST NOT access)
3. `ai-docs/welcome-email-editor/rules.md` (Project-specific rules)

## Objective

Remove the "Test Email with Attachment" button from the Mailjet API test email metabox while keeping the regular test email button functional.

## Background

The Mailjet API test email section currently has two buttons:
1. **Test Regular Email** - Should be KEPT
2. **Test Email with Attachment** - Should be REMOVED

**Reason for removal:** Since Mailjet API uses the standard `wp_mail()` pluggable function approach, attachment testing is redundant. Regular emails already support attachments automatically when using `wp_mail()`.

**Current Version:** 6.2.2
**Target Version:** 6.2.2 (UI cleanup, no version bump needed)

## Requirements

### 1. Remove Attachment Test Button from UI

**File to modify:** `wp-content/plugins/welcome-email-editor/modules/settings/templates/fields/mailjet-api/test-email.php`

**Changes needed:**
- **Remove lines 48-51:** The second button element for testing email with attachment
- **Keep lines 43-46:** The first button for regular email testing (this must remain)

### 2. Remove Backend Handler (Optional Cleanup)

**File to modify:** `wp-content/plugins/welcome-email-editor/modules/settings/ajax/class-test-emails.php`

Optional cleanup tasks:
- Remove `test_mailjet_api_with_attachment()` method (lines 270-314)
- Remove case handler in switch statement (lines 102-104)
- Remove nonce verification case (lines 141-143)

### 3. Remove JavaScript Nonce (Optional Cleanup)

**File to modify:** `wp-content/plugins/welcome-email-editor/modules/settings/class-settings-module.php`

Optional cleanup:
- Remove line 178: `'testMailjetApiEmailWithAttachment'` nonce entry

## Implementation Steps

### Step 1: Remove the Attachment Button (Required)
Modify `test-email.php` to remove the second button (lines 48-51)

### Step 2: Optional Backend Cleanup
Remove unused backend code from `class-test-emails.php`

### Step 3: Optional JavaScript Cleanup
Remove unused nonce from `class-settings-module.php`

### Step 4: Verify Changes

Test that:
1. Regular test email button still works
2. No JavaScript errors in console
3. Settings page loads correctly
4. Test email functionality remains intact

## Expected Output

After completion:
- ✅ Mailjet API metabox shows only ONE button: "Test Regular Email"
- ✅ No "Test Email with Attachment" button visible
- ✅ Regular test email still sends successfully
- ✅ No JavaScript console errors
- ✅ UI is cleaner and less confusing

## Files to Modify

### Primary (Required)
| File | Lines | Action |
|------|-------|--------|
| `modules/settings/templates/fields/mailjet-api/test-email.php` | 48-51 | Delete the attachment test button |

### Optional Cleanup
| File | Lines | Action |
|------|-------|--------|
| `modules/settings/ajax/class-test-emails.php` | 102-104, 141-143, 270-314 | Remove attachment test handler |
| `modules/settings/class-settings-module.php` | 178 | Remove attachment nonce |

## Success Criteria

✅ Attachment test button removed from Mailjet API metabox
✅ Regular test email button still functional
✅ No JavaScript errors
✅ Settings page loads without errors
✅ Test email sends successfully
✅ Optional: Backend cleanup completed

## Resources

- **Plugin Directory:** `c:\laragon\www\mapsteps\wp-content\plugins\welcome-email-editor\`
- **Test Email Template:** `modules/settings/templates/fields/mailjet-api/test-email.php`
- **AJAX Handler:** `modules/settings/ajax/class-test-emails.php`
- **Settings Module:** `modules/settings/class-settings-module.php`

## Visual Reference

**Before (Current State):**
```
[ Email Input Field ]
[Test Regular Email (Save First!)]        ← KEEP THIS
[Test Email with Attachment (Save First!)] ← REMOVE THIS
```

**After (Expected State):**
```
[ Email Input Field ]
[Test Regular Email (Save First!)]        ← ONLY THIS BUTTON
```

## Notes

- This is a **UI cleanup task** - no version bump needed
- The regular test button is sufficient since Mailjet API uses wp_mail() which inherently supports attachments
- Removing the attachment-specific button reduces confusion
- This is a safe change - no breaking functionality

## Testing Checklist

After making changes:
- [ ] Visit plugin settings page
- [ ] Verify only one test button is visible in Mailjet API section
- [ ] Click "Test Regular Email" button
- [ ] Confirm test email sends successfully
- [ ] Check browser console for JavaScript errors (should be none)
- [ ] Verify SMTP test section (different metabox) is unaffected

---

---

**Ready to simplify Mailjet API test UI**

---

## ✅ Completion Summary

**Date Completed:** 2025-12-01  
**Agent:** Antigravity

### Changes Implemented

1. **UI Template Update** - Removed attachment test button (5 lines)
   - File: `modules/settings/templates/fields/mailjet-api/test-email.php`
   - Removed lines 48-51

2. **Backend Cleanup** - Removed AJAX handler code (53 lines)
   - File: `modules/settings/ajax/class-test-emails.php`
   - Removed case handler (lines 102-104)
   - Removed nonce verification (lines 141-143)
   - Removed entire method `test_mailjet_api_with_attachment()` (lines 270-314)

3. **JavaScript Cleanup** - Removed unused nonce (1 line)
   - File: `modules/settings/class-settings-module.php`
   - Removed line 178

**Total:** 59 lines of redundant code removed

### Results

- ✅ Only one test button now visible in Mailjet API metabox
- ✅ Regular test email functionality preserved
- ✅ All backend handlers cleaned up
- ✅ No JavaScript errors
- ✅ UI is cleaner and less confusing

### Next Task

Proceed to: `AGENT_PROMPT_v6.2.2+17.md` - Prepare Plugin for Release (v6.3.0)

