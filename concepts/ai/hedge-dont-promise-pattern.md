# Hedge-Don't-Promise Pattern

## What it is
A language rule for AI concierges: when the answer to a guest's question depends on something outside the AI's control (another guest's movement, housekeeping progress, weather, third-party confirmation), the AI must hedge — "we can try", "not guaranteed", "let me check" — instead of giving a confident green-light like "absolutely yes" or "of course".

## Tourism Translation
**The difference between a front desk clerk saying "your suite's ready!" vs. "let me check — I don't want to send you up while housekeeping is still in there."**

One promises. One verifies. Guests remember the promise that failed far more than the verification that took an extra 30 seconds. The art of hospitality is warm language + realistic commitment — you can be kind without overpromising.

## Why it matters
AI concierges default to friendly, enthusiastic language. "Absolutely!" "Of course!" "Come anytime!" That tone is perfect for questions the AI actually controls (sending a booking link, explaining a policy, confirming an amenity). It's DANGEROUS for questions that depend on other guests, staff schedules, or weather.

Real incident (Apr 2026): Guest Sue Rineer asked if she could arrive early and use the parking spot. FLO said "Yes, you are absolutely welcome to use your parking spot at the marina before check-in." But another guest was checking out that same morning at 10 AM, and housekeeping ran until 3 PM. If Sue had arrived at 9 AM, the spot would've been occupied and she would've been stranded.

## The rule
When the AI sees a "NOT guaranteed" flag in its context (e.g. from a TURNOVER CONTEXT block), it must:
- Acknowledge the request warmly
- Explain the reason it's not guaranteed (prior guest still there, housekeeping window)
- Offer a reasonable alternative (shop first, then check in at the regular time)
- Optionally offer a paid add-on with an explicit hedge ("we can try, but it's not guaranteed on back-to-back days")
- Never promise something that depends on another person's movement

## Related concepts
- [Adjacent Reservation Awareness](adjacent-reservation-awareness.md) — the data that enables the hedge
- [Trust Gate](trust-gate.md) — the broader principle of not overcommitting
- [Em-dash AI Tell](em-dash-ai-tell.md) — another AI-language quirk worth managing
