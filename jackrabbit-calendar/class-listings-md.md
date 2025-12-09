# Jackrabbit Calendar - Class Listings API Response

This document describes the API response structure for class listings from the Jackrabbit API.

---

## API Response Structure

```json
{
  "rows": [
    {
      "id": 20616413,
      "category1": "Advantage Academy",
      "category2": "DK Composite",
      "category3": "In School Location Owner Registration",
      "description": "...",
      "end_date": "2026-05-12",
      "end_time": "16:35",
      "gender": "All",
      "instructors": [],
      "location": "FLG",
      "location_code": "FLG",
      "location_name": "South Hillsborough County",
      "master_class": false,
      "max_age": "P11Y11M",
      "meeting_days": {
        "mon": false,
        "tue": true,
        "wed": false,
        "thu": false,
        "fri": false,
        "sat": false,
        "sun": false
      },
      "min_age": "P05Y0M",
      "name": "Advantage Academy - Creative Dramatics",
      "online_reg_link": "https://app.jackrabbitclass.com/reg.asp?id=521613&hc=&initEmpty=&hdColor=&wl=0&preLoadClassID=20616413&loc=",
      "openings": {
        "calculated_openings": 16
      },
      "days": {
        "mon": 0,
        "tue": 0,
        "wed": 0,
        "thu": 0,
        "fri": 0,
        "sat": 0,
        "sun": 0
      },
      "reg_start_date": "2025-06-16",
      "room": "Plant City - Advantage Academy 304 W Prosser Dr, Plant City, FL 33563",
      "session": "2025-2026",
      "start_date": "2026-01-13",
      "start_time": "15:05",
      "waitlist": false,
      "location_addr1": "",
      "location_addr2": "",
      "location_city": "",
      "location_state": "",
      "location_postalcode": "",
      "location_phone": "",
      "tuition": {
        "billingCycle": "By Session Dates",
        "fee": 99,
        "days": {
          "day_1": 0,
          "day_2": 0,
          "day_3": 0,
          "day_4": 0,
          "day_5": 0,
          "day_6": 0,
          "day_7": 0
        }
      }
    }
  ]
}
```

---

## Tuition Billing Cycle

The `tuition.billingCycle` field indicates how tuition is charged:

| Value | Description |
|-------|-------------|
| `"Monthly"` | Tuition is paid monthly (recurring payment) |
| `"By Session Dates"` | Tuition amount is for the whole session (one-time payment) |

### Usage in Plugin

The `isClassRecurring()` method in `_vue/shared/mixins/JackrabbitData.js` uses this field:

```javascript
isClassRecurring(row) {
    if (row.tuition && row.tuition.billingCycle) {
        const billingCycle = row.tuition.billingCycle.toLowerCase();
        return billingCycle === 'monthly';
    }
    return false;
}
```

- Returns `true` for "Monthly" billing (recurring)
- Returns `false` for "By Session Dates" (one-time)

---

## Sample Class Data

### Class 1: Advantage Academy - Creative Dramatics

| Field | Value |
|-------|-------|
| **ID** | 20616413 |
| **Category** | Advantage Academy |
| **Type** | DK Composite |
| **Location** | In School Location Owner Registration |
| **Start Date** | 2026-01-13 |
| **End Date** | 2026-05-12 |
| **Start Time** | 15:05 |
| **End Time** | 16:35 |
| **Meeting Days** | Tuesday only |
| **Age Range** | 5-11 years |
| **Fee** | $99 |
| **Billing Cycle** | By Session Dates |
| **Openings** | 16 |

### Class 2: Apollo Beach Elementary

| Field | Value |
|-------|-------|
| **ID** | 20252960 |
| **Category** | Apollo Beach Elementary |
| **Type** | DK Composite |
| **Location** | In School Location Owner Registration |
| **Start Date** | 2026-01-13 |
