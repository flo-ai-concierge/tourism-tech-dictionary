# Webhook Signature Verification

## What it is
Checking that an incoming request actually came from the service it claims to be from, using a cryptographic signature (like a tamper-proof seal). The sender hashes the request body with a shared secret, and the receiver re-computes the hash to verify it matches. Without this, anyone could fake a webhook and inject malicious data.

## Tourism Translation
**"Verifying a guest's government ID at check-in — not just accepting anyone who says 'I have a reservation.'"**

The signature is the hologram on the ID that proves it's real. A front desk that skips ID verification is letting anyone walk into rooms. Similarly, a webhook endpoint without signature verification lets anyone send fake events to your system.

## Why it matters
Webhooks are publicly accessible URLs. Without signature verification, an attacker could:
- Send fake "reservation cancelled" events to delete real bookings
- Inject fake SMS messages into the inbox
- Trigger automated responses to guests they shouldn't be able to reach

Each integration signs differently: Hostaway uses HMAC-SHA256, Meta uses SHA-256 with an app secret, QUO (OpenPhone) uses Ed25519 signatures. The receiver must know which method to use and reject any unsigned request.

## In simpler terms
It's the difference between a locked front door and an open one. The webhook URL is the door. The signature is the key. Without it, anyone can walk in.
