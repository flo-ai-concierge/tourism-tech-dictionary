# Sync Window Drift

## What it is
A bug where the "last synced at" timestamp keeps advancing even when no data was actually synced. This happens when the sync process completes "successfully" (no errors) but finds zero results — often because the API was rejecting authentication. The system thinks it's current but it missed everything.

## Tourism translation
Like a night auditor who checks the guest log starting from where they left off last shift. If they accidentally mark "all caught up" without actually reading the log, they'll skip everything that happened. The next auditor trusts that mark and starts even later. Pretty soon, days of activity are invisible.

## When you'd see it
- Incremental sync systems that track a "last synced" timestamp
- Auth failures that return empty arrays instead of error codes
- Days of missing data that nobody notices until a guest complains

## How to prevent it
Only advance the sync timestamp when at least one record was actually processed. If the API returns zero results AND zero errors, hold the timestamp where it is.

## Learned from
QUO sync advanced last_synced_at every 5 minutes during a 24-hour auth break (Apr 15-16, 2026). After fixing the auth, incremental sync skipped all missed messages because the window had moved past them.
