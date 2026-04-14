# Incremental Sync (with Early-Stop)

## What it is
Instead of re-syncing ALL data from an external API every time (full sync), incremental sync only fetches data that changed since the last sync. The "early-stop" pattern sorts results by most recent activity and stops processing once it reaches records older than the last sync timestamp. This turns a 7,000-record scan into a ~50-record update.

## Tourism Translation
**Like a hotel night auditor who only reviews today's transactions instead of re-auditing every transaction since the hotel opened.** They start with the most recent charges, work backwards, and stop when they reach yesterday's closing balance. If they re-audited everything every night, they'd never finish their shift.

## Why it matters
- APIs that don't support `modifiedSince` filtering (like Hostaway conversations) require creative solutions
- Full syncs of 7,000+ records can take 30+ minutes and crash mid-run
- Incremental syncs with early-stop complete in seconds
- A hard timeout (e.g., 4 minutes) prevents runaway syncs from blocking the system

## Pattern
1. Sort API results by `latestActivityDesc` (newest first)
2. Track `lastSyncAt` in the database
3. Process each page of results
4. When you hit a record older than `lastSyncAt` → stop
5. Update `lastSyncAt` to now

## Related concepts
- Sync state lock — preventing concurrent sync runs
- Cron scheduled sync — periodic background execution
- Pagination (load more) — fetching data in pages
