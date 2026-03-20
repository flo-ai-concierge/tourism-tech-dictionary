# Webhook

## What it is
An automatic notification sent from one system to another when something happens. Instead of constantly checking "did anything change?" (polling), the source system pushes updates to you the moment something occurs.

## Tourism Translation
**An automatic channel manager alert.** When a guest books on Airbnb, you don't want to log into Airbnb every 5 minutes to check for new bookings. Instead, the channel manager automatically notifies your PMS the instant a booking happens. You didn't ask for it at that moment — it pushed to you.

Polling would be like calling every OTA every 5 minutes asking "any new bookings?" — exhausting and wasteful. A webhook is the OTA calling YOU when there's a booking.

## When you'll encounter it
- Airbnb/Booking.com → your PMS (reservation notifications)
- Payment processor → your system (payment confirmed)
- GHL → your platform (new message received)
- Meta → your platform (Facebook/Instagram DM received)

## How FLOHOM uses webhooks
Three webhook endpoints, one per integration:
- `/api/webhooks/hostaway` — reservation and message updates
- `/api/webhooks/ghl` — CRM messages (SMS, email, WhatsApp, social)
- `/api/webhooks/meta` — Facebook and Instagram interactions

## Related concepts
- [API Endpoint](./api-endpoint.md)
