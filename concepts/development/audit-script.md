# Audit Script (Diagnostic Pattern)

## What it is
A small, throwaway script that changes nothing — it just reports what's true about a system. Used to ground a debugging conversation in real data instead of assumptions. Runs in seconds, prints a clean report, exits.

The opposite of a fix. You write the audit script BEFORE you write the fix, so the fix targets the actual problem.

## Tourism Translation
**Walking the property at 8 AM with a clipboard.**

Before any decision-making, the property manager does the morning walk. Lights on or off? Doors locked? Trash to pick up? Damage from last night's storm? Pool chemicals at spec?

Nothing changes. No tools come out. The clipboard is just observation. By the time she sits down at her desk at 9, she has the actual state of the property — not what she assumed last night before going to bed.

Decisions made from the morning walk are 10x better than decisions made from yesterday's clipboard.

## Why it matters
Most production debugging fails because the team is debating theories without ground truth. "I think the cron is broken." "I think the API changed." "I think the data is stale." These are all hypotheses. None of them are evidence.

An audit script ends the debate by showing the actual state. Then the fix is obvious.

## How it played out on Apr 22, 2026
Two audits saved the day:

1. **`scripts/debug-daily-schedule.js`** — Josh said "MB market shows no activity but there's a turnover." We could've spent an hour theorizing why. Instead the audit script ran the cron's exact logic for Apr 26 and showed: every property's activity per market + the exact Slack message each channel WOULD post + a 🚩 flag on FLOHOM 15 because it had real bookings but was filtered out by `status: "upcoming"`. The fix took 1 line.

2. **`scripts/audit-flohom-15.js`** — After flipping FLOHOM 15 to active, we needed to know if the underlying data was complete. The audit checked 5 systems (FLOEx steps, upsell products, FAQ Bank, Airtable record, Hostaway listing) and printed ✅ / ⚠️ / ❌ per system. Revealed: the production DB still had `status: "upcoming"` even though the code was fixed. Also revealed: the Airtable lookup was failing because the Official Link didn't contain the listingId.

Without the audits, both fixes would've been guesses. With them, the fix path was obvious in 30 seconds.

## Pattern: what makes a good audit script
1. **Read-only by default** — no writes unless explicitly flagged (e.g., `--fix-status`)
2. **Touches every system** — pull from DB, API, files, external services in one pass
3. **Outputs ✅ / ⚠️ / ❌ per check** — emoji status that scans visually in 5 seconds
4. **Includes specific next-step hints** — not just "missing data" but "add row to Airtable FLOHOM table"
5. **Idempotent** — safe to run repeatedly during debugging

## When to write one
- Anytime you're about to spend more than 15 minutes debugging
- Any time someone reports "X looks wrong" and you don't have direct visibility into X's underlying data
- Before any major migration (audit before, audit after — diff the reports)
- When onboarding a new team member to a complex system (the audit becomes the "system tour")

## Related concepts
- [Audit Note](audit-note.md) — different pattern; audit-NOTE is a logging convention, audit-SCRIPT is a runtime diagnostic
- [Idempotent Operations](idempotent-operations.md) — audit scripts MUST be idempotent
- [Stale Refactor Trap](stale-refactor-trap.md) — audit scripts are how you detect this without running production
