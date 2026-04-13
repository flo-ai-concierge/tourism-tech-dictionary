# Re-ask Detection

## What it is
Tracking when a guest asks the same question twice in a conversation — a signal that the AI's first answer didn't resolve the issue. The system flags this so the AI gives a more thorough response on the second attempt.

## Tourism translation
Like when a guest calls the front desk twice about the same issue — the second call means the first person didn't resolve it. A good hotel flags repeat calls so the next staff member knows to go deeper, not give the same script.

## When you'll encounter it
- AI quality monitoring (re-asks indicate failed first responses)
- Working memory systems that track conversation state
- Customer satisfaction metrics (re-ask rate = inverse of first-contact resolution)

## How it works
```
Guest: "Where do I park?"
AI: "Parking is at the marina garage." (topic: parking → resolved)

Guest: "But where exactly is the garage?"
System: RE-ASK DETECTED (parking was already "resolved" but guest asked again)
AI: [gives more detailed response with address and directions]
```

## Related concepts
- [LLM-as-Judge](./llm-as-judge.md) — re-asks factor into quality scores
- [Anti-Deflection Rule](./anti-deflection-rule.md) — deflections cause re-asks
