# Adjacent Reservation Awareness

## What it is
Giving an AI concierge visibility into the reservations immediately before and after a guest's stay on the same property. When a guest asks about early arrival, late checkout, early parking, or early access, the AI checks the adjacent bookings first — if there's a same-day turnover, it hedges instead of promising.

## Tourism Translation
**A concierge glancing at the previous night's departure list before answering "can I drop my bags off at 11 AM?"**

A good hotel concierge doesn't say "absolutely!" the moment a guest asks about early access. They glance at the room status board: is the previous guest still checked in? Is housekeeping in the room? If yes to either, they say "let me check — I don't want to send you up while someone's still there." That glance — that awareness of who's in the room before AND after — is what separates a great concierge from one that overpromises and disappoints.

## Why it matters
Without adjacent reservation awareness, FLO (or any AI concierge) has a blind spot. It sees the guest's own reservation — check-in Apr 26, check-out Apr 27 — and nothing else. When that guest asks "can I arrive early and park?", FLO confidently says yes, because from its point of view, the guest's spot is obviously theirs.

But that spot belongs to the PRIOR guest until their checkout at 10 AM. And after 10 AM, housekeeping needs until 3 PM to turn the unit over. The AI had no way to see any of this — until we started loading adjacent reservations into its brief.

## How it works in FLOHOM
Before FLO generates a reply, the system runs two small SQL queries:
- **Prior reservation**: check_out on or before this guest's check_in, within 3 days
- **Next reservation**: check_in on or after this guest's check_out, within 3 days

The results get formatted into a "TURNOVER CONTEXT" block in the FLO Brief. If either adjacent reservation is same-day, the block gets flagged "NOT guaranteed" and FLO is instructed to hedge.

## Related concepts
- [Turnover](../operations/turnover.md) — the operational event
- [Tight Turnover Warning](../operations/tight-turnover-warning.md) — the flag itself
- [Hedge-Don't-Promise Pattern](hedge-dont-promise-pattern.md) — the language rule this enables
- [Context Injection](context-injection.md) — the broader pattern of pre-loading data into the AI
