# Lookback Window

## What it is
The time range a sync, scan, or query looks backward into when pulling data. "Last 24 hours," "last 7 days," "last 60 days" — all lookback windows. Too narrow and you miss data. Too wide and you do unnecessary work.

## Tourism Translation
**"Reviewing the last 60 days of arrivals when preparing your monthly report."**

You wouldn't pull every reservation since 2023 just to write this month's occupancy report. You also wouldn't pull only yesterday's — you'd miss 29 days. You pull a sensible window that catches everything you need without drowning in history.

The trick is picking the right window for the right question.

## Why it matters

### Too narrow = silent data loss
This is the bug that bit us. Our review sync used a 1-day lookback off `last_synced_at`. It asked Hostaway "give me reviews for stays that departed in the last day." But Hostaway filters by *departure date*, not *review submission date*, and guests routinely take 2-7 days to write reviews. Any review submitted for a stay that checked out more than 1 day before the sync ran was silently dropped.

### Too wide = wasted work
Pulling 5 years of reviews every hour is possible but pointless. Most of those reviews are already in our DB and get rejected by `ON CONFLICT`. You're paying for API calls, CPU, and database work to confirm nothing new happened in old data.

### The sweet spot is "wider than your delay pattern"
For reviews, guests have up to 14 days on Airbnb to post. Add a safety margin and you get 30-60 days as the right window. We chose 60 — any review submitted for a stay in the last two months will always be caught.

### Real FLOHOM example
```js
// BEFORE (buggy):
const sinceDate = lastSync
  ? new Date(new Date(lastSync).getTime() - 24 * 60 * 60 * 1000)  // 1 day — too narrow
  : new Date(Date.now() - 5 * 365 * 24 * 60 * 60 * 1000);

// AFTER (fixed):
const MIN_LOOKBACK_MS = 60 * 24 * 60 * 60 * 1000; // 60 days
const sinceDate = lastSync
  ? new Date(Date.now() - MIN_LOOKBACK_MS)
  : new Date(Date.now() - 5 * 365 * 24 * 60 * 60 * 1000);
```
The fix cost us nothing — dedup via `ON CONFLICT` means the wider window doesn't produce duplicates. We just catch more of what we should have been catching all along.

## In simpler terms
It's the difference between glancing over your shoulder (you miss the car behind you) and turning fully around (you see clearly). Pick a window wide enough to see what matters.
