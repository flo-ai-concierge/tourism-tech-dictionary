# One-Way Sync

## What it is
Data flows in one direction only. In FLOHOM's guidebook system, content is edited in Airtable and pushed to the app's database — but edits made in the app don't push back to Airtable. Airtable is the "source of truth" and the app is the consumer.

## Tourism translation
Like a housekeeping checklist that HQ prints and distributes to cleaners at each property. Cleaners follow the checklist, but any changes to the checklist come from HQ only. If a cleaner writes a note on their copy, it doesn't update the master at HQ.

## When you'll encounter it
- Airtable guidebooks syncing to PostgreSQL every 15 minutes
- Airtable services syncing to the upsell_services table
- Any system where one side is the "editor" and the other is the "reader"

## How it works
```
Airtable (edit here)
    --> Sync job (every 15 min)
        --> PostgreSQL (read from here)
            --> Guest pages, FLO concierge, Admin UI
```

## Why not two-way?
Two-way sync creates conflicts: if someone edits in Airtable AND someone edits in the app at the same time, which one wins? One-way avoids this entirely. One place to edit, one source of truth.

## Related concepts
- [Cron / Scheduled Sync](./cron-scheduled-sync.md) — the timing mechanism
- [Sync State Lock](./sync-state-lock.md) — preventing overlapping syncs
