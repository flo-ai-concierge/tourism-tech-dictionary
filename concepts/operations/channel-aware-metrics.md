# Channel-Aware Metrics

## What it is
The practice of computing and presenting metrics differently based on which booking channel the data comes from, because each channel has different data quality, fee structures, and business meaning. Never aggregate across channels without channel-specific logic.

## Tourism Translation
**"Airbnb reviews and Booking.com reviews are not the same thing."**

Your Airbnb listing has a 4.9 rating from 200 reviews. Your Booking.com listing has a 8.2 from 50 reviews. You can't average them (4.9 + 8.2) / 2 because they use different scales, different guest populations, and different review criteria. Combining them produces a meaningless number.

The same applies to every metric: response time, commission, conversion rate, inquiry tracking. Each channel works differently, and treating them as interchangeable produces wrong conclusions.

## Why it matters

### Commission is channel-specific
- Airbnb: uses `airbnbListingHostFee` (3% split-fee or 14% simplified)
- VRBO: uses `channelCommissionAmount` (~12%)
- Direct/booking engine: 0% commission
- NULL commission ≠ zero commission — it means "we don't know"

### Response tracking differs by channel
- Airbnb: reliable in-thread message tracking
- VRBO: reliable but slower median response
- Booking engine: unreliable — previous staff replied via SMS/QUO outside the tracked thread
- Direct: often no messages at all (phone/email bookings entered manually)

### Conversion rates aren't comparable
- Airbnb instant book: guest clicks "Book" → confirmed. No inquiry step.
- Booking engine: guest submits inquiry → may or may not get replied to → may convert
- Direct: owner creates reservation manually → always "converts" at 100%

## Key principles
1. **Never average metrics across channels** without channel-specific logic
2. **Label which channels are included** — "Airbnb + VRBO only (booking engine excluded)"
3. **Exclude unreliable channels from actionable KPIs** — use them for context, not decisions
4. **Commission = channel acquisition cost**, not "leakage" — it's the price of distribution
5. **NULL is not zero** — missing data requires explicit handling, not silent fallback to 0
6. **Sample size gates** — suppress rates where n < 5, label n < 20 as "small sample"

## Related concepts
- [Source-of-Truth Hierarchy](./source-of-truth-hierarchy.md)
- [Locked Values](../ai/locked-values.md)
