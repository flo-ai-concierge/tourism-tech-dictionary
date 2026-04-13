# Prompt Caching

## What it is
Storing parts of AI instructions so they don't need to be re-processed every time. When the same system prompt is sent repeatedly, the AI provider remembers it and charges 90% less for the cached portion.

## Tourism translation
Like having pre-printed check-in packets instead of handwriting each guest's welcome letter every time. The packet template is "cached" — you only customize the guest name and room number. Saves time and cost per guest.

## When you'll encounter it
- Running an AI concierge that handles hundreds of conversations with the same system instructions
- Any AI system where the prompt is mostly static but the user message changes each time
- Cost optimization for high-volume AI applications

## How it works
```
First request:  System prompt (1000 tokens) + User message → Full price
Second request: System prompt (cached!) + User message → 90% cheaper on cached portion
```
The AI provider keeps the system prompt in memory for ~5 minutes. Any request within that window reuses it.

## Related concepts
- [System Prompt](./system-prompt.md) — the instructions being cached
- [Max Tokens](./max-tokens-truncation.md) — how much the AI can respond with
