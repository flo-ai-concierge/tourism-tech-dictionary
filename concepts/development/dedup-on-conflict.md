# Dedup / ON CONFLICT

## What it is
A database rule that says "if a row with this unique key already exists, don't insert a new one — either skip or update the existing row." Implemented in PostgreSQL with `INSERT ... ON CONFLICT (key) DO NOTHING` or `DO UPDATE`.

## Tourism Translation
**"Checking the guest list before printing a new key card."**

A guest calls asking for a second key. The front desk checks: is there already a key printed for this room + this guest? If yes, skip. If no, print one. You never end up with two conflicting keys for the same person.

## Why it matters

### Prevents duplicate reviews
Every review we ingest has a `source_id` like `ha_review_38055083`. The column has a `UNIQUE (source, source_id)` constraint. When the sync runs and encounters the same review ID twice, PostgreSQL rejects the second insert automatically. No duplicates, no hand-coded "does this already exist?" check needed.

### Enables safe retries
Because the database handles deduplication, our sync script can be simple: "try to insert everything, the DB will refuse duplicates." Re-running it is free.

### Real FLOHOM example
```sql
INSERT INTO reputation_mentions
  (source, source_id, title, body, ...)
VALUES ($1, $2, $3, $4, ...)
ON CONFLICT (source, source_id) DO NOTHING
RETURNING *;
```
If this INSERT returns 0 rows, the review was already in the database. If it returns 1 row, it's genuinely new. We fire the Slack post only when `rowCount > 0`, guaranteeing one Slack card per review forever.

### Without it, you need manual dedup
Without `ON CONFLICT`, you'd have to do two queries: first SELECT to check if the row exists, then INSERT if it doesn't. That's slow AND has a race condition — two concurrent syncs could both see "doesn't exist" at the same time and both insert, producing duplicates.

## In simpler terms
It's the front desk asking "have we already checked this guest in?" before handing them a room key. If yes, don't charge them a second time. If no, proceed.
