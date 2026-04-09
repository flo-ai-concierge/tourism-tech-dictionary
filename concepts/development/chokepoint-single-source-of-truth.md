# Chokepoint / Single Source of Truth

## What it is
A deliberate architectural pattern where every path through your system funnels through one central function or module. If you change the behavior there, every path gets the new behavior automatically. No duplication, no "oops I forgot to update one place."

## Tourism Translation
**"Every guest picks up their key at the front desk — nowhere else."**

Imagine if you had five different ways to get a room key: front desk, lobby kiosk, a box near the pool, a drawer in the spa, and housekeeping's office. Now imagine you decide to switch to digital keys. You have to update all five places. You will miss one. A guest will show up at the spa, get a physical key, and chaos ensues.

Instead: one front desk. Every guest goes there. When you switch to digital keys, you update exactly one system.

## Why it matters

### Our review ingestion chokepoint
Every review in FLOHOM — from Hostaway sync, from GHL webhook, from the PDF parser, from manual admin entry — flows through exactly one function: `ingestMention()` in `src/lib/flo-reputation.js`.

When we added the auto-Slack-post hook, we added it to `ingestMention()`. Instantly, every path started posting to Slack. We didn't have to touch the Hostaway sync, the webhook handler, or the parser — they all call the same chokepoint.

### When you update the logic, everyone benefits
When we added the property-matching fallback (parse review body for FLOHOM references), we put it inside `ingestMention()`. Now the Hostaway sync, GHL webhook, and manual entries all get the same matching logic. No duplication.

### When you break the chokepoint, everyone breaks
This is the downside. A bug in `ingestMention()` breaks every ingestion path at once. So the chokepoint needs to be well-tested, well-reviewed, and carefully changed.

### Real FLOHOM example
```
Hostaway sync ──┐
                ├──> ingestMention() ──> reputation_mentions
GHL webhook ────┤                              │
                │                              ▼
PDF parser ─────┘                      postReviewToSlack() (fire-and-forget)
```
One chokepoint, three sources, one consistent outcome.

## In simpler terms
It's the kitchen at a restaurant. Every dish, whether it's for dine-in, takeout, or delivery, comes out of one kitchen. Change the kitchen — new chef, new equipment, new menu — and every order, from every channel, gets the change automatically.
