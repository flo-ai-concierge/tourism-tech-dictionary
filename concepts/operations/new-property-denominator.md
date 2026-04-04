# New Property Denominator Problem

## What it is
When a performance metric (like occupancy or RevPAR) uses a fixed time window (e.g., 90 days) as the denominator, but the property hasn't been open for that long. The metric is artificially deflated because you're dividing by days the property didn't exist.

## Tourism translation
You open a new restaurant on March 6. By April 4 (29 days later), you've served 300 covers. Someone calculates "90-day performance" and says you averaged 3.3 covers per day. But you were only open 29 days — your real average is 10.3 per day. Three times better than the report says.

That's the new property denominator problem. The measurement window is longer than the property's operating history, making it look like an underperformer.

## The fix
Use `MIN(90, actual_days_active)` as the denominator. If a property has been active 29 days, divide by 29, not 90.

## Real example
FLOHOM Port Noir (FLO 13) opened with its first guest on March 6, 2026. The revenue report measured all properties over a 90-day window. Port Noir showed:
- 13.3% occupancy / $88 RevPAR → ranked #14 out of 14 (last place)

After fixing the denominator to 29 days:
- 44.8% occupancy / $274 RevPAR → ranked #6 (top half of portfolio)

The property went from "worst performer" to "strong mid-tier" with one denominator fix.

## When you'll encounter it
- Any new property added to a portfolio report
- Seasonal properties with limited operating windows
- Properties coming back online after renovation or closure

## Related concepts
- [Stay Date vs Booking Date](stay-date-vs-booking-date.md) — which dates to measure
- [Channel-Aware Metrics](channel-aware-metrics.md) — different properties need different treatment
