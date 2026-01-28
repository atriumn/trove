# Query Patterns

Common queries against Trove data.

## Display Conventions

- **Always chronological ascending**: Mon → Tue → Wed → Thu → Fri → Sat → Sun
- **Within same day**: Sort by time ascending
- **Counts**: Include totals where useful

## jq Examples

These work against the raw JSON files.

### Trials This Week

```bash
jq -r '.classes[] | select(.trials > 0) | "- \(.name) (\(.schedule | split("-")[0])): \(.trials) trial(s)"' data.json
```

### Openings by Class Type

```bash
jq -r '.classes[] | select(.openings > 0) | "\(.program)\t\(.openings)\t\(.schedule | split("-")[0])"' data.json \
  | sort -t$'\t' -k1,1 -k2,2rn
```

### Classes for Specific Level

```bash
jq -r '.classes[] | select(.program | test("Junior")) | "\(.schedule): \(.openings) open"' data.json
```

### Chronological Sort (by day of week)

```bash
jq -r '.classes[] | select(.openings > 0) | "\(.schedule | split(" ")[0])\t\(.schedule)\t\(.openings)"' data.json \
  | awk -F'\t' 'BEGIN {d["Mon"]=1;d["Tue"]=2;d["Wed"]=3;d["Thu"]=4;d["Fri"]=5;d["Sat"]=6;d["Sun"]=7} {print d[$1]"\t"$0}' \
  | sort -t$'\t' -k1,1n | cut -f2-
```

## SQL Examples

Once data is in SQLite:

### Trials This Week

```sql
SELECT name, schedule, trials
FROM classes
WHERE report_id = (SELECT MAX(id) FROM reports)
  AND trials > 0
ORDER BY 
  CASE substr(schedule, 1, 3)
    WHEN 'Mon' THEN 1 WHEN 'Tue' THEN 2 WHEN 'Wed' THEN 3
    WHEN 'Thu' THEN 4 WHEN 'Fri' THEN 5 WHEN 'Sat' THEN 6 WHEN 'Sun' THEN 7
  END,
  schedule;
```

### Fill Rate by Program

```sql
SELECT program,
       SUM(current) as enrolled,
       SUM(max) as capacity,
       ROUND(100.0 * SUM(current) / SUM(max), 1) as fill_rate
FROM classes
WHERE report_id = (SELECT MAX(id) FROM reports)
GROUP BY program
ORDER BY fill_rate DESC;
```

## Natural Language → Query

When user asks... | Query this
------------------|------------
"trials this week" | classes where trials > 0
"openings in Junior Ninjas" | classes where program contains "Junior" and openings > 0
"what's full" | classes where openings <= 0
"Saturday classes" | classes where schedule starts with "Sat"
"birthday parties this weekend" | parties on Sat/Sun of current week
