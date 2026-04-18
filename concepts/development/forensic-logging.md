# Forensic Logging

## What it is
Adding extra log statements to your code specifically designed to capture evidence the next time a bug happens — so when it does, you have the data to diagnose without guessing. Different from regular logging: forensic logs are added BECAUSE you're debugging a recurring intermittent bug. They often get removed once the bug is solved.

## Tourism translation
**Installing a security camera at the loading dock for one week.**

Inventory keeps shrinking but no one knows why or when. Instead of changing locks, accusing staff, or installing alarms blind — you put up a camera. For a week, it records everything. The next time inventory shrinks, you have video. Now you can SEE who, when, what, and why. Then you fix the actual cause.

After the bug is solved, you might take the camera down (or leave it for general security).

## What forensic logs should capture
For each failure-prone operation, log:
- The exact inputs received (not summarized — full)
- Intermediate values your code computed
- The decision branch that was taken
- A correlation ID so you can trace one event end-to-end across logs
- Wall-clock timestamp with millisecond precision

For dedup or race-condition bugs specifically:
- The dedup key being checked
- Whether the check passed or failed
- The process ID (`pid`) that did the check
- The DB query result (e.g., `rowCount = 0` vs `rowCount = 1`)

## When you'd see it
- A bug that "sometimes" happens but you can't reproduce locally.
- Race conditions in concurrent systems.
- Dedup that "should work" but duplicates appear in production.
- AI outputs that occasionally go off-script.

## Why it matters
We tried to fix a Minut duplicate-posts bug NINE times in four days. Each fix was based on a guess about the cause. None worked. The breakthrough came when we considered: "we've been guessing — let's add forensic logs that will capture the next duplicate's full context (subject, message ID, envelope time, parsed type, computed bucket, lock acquisition result), then look at the data."

The right next step on a recurring bug is rarely a 10th fix attempt. It's evidence collection.

## What to remove later
Once the bug is found and fixed, remove the forensic logs (they add noise to production logs). KEEP the structural lessons — the correlation IDs, the operation summaries — but drop the verbose per-step traces.

## Learned from
FLOHOM Minut scanner (Apr 14–18, 2026). After 9 failed iterative fixes, switched to forensic-logging-first approach. Found the actual root cause (timezone bug + multi-email-per-event from the sender) within one debugging cycle.

## Related concepts
- [`development/race-condition`](race-condition.md) — common bug class that forensic logs catch
- [`infrastructure/deploy`](../infrastructure/deploy.md) — important to know what version emitted each log
