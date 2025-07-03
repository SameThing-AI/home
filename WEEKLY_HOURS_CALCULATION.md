# Implement Automatic Weekly Hours Calculation

**Problem:** Weekly hours in archive page are currently hardcoded and need manual updates.

**Current Situation:**
- Hours are hardcoded: Week 1 = 28.2h, Week 2 = 20.5h
- Requires manual calculation and code updates for each new week

**Desired Solution:**
- Automatically parse `time started` and `time ended` from post front matter
- Calculate daily hours worked and sum by week
- Handle AM/PM format and overnight sessions
- Display calculated totals in archive badges

**Technical Details:**
- Parse YAML fields with spaces: `post["time started"]`
- Convert "11:02 PM" format to 24-hour calculations  
- Handle cross-midnight sessions (11:02 PM to 4:06 PM next day)
- Sum hours across all posts per week

**Files:** `archive.md`

**Priority:** Medium (current solution works but needs maintenance)
