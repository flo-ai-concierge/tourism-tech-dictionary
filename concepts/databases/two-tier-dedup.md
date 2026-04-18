# Two-Tier Deduplication

## What it is
Two layered dedup checks instead of one. Layer 1 asks "have I seen this exact RECORD before?" (per-row). Layer 2 asks "have I already done this real-world ACTION?" (per-event). Either check can catch a duplicate. You need both because they catch different failure modes — Layer 1 misses cases where the same event arrives as multiple records, and Layer 2 misses cases where the same record gets re-processed.

## Tourism translation
**Two checks at the front desk before a guest gets a room key.**

Layer 1 — "Have I scanned this exact passport already today?" Catches the case where the same guest hands you their passport twice in one shift.

Layer 2 — "Has someone already checked into Room 305 this afternoon?" Catches the case where the same guest comes back with their friend's passport, OR where two siblings show up separately to claim the same booking.

Either check on its own misses something. Together, they prevent every double check-in.

## When you'd see it
- Email scanners: a sender (like Minut sensors) might dispatch two emails for the same physical event with different message IDs. Per-email dedup misses it; per-event dedup catches it.
- Webhook receivers: the same event can fire from multiple sources or get retried.
- Sync engines: the same record can arrive from a webhook AND a polled API in the same window.

## Why it matters
We hit this in the FLOHOM Minut sensor pipeline. Minut sometimes sent two emails for the same noise event with slightly different message IDs. Our messageId-only dedup let both pass, both posted to Slack. Adding an event-level claim (`property + event_type + 5-min-window`) as Layer 2 collapsed them — only the first email wins the lock and posts; the others quietly skip.

## How it's implemented
Both layers store keys in the same dedup table:

- Layer 1 keys: the raw `messageId` or unique record ID.
- Layer 2 keys: a synthetic key like `evt:property7_noise_10_2960795`.

When processing a record:
1. Check messageId in dedup table → skip if seen.
2. Compute event signature → atomic INSERT ON CONFLICT DO NOTHING.
3. If insert returned 0 rows, another record already claimed this event → skip and mark this messageId so we don't re-evaluate.
4. If insert succeeded, post the action.
5. After successful post, mark messageId too.
6. If post fails, RELEASE the event claim so a retry can happen on the next scan.

## Learned from
FLOHOM Minut → Slack pipeline (Apr 18, 2026). Spent 9 commits trying to fix duplicate Slack posts with one-tier dedup. The two-tier pattern with atomic event claim plus release-on-failure was what finally killed the duplicates for good.

## Related concepts
- [`databases/idempotent-operation`](idempotent-operation.md) — the underlying SQL pattern
- [`development/dedup-on-conflict`](../development/dedup-on-conflict.md) — atomic INSERT ON CONFLICT
- [`development/db-backed-dedup`](../development/db-backed-dedup.md) — why dedup must persist across restarts
- [`apis/canonical-dedup-key`](../apis/canonical-dedup-key.md) — designing the key
