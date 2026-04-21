# Idempotent Migration

## What it is
A database schema change (or data import) that can safely run multiple times without breaking anything or producing different results. The first run creates the thing; every subsequent run is a no-op. Same end state every time.

## Tourism translation
A standing instruction to housekeeping: *"Refill the mini-bar to capacity."*

If the mini-bar is empty, they fill it. If it's already full, they do nothing. You can give that instruction every morning for a year and the mini-bar never gets double-stocked or knocked empty. That's idempotent.

Compare to a non-idempotent instruction: *"Add 3 bottles of water to the mini-bar."* Run that every morning and by Friday the guest has 15 bottles.

## When you'd see it
- Database migrations: `CREATE TABLE IF NOT EXISTS`, `ADD COLUMN IF NOT EXISTS`, `CREATE INDEX IF NOT EXISTS`
- One-time data seeds: `INSERT ... ON CONFLICT DO NOTHING`
- Deploy scripts that run on every server boot
- Syncs that might be triggered twice by accident

## Why it matters
Production deploys rerun migrations every time the server restarts. If the migration script errors on "table already exists," every deploy after the first one crashes. Idempotent migrations just silently succeed the second time and move on.

It also lets you **run the same script on local dev, staging, and production** without special-casing each environment — they all converge to the same end state regardless of starting state.

## The SQL patterns
```sql
-- Safe to run repeatedly
CREATE TABLE IF NOT EXISTS marinas (...);

ALTER TABLE marinas ADD COLUMN IF NOT EXISTS priority_rank TEXT;

CREATE INDEX IF NOT EXISTS idx_marinas_status ON marinas(status);

-- Dangerous: NOT idempotent
ALTER TABLE marinas ADD COLUMN priority_rank TEXT;  -- errors second time
```

## Idempotent data seeds
```sql
-- Safe to rerun
INSERT INTO admin_users (email, role)
VALUES ('reservations@flohom.com', 'admin')
ON CONFLICT (email) DO NOTHING;

-- Also safe
INSERT INTO ... ON CONFLICT ... DO UPDATE SET ...;
```

## Gotchas
- `IF NOT EXISTS` only checks *existence* — if the column is there but with a different type, the migration silently skips it. Add explicit type-change migrations when needed.
- Deleting isn't automatically idempotent. `DROP TABLE IF EXISTS` is safe; plain `DROP TABLE` errors the second time.
- Data migrations (backfilling values) need careful thought: "UPDATE every row where X is null" is idempotent — the second run finds zero matching rows and updates nothing.

## Learned from
FLOHOM instrumentation.js (multiple sessions including Apr 20, 2026). Every migration is wrapped in `CREATE TABLE IF NOT EXISTS` / `ADD COLUMN IF NOT EXISTS` / `CREATE INDEX IF NOT EXISTS`. Render restarts the server on every deploy — the migrations run every time and never fail. When we added the 5 marina tables, we didn't need a migration framework or version tracking — the idempotent statements just skip already-applied changes.
