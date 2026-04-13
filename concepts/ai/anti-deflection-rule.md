# Anti-Deflection Rule

## What it is
A prompt rule that prevents AI from saying "email us" or "call support" as its first response. Instead, the AI must try to answer using its tools, and only escalate to a human who will follow up — never punt the guest to another channel.

## Tourism translation
Like training front desk staff to never say "call back tomorrow" — either solve it now, or get a manager who will personally call the guest back within the hour. The guest should never feel redirected or abandoned.

## When you'll encounter it
- AI concierges that have knowledge gaps (parking info, addresses, furniture details)
- Any customer-facing AI where "I don't know, email us" is a failure state
- Quality audits that find the AI deflecting instead of helping

## Why it matters
If a guest asks "Where do I park?" and the AI says "Email reservations@company.com," the guest's experience is worse than if no AI existed. The whole point of an AI concierge is to eliminate the need to email.

## The fix
```
BEFORE: "I don't have that info. Email reservations@flohom.com"
AFTER:  "Let me check on that for you. I'll have the team follow up with the details."
```
The AI escalates to a human behind the scenes. The guest feels taken care of, not redirected.

## Related concepts
- [LLM-as-Judge](./llm-as-judge.md) — catches deflection patterns in quality scoring
