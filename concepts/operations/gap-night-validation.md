# Gap Night Validation (Calendar-Aware)

## What it is
The process of verifying that empty nights between bookings are actually available for sale. A "gap" in the reservation database doesn't always mean the property is bookable — it could be blocked for cleaning, owner use, maintenance, or an internal hold. Validation requires checking the channel's live calendar, not just the reservation table.

## Tourism Translation
**"The room looks empty on the chart" vs. "the room is actually ready to sell."**

Your reservation grid shows a 3-night gap between Guest A's checkout (Apr 6) and Guest B's check-in (Apr 9). Your revenue manager flags it as lost income. But housekeeping blocked Apr 6 for deep cleaning after a pet stay. The real sellable gap is only 2 nights (Apr 7-8, checkout Apr 9).

If you advertise 3 nights and a guest books Apr 6, you have a conflict. Validation means checking the actual calendar — not just the whitespace between bookings.

## Why it matters
- **False gaps waste ad spend** — promoting dates that aren't actually available
- **Overstated opportunity** — telling the owner "you're losing $5,000 in gap revenue" when $2,000 of that is genuinely blocked
- **Split logic matters** — when a 3-night gap has 1 blocked day in the middle, you need to show two smaller available windows, not remove the whole gap

## Key principles
1. **SQL finds candidates, calendar confirms truth** — database gaps are hypotheses, live calendar is proof
2. **Split around blocks, don't discard** — if 1 of 3 nights is blocked, show the 2 available nights
3. **Respect check-in/check-out boundaries** — a "reserved" date in the calendar means a guest arrives that day; the previous night is still sellable (it's checkout morning)
4. **Include block reason when available** — "owner hold" vs. "maintenance" vs. "minimum stay restriction" changes the action
5. **Urgency tiers drive action** — 0-14 days = last-minute discount push, 15-30 days = standard promo, 31-60 days = planning horizon

## Related concepts
- [Stay-Date vs. Booking-Date Revenue](./stay-date-vs-booking-date.md)
- [Source-of-Truth Hierarchy](./source-of-truth-hierarchy.md)
