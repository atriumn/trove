# Trove Data Schema

## iClassPro Class Data

Weekly class report pulled from iClassPro.

### JSON Format

```json
{
  "report_date": "2026-01-28",
  "date_range": { "start": "2026-01-26", "end": "2026-02-01" },
  "location": "Ultimate Ninjas Academy Naperville",
  "summary": {
    "total_classes": 55,
    "total_enrollments": 287,
    "capacity": 479,
    "fill_rate": 59.92,
    "total_trials": 23,
    "total_makeups": 10
  },
  "classes": [...]
}
```

### Class Record

```json
{
  "id": 1,
  "name": "Junior Ninjas",
  "schedule": "Mon 4:00PM-4:50PM",
  "program": "Level 4-Junior Ninjas",
  "gender": "C",
  "age_range": "6Y-9Y",
  "max": 7,
  "current": 5,
  "openings": 2,
  "trials": 1,
  "makeups": 0,
  "single_day": 0,
  "price": 130.00
}
```

### Class Levels

| Level | Program Name | Age Range |
|-------|--------------|-----------|
| 1 | Ninja Tots | 2Y-3Y |
| 2 | Mini Ninjas | 3Y-4Y |
| 3 | Lil Ninjas | 3Y-5Y |
| 4 | Junior Ninjas | 6Y-9Y |
| Elite | Elite Team | 6Y-9Y |

Homeschool classes use the same levels with "Homeschool Class" prefix.

## Staff Schedule

Weekly schedule exported from spreadsheet. Currently manual paste (messy format).

### Columns
Days of week: Monday → Sunday

### Data Included
- AM Manager / Front Desk
- PM Manager / Front Desk
- Class times with coaches (1-2 per class)
- Birthday parties

## Birthday Parties

### Fields

| Field | Description |
|-------|-------------|
| day | Day of week |
| time | Party start time |
| honoree | Birthday child's name |
| guest_count | Expected attendees |
| hosts | 1-2 staff members |
| attendees | List of guest names (future) |
| waivers | Waiver completion status (future) |

### Display Format

```
**Saturday Jan 31**
- 1:00 PM: Finn (25 guests) — Ria & Kerrigan
  *(awaiting attendee list for waivers)*
```

When attendee list is available:
```
- 1:00 PM: Finn (25 guests) — Ria & Kerrigan
  ✅ 23/25 waivers signed
```
