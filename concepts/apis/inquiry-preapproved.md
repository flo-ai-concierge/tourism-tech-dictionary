# inquiryPreapproved (Hostaway/Airbnb Status)

## What it is
A reservation status in Hostaway meaning the host has said "yes, we'd love to host you" but the guest hasn't actually booked or paid yet. It's a green light from the host's side — the ball is now in the guest's court to complete the booking within 24 hours.

## Tourism Translation
**Telling a walk-in guest "yes, we have a room available for you" — but they haven't signed the registration card or paid yet.**

The guest asked "do you have availability?" and you said "absolutely!" But until they hand over their credit card and sign in, the room isn't actually booked. If they walk away and come back tomorrow, the room might be taken by someone else. Pre-approval is the host's handshake — the booking happens when the guest follows through.

## Important distinction
- **Inquiry** = Guest asks "do you have availability?" (no commitment from either side)
- **Pre-approved** = Host says "yes, come on in!" (host committed, guest hasn't)
- **Confirmed/New** = Guest books and pays (both sides committed)

## Channel-specific behavior
- **Airbnb**: Pre-approval gives the guest 24 hours to accept. Must be done through Airbnb or Hostaway — external systems cannot trigger this.
- **VRBO**: Uses a different approval flow.
- **Website/Direct**: Approval immediately creates a confirmed reservation.

## Related concepts
- [Webhook](./webhook.md)
- Reservation lifecycle — the journey from inquiry to checkout
