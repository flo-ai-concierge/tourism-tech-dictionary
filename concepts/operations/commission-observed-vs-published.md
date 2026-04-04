# Commission: Observed vs Published Rates

## What it is
The difference between what a booking platform says their fee is (published rate) and what you actually pay per booking (observed rate from transaction data).

## Tourism translation
VRBO says "5% host fee." But when you check your actual payouts across 76 bookings, you're paying 11.8% on average. Why?

Because "5%" is the published host service fee — what the HOST pays. But the system may also record the GUEST service fee (what the traveler pays) bundled into one "channel commission" number. So the data shows 11.8% (host 5% + guest ~7%) even though the host only "pays" 5%.

Similarly, Airbnb publishes "15.5% simplified pricing" — but if some properties use split-fee (3% host / 14% guest) and others use simplified (15.5% host), blending them into one average gives a number that represents neither model.

## The lesson
- Always know WHICH fee you're reporting: host-paid, guest-paid, or total platform take
- Don't blend different pricing models into one average
- Published rates are policy. Observed rates are reality. Report the one your audience needs.
- A CEO wants to know "what do I pay?" — that's the host fee only
- A revenue analyst might want "total platform cost" — that's host + guest combined

## Real example
FLOHOM's Revenue Report showed Airbnb at 6.8% and VRBO at 11.9%. Brian (CEO) said "VRBO is 5% and Airbnb is 15.5%." Investigation revealed:
- Airbnb 6.8% was wrong — NULL-fee bookings diluted the denominator. Real rate: 15.5% of listing subtotal for simplified pricing.
- VRBO 11.9% included the guest service fee, not just the host fee. Brian's 5% was what HE pays.
- The denominator matters: dividing by `totalPrice` (includes guest fees) gives a lower % than dividing by listing subtotal (base + cleaning).

## Related concepts
- [Source of Truth Hierarchy](source-of-truth-hierarchy.md) — which data to trust
- [Channel-Aware Metrics](channel-aware-metrics.md) — different channels need different logic
