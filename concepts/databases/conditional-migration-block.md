---
term: Conditional Migration Block (DO $$ ... $$)
category: databases
session: FLOTurn Phase 1 — May 2026
---

## Plain English

A block of SQL code that checks whether something exists **before changing it**, so the migration is safe to run multiple times. It asks "does column X still exist?" before trying to rename or drop it. This prevents the migration from crashing if it's been partially run before, or run on different environments with different states.

## Tourism / Hospitality Analogy

A maintenance contractor who checks "is the lock already replaced?" before installing a new one. They won't remove a perfectly good lock just because the work order says "install lock" — they verify the current state first, then act only if needed.

## Technical Detail

```sql
DO $$
BEGIN
  -- Only run this if the OLD column still exists
  IF EXISTS (
    SELECT 1 FROM information_schema.columns
    WHERE table_name = 'cleaning_tasks' AND column_name = 'photo_url'
  ) THEN
    -- Migrate data
    UPDATE cleaning_tasks
       SET photo_urls = ARRAY[photo_url]
     WHERE photo_url IS NOT NULL;
    -- Remove old column
    ALTER TABLE cleaning_tasks DROP COLUMN photo_url;
  END IF;
END $$;
```

## Why It Matters

Without this guard, running a migration twice would crash: "column photo_url does not exist." With the guard, it's idempotent — safe to run on prod, staging, and local with no ill effects regardless of what state each environment is in.
