# Sync State Lock

## What it is
A flag in the database that marks whether a sync process is currently "running" or "idle." It prevents two copies of the same sync from running simultaneously. The danger: if the process crashes mid-run without resetting the flag to "idle," no future syncs can start — the system thinks one is still running.

## Tourism translation
Like a hotel room's "Do Not Disturb" sign. When housekeeping sees it, they skip the room. But if a guest checks out and forgets to remove the sign, that room never gets cleaned — it just sits there untouched while the front desk wonders why it's never available. A stuck sync state lock is that forgotten DND sign blocking the whole operation.

## When you'll encounter it
- Automated data syncs that run on a timer (every 60 seconds, every hour)
- Background jobs that should never overlap (importing reservations, syncing messages)
- Any cron job where running two instances simultaneously would cause duplicate data

## Related concepts
- Cron jobs — scheduled tasks that run automatically
- Idempotency — making operations safe to run multiple times
- Dead letter queues — handling jobs that fail and need retry
