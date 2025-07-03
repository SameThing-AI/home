# Implement Automatic Weekly Hours Calculation in Archive

## Problem
Currently, the weekly hours worked in the archive page (`archive.md`) are hardcoded values. This requires manual updates every time new blog posts are added and doesn't scale well.

## Current Implementation
```liquid
<!-- Hardcoded weekly hours - TODO: Calculate automatically -->
{% assign week_start_date = post.date | date: "%Y-%m-%d" %}
{% if week_start_date >= "2025-06-24" and week_start_date <= "2025-06-27" %}
  {% assign week_hours = 40.2 %}
{% elsif week_start_date >= "2025-06-30" and week_start_date <= "2025-07-02" %}
  {% assign week_hours = 20.5 %}
{% endif %}
```

## Desired Solution
Implement automatic calculation that:
1. Parses `time started` and `time ended` fields from each post's front matter
2. Handles AM/PM time format conversion to 24-hour format
3. Calculates duration for each day, including overnight sessions
4. Sums up total hours per week
5. Displays the calculated total in the weekly hours badge

## Technical Requirements
- Parse time fields with spaces in YAML keys: `post["time started"]` and `post["time ended"]`
- Handle time formats like "11:02 PM" and "4:06 PM"
- Convert to 24-hour format for calculations
- Handle overnight sessions (when end time is before start time, add 24 hours)
- Sum hours across all posts in each week

## Files to Modify
- `archive.md` - Replace hardcoded values with calculation logic

## Acceptance Criteria
- [ ] Weekly hours are calculated automatically from post data
- [ ] Handles AM/PM time format correctly
- [ ] Correctly calculates overnight sessions
- [ ] No manual updates needed when adding new posts
- [ ] Maintains current visual design and layout
- [ ] Shows decimal hours (e.g., "40.2h worked")

## Priority
Medium - Current hardcoded solution works but needs maintenance

## Labels
- enhancement
- technical-debt
- archive-page
