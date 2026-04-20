# Tight Turnover Warning

## What it is
A flag raised by the system when a property has back-to-back guest movements within the same housekeeping window — i.e. one guest checks out at 10 AM and another checks in at 3 PM on the same day (or one day's gap). The warning tells both staff and AI systems: "this is a high-pressure turnover day — don't promise flexibility you don't have."

## Tourism Translation
**A "red day" on the cleaning schedule.**

Housekeeping teams color-code their daily schedule: green = check-in only, yellow = check-out only, red = turnover. On red days, every minute between 10 AM checkout and 3 PM check-in is spoken for. There's no "we can squeeze you in early" — the window is already full. A tight turnover warning is that red flag, surfaced to anyone making promises to guests.

## When it fires
The system raises the warning when:
- A PRIOR reservation's check_out equals the current guest's check_in (same-day turnover before)
- A NEXT reservation's check_in equals the current guest's check_out (same-day turnover after)
- Optionally: if the gap is just 1 day (still tight, but not impossible)

## Why it matters
Without this warning, systems treat every day the same. A guest asks "can I arrive at noon?" and the AI says yes — not realizing noon is smack in the middle of the 5-hour cleaning window. Or a staff member promises late checkout at 12 PM on a day when the next guest arrives at 3 PM.

The warning converts invisible scheduling conflicts into visible flags. It's the difference between "I didn't know" and "I knew — and I hedged."

## Where it shows up in FLOHOM
- **FLO Brief**: a "TURNOVER CONTEXT" block flagged "NOT guaranteed"
- **FLO's replies**: automatic hedging language ("we can try, but it's not guaranteed on back-to-back days")
- **Future**: potentially surfaced to admin inbox UI as a badge on the conversation

## Related concepts
- [Turnover](turnover.md) — the operational event itself
- [Adjacent Reservation Awareness](../ai/adjacent-reservation-awareness.md) — the AI-side view
- [Hedge-Don't-Promise Pattern](../ai/hedge-dont-promise-pattern.md) — the language rule triggered by the flag
- [Check-in/Check-out Boundaries](checkin-checkout-boundaries.md) — the underlying date windows
