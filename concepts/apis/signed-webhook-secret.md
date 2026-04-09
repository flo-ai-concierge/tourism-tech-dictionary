# Signed Webhook Secret

## What it is
A secret password embedded in a webhook URL (or validated via an HMAC signature header) that proves the incoming request actually came from the service that's supposed to be calling us. Without it, anyone who discovers the URL could POST fake data into our system.

## Tourism Translation
**"The parking gate code — only real guests have it."**

The gate to your marina parking lot is on a public road. Anyone can walk up. But the gate only opens for vehicles with the 4-digit code printed on the reservation confirmation email. If you don't have the code, you don't get in, no matter how confidently you press the buttons.

Our Hostaway webhook URL looks like `https://flohom-guest.onrender.com/api/webhooks/hostaway?secret=cf4d4217...`. That `secret=` part is the parking code. Hostaway includes it on every call. If the secret doesn't match, we reject the request with a 401.

## Why it matters

### Webhooks are public endpoints
By definition, a webhook URL has to be reachable from the internet so the external service can call it. That means a scraper, an attacker, or a curious former employee could find it. The secret is the one thing standing between "real Hostaway event" and "random garbage POST."

### Constant-time comparison
Comparing the secret with `===` leaks timing information to attackers. Our code uses `crypto.timingSafeEqual()` instead, which takes the same amount of time regardless of how many characters match. This prevents timing attacks.

### Rotation
If a secret ever leaks, you generate a new one, update it in both Hostaway's webhook config and Render's env vars, and the old URL stops working immediately.

## In simpler terms
It's the difference between leaving your front door unlocked with a "come on in" sign, and locking it with a key only trusted partners have a copy of.
