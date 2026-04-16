# Idempotent Operation

## What it is
An operation that produces the same result no matter how many times you run it. Running it once or ten times has the exact same effect. In databases, `INSERT ... ON CONFLICT DO NOTHING` is the classic example — if the record already exists, it silently skips instead of creating a duplicate.

## Tourism translation
Like scanning your boarding pass at the gate. Scanning it once checks you in. Scanning it 5 more times doesn't book you 5 extra seats or charge you 5 times. It just confirms you're already checked in.

## When you'd see it
- Sync engines that might process the same data twice (network retries, overlapping runs)
- Webhook handlers that receive duplicate events
- Any operation where "retry safely" is important
- Database inserts with unique constraint handling

## Why it matters
Without idempotency, retrying a failed sync could create duplicate messages, double-charge payments, or send the same notification twice.

## Learned from
All QUO message and call sync uses ON CONFLICT (external_id) DO NOTHING — safe to re-run full syncs any number of times without creating duplicates.
