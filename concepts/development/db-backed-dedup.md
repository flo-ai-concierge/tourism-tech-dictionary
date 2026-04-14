# DB-Backed Dedup (Persistent Deduplication)

## What it is
Storing processed item IDs in a database table instead of in-memory (RAM). In-memory dedup (a JavaScript `Set()`) is fast but gets wiped every time the server restarts — which happens on every deploy. DB-backed dedup survives restarts because the data is persisted to disk. Best practice: use both layers — in-memory for speed, DB query as a safety net before any action.

## Tourism Translation
**Like a hotel's guest check-in log.** If the front desk keeps the log on a whiteboard (in-memory), it gets erased every shift change and the next shift might check in the same guest twice. If they keep it in the computer system (database), every shift can see who already checked in — no duplicates, no matter how many shift changes happen.

## The three-layer pattern
1. **In-memory cache** — fast first check, skips most duplicates instantly
2. **DB query before action** — hard check right before posting/sending, catches anything the cache missed
3. **DB write after action** — persists the ID so it's known forever (auto-clean after 7 days)

## Why in-memory alone fails
- Server restarts (deploys) clear the Set
- Multiple server instances don't share memory
- Crash recovery loses all tracking
- The 5-minute IMAP overlap window re-fetches recent emails — without persistent dedup, they get re-posted

## Related concepts
- Dedup on conflict — database-level INSERT deduplication
- Deduplication key — choosing the right unique identifier
- Sync state lock — preventing concurrent operations
