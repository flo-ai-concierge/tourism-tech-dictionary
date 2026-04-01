# Date Conflict Block (API Limitation)

## What it is
When a booking system's API refuses to change an old inquiry's status because another guest has already booked those same dates. Even though you're trying to cancel or decline the old inquiry, the API sees the date overlap and blocks the change. This is a known limitation in some PMS APIs (like Hostaway).

## Tourism Translation
**Trying to cancel a waitlist entry for a table that's already been given to someone else — but the reservation book won't let you cross it out.**

Imagine your restaurant had two people interested in the 7 PM table. Guest A got it and is confirmed. Now you want to cross out Guest B from the waitlist, but the book says "Error: that table is occupied." You know it's occupied — that's WHY you're crossing them out! But the system is too rigid to understand the context.

## How to handle it
1. **Update your local records** — mark it as declined in your own system
2. **Send the decline message** — let the guest know the dates aren't available
3. **Manual cleanup** — if the PMS dashboard allows it, decline there directly (the UI often works even when the API doesn't)
4. **Don't delete** — never delete reservations from the PMS to work around this

## Related concepts
- [Webhook](./webhook.md)
- [API Endpoint](./api-endpoint.md)
- Error handling — gracefully managing when things go wrong
