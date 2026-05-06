# Admin Preview Token / Mode

## What it is
A special URL mode that lets an admin see exactly what a guest would see — using real property data — without needing an actual guest booking or authentication. Typically implemented as a special token or URL pattern that the API recognizes as "admin preview mode" and responds with real content but a mock identity.

## The pattern
```
/floex/preview-admin-{propertyId}
```
When the boarding pass API receives a token starting with `preview-admin-`, it:
1. Extracts the real property ID
2. Loads real property data (steps, upsells, wifi, access codes, etc.)
3. Substitutes a mock guest object (fake name, no real reservation)
4. Returns the full boarding pass — exactly as a guest would see it

This lets admin staff review, configure, and QA the boarding pass without creating fake reservations.

## Tourism translation
A hotel general manager doing a "mystery guest" walkthrough of their own property — they walk the check-in process, use the room key, test the amenities, and evaluate the experience exactly as a guest would. The difference: they know it's a test, but everything they interact with is the real product.

It's also like a restaurant manager plating the dish themselves before service starts — real food, real presentation, no actual diner.

## Why it exists
- **Config confidence**: admins editing check-in steps, upsell products, or WiFi info need to see the result before a real guest does
- **No test data pollution**: no need to create fake reservations in the PMS (Hostaway) just to preview a boarding pass
- **Safe**: mock guest has no real payment info, no real contact info — nothing that could accidentally trigger real notifications

## Implementation checklist
1. Define the preview token format (e.g., `preview-admin-{id}`) — easy to detect, hard to accidentally collide with real tokens
2. In the API: branch on token prefix. If preview, skip real guest lookup; inject mock guest object
3. Require admin session for the preview endpoint or use a secret prefix unknown to guests
4. Show a visible "Admin Preview" banner in the UI so staff know they're not looking at a real pass

## Gotcha
The boarding pass iframe in an admin page needs `X-Frame-Options: SAMEORIGIN` and `frame-ancestors 'self'` on the guest-facing route — otherwise the browser blocks the iframe due to CSP. See `content-security-policy.md`.

## Learned from
FLOHOM FLOx Config redesign (May 2026). The admin needed a live phone-framed preview of the boarding pass while editing steps, upsells, and guidebook content. The `preview-admin-{propertyId}` token mode already existed in the API — it just needed the CSP unblocked to render inside the admin iframe.
