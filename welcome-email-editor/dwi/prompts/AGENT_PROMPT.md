# Agent Prompt: Implement WordPress Core Email Tests

**Status:** 🎯 Active
**Version:** v6.2.2+15
**Last Updated:** 2025-11-26

**Rules**:
Please strictly follow the rules defined in:

1. `.antigravityrules` (Root-level operating principles)
2. `.antigravityignore` (Forbidden files and directories that you MUST NOT access)
3. `ai-docs/welcome-email-editor/rules.md` (Project-specific rules)

## Objective

Implement E2E tests for WordPress core email functionality to verify that the Welcome Email Editor plugin correctly sends all WordPress system emails through the configured mailer (SMTP or Mailjet API).

## Background

The E2E testing framework is fully operational with real Mailjet credentials configured. All current tests (11/11) are passing. The next step is to expand test coverage to include WordPress core emails.

**Current Test Status:**
- ✅ Settings persistence tests passing
- ✅ Test email sending tests passing
- ✅ UI logic tests passing
- 🎯 Need to add WordPress core email tests

**Testing Infrastructure:**
- **Location:** `c:\laragon\www\mapsteps\welcome-email-editor-e2e-testing\`
- **Framework:** Nightwatch v3.12.3
- **WordPress URL:** `http://mapsteps.local`
- **Test Email:** `dwie.cendhol@gmail.com`

## Requirements

### 1. User Registration Email Test
Create a test that:
- Creates a new WordPress user via admin interface
- Verifies the registration email is sent without errors
- Uses temporary test user (e.g., `test-user-{timestamp}@example.com`)
- Does NOT delete the user after test (per user request)

### 2. Password Reset Email Test
Create a test that:
- Triggers password reset for a test user
- Verifies the password reset email is sent without errors
- Checks that the plugin doesn't throw errors during the process

### 3. Admin New User Notification Test
Create a test that:
- Creates a new user
- Verifies admin notification email is sent without errors
- Admin email should be sent to the WordPress admin email address

## Implementation Steps

### Step 1: Create WordPress Email Test Specification
Create `tests/specs/wordpress-emails.spec.ts` with tests for:
- User registration email
- Password reset email
- Admin new user notification

### Step 2: Create Helper Functions
Create or update helper files to support:
- User creation via WordPress admin
- Password reset triggering
- Email verification (checking for no errors)

### Step 3: Test Configuration
- Use test email: `dwie.cendhol@gmail.com` for all test users
- Create temporary users with pattern: `test-user-{timestamp}`
- Do NOT delete users after tests

### Step 4: Run and Validate
- Run all WordPress email tests
- Verify no JavaScript errors occur
- Verify WordPress doesn't throw PHP errors
- Document results

## Test Approach

Per user request from previous session:
> "just check the plugin doesn't throw the error"

The tests should:
1. Trigger the WordPress email action
2. Wait for the action to complete
3. Verify the page is still functional (no errors)
4. NOT check for actual email delivery or notice visibility

## Expected Test Structure

```typescript
describe("WordPress Core Emails", function () {
  it("should send user registration email without errors", function (browser) {
    // Create new user
    // Verify no errors
    // Verify page functional
  });

  it("should send password reset email without errors", function (browser) {
    // Trigger password reset
    // Verify no errors
    // Verify page functional
  });

  it("should send admin notification email without errors", function (browser) {
    // Create new user (triggers admin notification)
    // Verify no errors
    // Verify page functional
  });
});
```

## Success Criteria

✅ New test file created: `tests/specs/wordpress-emails.spec.ts`
✅ All WordPress email tests passing
✅ No errors thrown during email sending
✅ Test users created with email: `dwie.cendhol@gmail.com`
✅ Users NOT deleted after tests
✅ Documentation updated with results

## Resources

- **E2E Tests Location:** `c:\laragon\www\mapsteps\welcome-email-editor-e2e-testing\`
- **WordPress Admin:** `http://mapsteps.local/wp-admin/`
- **Test Credentials:** In `.env.local` at project root
- **Existing Tests:** Reference `smtp-correctness.spec.ts` and `mailjet-correctness.spec.ts` for patterns

## Notes

- Test users should use pattern: `test-user-{timestamp}`
- All test user emails should be: `dwie.cendhol@gmail.com`
- Do NOT delete users after tests
- Focus on verifying no errors, not email delivery
- Use real Mailjet credentials already configured in `test-data.ts`

---

**Status:** 🎯 Ready to implement WordPress core email tests

**Start by creating the test specification file and helper functions.**
