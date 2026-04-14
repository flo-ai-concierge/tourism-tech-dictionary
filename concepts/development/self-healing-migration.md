# Self-Healing Migration

## What it is
Code that automatically detects and fixes missing database columns, tables, or data on application startup — without requiring manual intervention. Uses `ALTER TABLE ... ADD COLUMN IF NOT EXISTS` or `CREATE TABLE IF NOT EXISTS` patterns so the app repairs itself on every deploy. If the column already exists, the command does nothing. If it's missing, it gets created automatically.

## Tourism Translation
**Like a hotel that does a facilities check every morning before opening.** If the lobby TV is missing, maintenance installs a new one before guests arrive. If it's already there, they move on. The hotel never opens with broken facilities because the morning checklist catches and fixes everything automatically — no manager needs to remember or intervene.

## Why it matters
- Local development databases and production databases drift apart over time
- Schema files define what SHOULD exist, but migrations define what DOES exist
- Self-healing migrations close the gap — the app fixes itself on boot
- Prevents "column does not exist" errors that break features in production while working locally

## Pattern (in instrumentation.js)
```sql
ALTER TABLE conversations ADD COLUMN IF NOT EXISTS waiting_since TIMESTAMPTZ;
ALTER TABLE conversations ADD COLUMN IF NOT EXISTS first_reply_at TIMESTAMPTZ;
ALTER TABLE messages ADD COLUMN IF NOT EXISTS external_id TEXT;
```

## Related concepts
- Database migration — structured schema changes
- Deploy — pushing code to production
- Idempotent operations — safe to run multiple times
