# Agent Prompt: Test billingCycle Integration

**Status:** 🎯 Active
**Version:** v1.0.0+2
**Last Updated:** 2025-12-09

**Rules:**
Please strictly follow the rules defined in:
1. `ai-docs/jackrabbit-calendar/rules.md` (Project-specific rules)

## Objective

Test and verify the updated `isClassRecurring()` method that now uses the API's `billingCycle` field instead of the previous 14-week calculation logic.

## Background

The `isClassRecurring()` method in `JackrabbitData.js` was updated to use the new `billingCycle` field from the Jackrabbit API:

```javascript
isClassRecurring(row) {
    if (row.tuition && row.tuition.billingCycle) {
        const billingCycle = row.tuition.billingCycle.toLowerCase();
        return billingCycle === 'monthly';
    }
    return false;
}
```

### API billingCycle Values
| Value | Meaning | `isClassRecurring()` Returns |
|-------|---------|------------------------------|
| `"Monthly"` | Tuition paid monthly | `true` |
| `"By Session Dates"` | One-time session tuition | `false` |

## Requirements

### 1. Verify API Response
Confirm the API returns the `billingCycle` field in the expected format:
```json
{
  "tuition": {
    "billingCycle": "Monthly" | "By Session Dates",
    "fee": 99,
    "days": { ... }
  }
}
```

### 2. Test isClassRecurring() Method
Verify the method correctly identifies:
- Classes with `"Monthly"` billing → returns `true`
- Classes with `"By Session Dates"` billing → returns `false`
- Classes with missing `billingCycle` → returns `false` with console warning

### 3. Check UI Display
Verify any UI components that use `isClassRecurring()` display correctly:
- Monthly tuition classes show appropriate pricing/label
- Session-based tuition classes show appropriate pricing/label

## Files to Review

| File | Purpose |
|------|---------|
| `_vue/shared/mixins/JackrabbitData.js` | Contains `isClassRecurring()` method |
| `_vue/jack-2-list-views/src/components/*.vue` | List view components |
| `_vue/jack-monthly-calendar-2/src/components/*.vue` | Calendar components |
| `_vue/jack-weekly-calendar/src/*.vue` | Weekly calendar components |

## Testing Steps

### Step 1: Check API Response
1. Open browser developer tools
2. Navigate to a page with the Jackrabbit Calendar
3. Check Network tab for API response
4. Verify `tuition.billingCycle` field exists

### Step 2: Console Testing
Add temporary console log to verify:
```javascript
console.log('Class:', row.name, 'billingCycle:', row.tuition?.billingCycle, 'isRecurring:', this.isClassRecurring(row));
```

### Step 3: Visual Verification
- Check that tuition displays correctly for different class types
- Verify no JavaScript errors in console

## Success Criteria

✅ API returns `billingCycle` field correctly
✅ `isClassRecurring()` returns `true` for "Monthly" classes
✅ `isClassRecurring()` returns `false` for "By Session Dates" classes
✅ No JavaScript console errors
✅ UI displays tuition information correctly
✅ Build completes without errors (if rebuild needed)

## Build Commands (if needed)

```bash
# Navigate to Vue app directory
cd wp-content/plugins/jackrabbit-calendar/_vue/jack-2-list-views
npm run build

# Or for other views
cd wp-content/plugins/jackrabbit-calendar/_vue/jack-monthly-calendar-2
npm run build
```

## Resources

- **Plugin Directory:** `wp-content/plugins/jackrabbit-calendar/`
- **API Documentation:** `ai-docs/jackrabbit-calendar/class-listings-md.md`
- **Previous Handoff:** `ai-docs/jackrabbit-calendar/dwi/progress-handoffs/PROGRESS_HANDOFF.md`

---

**Ready to test the billingCycle integration**
