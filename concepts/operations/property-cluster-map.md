# Property Cluster Map

## What it is
A hardcoded lookup table that knows which properties are geographically near each other. When an alert fires at one property (like a noise complaint), the system automatically checks on neighboring properties — are they occupied? Could their guests be affected?

## Tourism Translation
**"A resort campus map showing which villas share a courtyard."**

If Villa 4 reports a noise complaint at 2 AM, the night manager doesn't just deal with Villa 4 — they automatically check on Villas 6 and 8 next door. The cluster map is the manager's mental model of "these three are close together, what happens at one affects the others."

## Why it matters
FLOHOM has 15 properties across multiple markets. Some are standalone, but several are in the same building or marina:
- FLOHOM 1, 5, 13 — Inner Harbor, Baltimore
- FLOHOM 4, 6, 8 — National Harbor
- FLOHOM 2, 7 — Canton
- FLOHOM 10, 11 — Virginia Beach

When FLO generates guidance for a noise alert at FLOHOM 4, it automatically mentions: "FLOHOM 6 and 8 are in the same area — check if their guests are being affected. Check VicoPhone CCTV for visual confirmation."

## In simpler terms
It's knowing your neighbors. When there's a party at one property, you check on the ones next door.
