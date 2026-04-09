# API Probing

## What it is
Sending test requests to an API's unknown or undocumented endpoints to see how they respond, then inferring from the response code whether the feature exists, requires different auth, or isn't exposed at all. Used when vendor docs are incomplete or vague.

## Tourism Translation
**"Calling a restaurant at midnight to find out if they're open."**

The website doesn't list their hours. You pick up the phone and dial. Three outcomes:
- They answer → open
- It rings out → closed or understaffed
- "This number is disconnected" → they don't exist

API probing is the same thing. You try `POST /v1/reviews` against Hostaway. Three outcomes:
- `200 OK` → endpoint exists and you can write reviews
- `401 Unauthorized` → endpoint exists but you need more permissions
- `404 Not Found` → endpoint doesn't exist, this feature isn't publicly available

## Why it matters

### Vendor documentation lies
Most API docs are incomplete or outdated. The only way to know for sure whether a feature works is to try it in a safe, non-destructive way.

### It saves days of back-and-forth
Instead of emailing "Hi Hostaway support, does your API support writing host-to-guest reviews?" and waiting a week, you spend 30 seconds probing and know the answer immediately.

### It has to be safe
Never probe with real data. Always use empty payloads, test reservation IDs, or known-disposable records. A probe that accidentally deletes a production reservation is worse than not probing at all.

### Real FLOHOM example
When we planned the host-to-guest review submission flow, I probed Hostaway's API with `POST /v1/reviews`, `PUT /v1/reviews/{id}`, `POST /v1/reviews/{id}/submit`, and several nested paths. All returned 404. That told us immediately that Hostaway's public API doesn't support review writes — we pivoted to a copy-paste workflow instead of wasting 2 days building against a dead endpoint.

## In simpler terms
Try the door handle before knocking. If the door isn't even there, you won't waste time shouting through a wall.
