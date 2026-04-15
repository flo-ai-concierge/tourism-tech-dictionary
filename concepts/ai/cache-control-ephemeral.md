# Cache Control: Ephemeral

## What it is
A tag added to AI system prompts that tells Claude "remember this instruction block for 5 minutes so you don't have to re-process it." The word "ephemeral" means temporary — the cache expires after a short window, but within that window every subsequent call is 90% cheaper.

## Tourism translation
Like a concierge keeping the property guidebook open on their desk instead of walking to the filing cabinet every time a guest asks a question. The book stays open for a few minutes, and during that time every answer is faster and cheaper.

## When you'll encounter it
- Any Claude API call that uses `cache_control: { type: "ephemeral" }` on the system prompt
- Applied to all 13 Claude API endpoints in the FLOHOM platform (as of Apr 15, 2026)
- The Anthropic SDK handles the caching automatically — you just add the tag

## How it works
```javascript
// Without caching — full price every call
system: "You are FLO, the concierge for FLOHOM..."

// With caching — 90% cheaper on repeat calls within 5 min
system: [{ type: "text", text: "You are FLO...", cache_control: { type: "ephemeral" } }]
```

## Related concepts
- [Prompt Caching](./prompt-caching.md) — the broader concept
- [System Prompt](./system-prompt.md) — what gets cached
