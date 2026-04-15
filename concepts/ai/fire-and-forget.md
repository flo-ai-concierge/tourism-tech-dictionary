# Fire-and-Forget

## What it is
Starting a background task without waiting for it to finish. The main process continues immediately while the task runs independently. If it fails, it fails silently — the user's experience isn't blocked.

## Tourism translation
Like dropping off laundry at the marina service. You hand over the bag and walk away — you don't stand there watching them wash it. If they lose a sock, you'll deal with it later, but your day isn't blocked.

## When you'll encounter it
- FLO Quality scoring: after every reply, a Haiku judge call fires in the background without slowing down the guest's response
- Slack alert posting: quality alerts are sent to Slack without waiting for Slack's API to confirm delivery
- Sentiment analysis: when a new review is ingested, sentiment scoring runs without blocking the ingestion

## How it works
```javascript
// Blocking (slow) — user waits for both to finish
const reply = await generateReply(message);
const score = await scoreQuality(reply);  // user waits for this too
return reply;

// Fire-and-forget (fast) — user gets reply immediately
const reply = await generateReply(message);
scoreQuality(reply).catch(() => {});  // runs in background, no waiting
return reply;
```

## Related concepts
- [LLM-as-Judge](./llm-as-judge.md) — the quality scoring that runs fire-and-forget
