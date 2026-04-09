# Rate Limit / Retry-After

## What it is
A limit on how fast you can make requests to an external service. When you hit the limit, the service rejects your next request with a `429` status code and a `Retry-After` header telling you how many seconds to wait before trying again.

## Tourism Translation
**"Airbnb won't let you send 100 messages in 10 seconds — they throttle you."**

You're blasting out a batch update to 200 guests. After the first 50 messages, Airbnb's API starts returning errors: "slow down, wait 60 seconds." Your script either respects that and pauses, or keeps hammering the door and gets locked out entirely.

## Why it matters

### It protects the service from abuse
Rate limits exist so one sloppy script can't take down a whole platform. Slack's `chat.delete` is limited to about 50 calls per minute per workspace. Hostaway, Stripe, and every major booking platform work the same way.

### You have to code around it
A well-built sync respects the `Retry-After` header: when it gets a 429, it reads the suggested wait time, sleeps that long, then resumes. A bad script retries immediately and gets banned faster.

### Real FLOHOM example
During the #reviews Slack backfill of 1,024 cards, we hit Slack's Tier 3 limit (chat.delete rate-limited to bursts of ~4). Every burst we hit, Slack returned `retry-after: 10`. The cleanup script had to honor that or the full cleanup would have taken forever.

## In simpler terms
The API is a popular bar. It'll serve you, but if you order 20 drinks in 30 seconds the bartender will cut you off until you calm down. Space your orders out and you'll be served all night.
