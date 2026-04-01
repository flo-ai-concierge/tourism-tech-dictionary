# Split Payment (50/50 Payment Model)

## What it is
A payment structure where the guest pays in two installments: half at the time of booking, and the other half closer to their arrival date. Different booking channels handle payments differently — some collect everything upfront, others split it.

## Tourism Translation
**A resort deposit system — 50% to hold the room, 50% on arrival day.**

Think of it like booking a wedding venue. You pay a deposit to lock in the date, then pay the balance closer to the event. This is how VRBO works — the guest pays 50% when they book, and the remaining 50% is charged the day before arrival. Airbnb, on the other hand, is like buying a concert ticket — you pay the full amount immediately.

## Channel payment models (FLOHOM)
| Channel | Payment Model |
|---------|--------------|
| **Airbnb** | Paid in full at booking (always shows "Paid") |
| **VRBO** | 50% at booking, 50% day before arrival |
| **Website (Booking Engine)** | Depends on settings — may require full or partial payment |
| **Direct** | Manual collection via Stripe/Venmo — host tracks it |

## Why it matters
A "Partially paid" VRBO reservation is completely normal — it's their standard 50/50 split. Don't flag it as a problem. But a "Partially paid" Direct booking means someone hasn't finished paying and needs follow-up.

## Related concepts
- [Webhook](./webhook.md) — how payment status updates flow between systems
- Payment gateway — the service that processes the actual money transfer
