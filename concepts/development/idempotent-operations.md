# Idempotent Operations

## What it is
An operation that produces the same result no matter how many times you run it. Running it once or running it ten times gets you to the exact same state. Safe to retry.

## Tourism Translation
**"Re-printing the same boarding pass doesn't create two reservations."**

The guest loses their FLOEx Pass. You click "Resend." They get a new PDF. Same reservation ID, same QR code, same check-in instructions. The system doesn't duplicate the booking, charge them twice, or fire off a second housekeeping alert. You could click "Resend" a hundred times and nothing downstream breaks.

That's idempotent.

## Why it matters

### Retries become safe
If a sync fails halfway through, you can just run it again without worrying about creating duplicates. Our `syncHostawayReviews()` uses `ON CONFLICT (source, source_id) DO NOTHING`, so re-running it is free: existing reviews are no-ops, only new ones get inserted.

### Webhooks can fire twice
Every external service (Hostaway, Slack, Stripe) occasionally sends the same webhook twice due to network retries. If your handler isn't idempotent, you end up with duplicate reservations, double-billed guests, or double Slack posts. Idempotency is non-negotiable for webhook receivers.

### Real FLOHOM example
When we ran the Slack backfill of 1,024 reviews and it crashed halfway, we could simply re-run it. The backfill endpoint reads from `reputation_mentions`, the hook fires `postReviewToSlack` for each, and Slack happily posts them. If we'd already posted some, we'd have duplicates in Slack — so the cleanup script used `chat.delete` (also idempotent: deleting an already-deleted message is a no-op) to clear the channel before re-running.

### The opposite is scary
Non-idempotent operations are things like "charge the guest's card." You REALLY don't want to run that twice. Those operations need explicit dedup keys (e.g., `idempotency_key` in Stripe) to make them safe.

## In simpler terms
Pressing an elevator call button. It doesn't matter if you press it once or twenty times. The elevator comes once.
