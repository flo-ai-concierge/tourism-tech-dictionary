# Race Condition

## What it is
A bug that happens when two processes try to do the same thing at the same time and the outcome depends on which one finishes first. The result is unpredictable and often wrong.

## Tourism Translation
**"Two front-desk agents both booking the same suite for the same night."**

Agent A pulls up FLOHOM 7 on the booking system. Agent B, on a different computer 30 seconds later, also pulls up FLOHOM 7. Both see "available." Both click "Confirm Booking" within seconds of each other. Now there are two confirmations for the same night in the same property, and somebody's vacation is ruined.

Neither agent did anything wrong individually. The bug is that the system let both of them operate on the same resource at once without a check.

## Why it matters

### Bulk operations need protection
During the Slack backfill, two processes were racing each other: one was posting 1,024 review cards, another was trying to delete the same messages. Whichever one grabbed the channel history first "won" that pass, and it took several rounds of cleanup to fully settle.

### The classic symptoms
- Count doesn't decrease even when you're deleting things (something else is adding)
- The same ID gets processed twice
- State flips back and forth unexpectedly
- Tests pass but production breaks randomly

### How to prevent it
1. **Locks** — mark the resource as "in use" so nothing else can touch it
2. **Idempotent operations** — design the operation so running it twice has no extra effect
3. **Unique constraints** — let the database enforce uniqueness, not application code
4. **Queue, don't parallelize** — sometimes it's cheaper to process things one at a time

### Real FLOHOM example
When our Slack backfill handler ran on Render and someone hit the "Test Slack 3" button at the same time, both POST handlers started posting to the same channel. Messages interleaved wrong, counts went haywire. Fix: force a Render redeploy to kill all in-flight handlers, clean up the channel, then run exactly one backfill end-to-end.

## In simpler terms
Two people reaching for the last slice of pizza at the same time. Whoever's hand moves faster gets it. The winner depends entirely on reflexes, not on who deserves it.
