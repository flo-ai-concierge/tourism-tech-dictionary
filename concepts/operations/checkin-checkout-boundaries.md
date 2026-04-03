# Check-in / Check-out Date Boundaries

## What it is
The rule that a reservation's check-in date is the day the guest arrives (they sleep that night), and the check-out date is the day they leave (they do NOT sleep that night). This means the check-out date of one guest is available as the check-in date for the next guest — they are the same calendar day.

## Tourism Translation
**"Tuesday checkout, Tuesday check-in — same day, different guests."**

Guest A checks out Tuesday morning. Guest B checks in Tuesday afternoon. Tuesday is both a checkout and a check-in. In the calendar system, Tuesday shows as "reserved" because Guest B is arriving. But for gap calculations, Tuesday is the last available check-in date for any gap ending before Guest B.

If you see a gap of Apr 6–Apr 9 and the calendar shows Apr 9 as "reserved," that doesn't mean Apr 9 is lost. It means a new guest arrives Apr 9. A guest filling the gap checks in Apr 6 (or later), sleeps through Apr 8, and checks out the morning of Apr 9 — right before the next guest arrives.

## Why it matters
Getting this wrong by one day across a portfolio creates systematic errors:
- **Gap nights undercounted** — every gap loses its last sellable night
- **Revenue opportunity understated** — 1 missing night × 14 properties × $500/night = $7,000 invisible
- **Calendar validation bugs** — code that checks if the checkout date is "available" will always reject it because the next guest is arriving that day

## Key principles
1. **Nights = checkout date minus check-in date** — a guest checking in Mon, out Wed = 2 nights (Mon, Tue)
2. **The checkout date is NOT a blocked night** — it's a transition day
3. **In calendar APIs, "reserved" on a date means a guest arrives that day** — the previous night is still the last available sleep night
4. **Gap end = next guest's check-in = this gap's checkout** — don't check this date for availability
5. **Always test with real calendar data** — never assume date logic is correct without verifying against the live system

## Related concepts
- [Gap Night Validation](./gap-night-validation.md)
- [Stay-Date vs. Booking-Date Revenue](./stay-date-vs-booking-date.md)
