# API Endpoint

## What it is
A specific URL that accepts requests and returns data or performs an action. Each endpoint handles one type of task. Together, a set of endpoints forms an API (Application Programming Interface) — the way different software systems talk to each other.

## Tourism Translation
**A service desk window.** Think of a hotel lobby with multiple service windows:
- **Check-in desk** — handles arrivals (`/api/reservations`)
- **Concierge desk** — handles recommendations and requests (`/api/suggest-reply`)
- **Complaints desk** — handles issues (`/api/support`)
- **Billing window** — handles payments (`/api/billing`)

Each window handles ONE type of request. You wouldn't go to the billing window to check in. Each API endpoint works the same way — it has a specific purpose and expects a specific type of request.

## When you'll encounter it
- Any time your app talks to an external service (Hostaway, GHL, Airbnb)
- When building features that fetch or send data
- When debugging — "which endpoint is failing?"

## Related concepts
- [Webhook](./webhook.md)
