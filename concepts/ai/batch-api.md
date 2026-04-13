# Batch API

## What it is
Sending multiple AI requests in one bundle at a 50% discount, processed within hours instead of instantly. Good for background tasks that don't need real-time responses.

## Tourism translation
Like submitting all your linen orders for the week in one batch to the laundry service at a bulk rate, instead of calling for each room individually at rush pricing. You wait a bit longer, but pay half price.

## When you'll encounter it
- Scheduled AI reports (weekly debriefs, performance summaries)
- Processing multiple items that don't need instant results
- Any AI workload where you can tolerate minutes or hours of delay

## How it works
```
Real-time:  Send 1 request → Get response in 2 seconds → Full price
Batch:      Send 50 requests → Get all responses in ~1 hour → 50% off
```

## Related concepts
- [Prompt Caching](./prompt-caching.md) — another cost optimization (can combine with batch for up to 95% savings)
