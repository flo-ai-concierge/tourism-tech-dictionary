# Rate Limiting (Webhook)

## What it is
Capping how many requests a webhook endpoint accepts per time window (e.g., 30 requests per minute per IP). Excess requests get rejected with a 429 "Too Many Requests" response. Prevents abuse, accidental floods, or denial-of-service attacks from overwhelming your server.

## Tourism Translation
**"A hotel concierge desk that serves max 30 guests per hour."**

If a tour bus drops off 200 people and they all rush the concierge desk at once, the first 30 get helped and the rest are politely asked to wait. Without this limit, the concierge collapses under the load and nobody gets helped — including VIP guests with real emergencies.

## Why it matters
Webhooks are public URLs that external services hit automatically. Without rate limiting:
- A misconfigured integration could send thousands of duplicate events per minute
- An attacker could flood the endpoint to crash the server
- Legitimate webhooks from other services would fail because the server is overwhelmed

FLOHOM uses a sliding-window rate limiter (30 requests/minute/IP) on all webhook endpoints — Hostaway, GHL, Meta, QUO, Google Alerts, and GHL Reviews.

## In simpler terms
It's a bouncer at the door who counts people. Once the room is at capacity, new arrivals wait outside until someone leaves.
