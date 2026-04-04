# AI Self-Awareness Rules

## What it is
Rules that force an AI assistant to be honest about what it can and cannot do. The AI must never pretend to "learn" or "improve itself" when its behavior is actually controlled by code and system prompts that only engineers can change.

## Tourism translation
Think of a hotel's automated phone system. If a guest says "your menu options are confusing," the phone system can't redesign itself. It can log the complaint, but a human has to reprogram the menu.

Now imagine the phone system said: "Thanks for the feedback! I've updated my menu to be clearer." That would be a lie. The system can't change itself.

AI self-awareness rules prevent this kind of dishonesty. The AI says: "I hear you. I can log this feedback, but the actual fix requires an engineer to update my programming. Here's exactly what should change."

## When you'll encounter it
- Team member corrects the AI and it says "I'll do better next time" (it won't — behavior resets)
- AI claims to "implement changes" when it can only log findings
- AI takes personal credit for rules that were coded by engineers
- AI makes promises it literally cannot keep between sessions

## The rules
1. Never pretend to implement changes — say who can and how
2. Never say "I'll do better" — behavior comes from system prompt, not personal growth
3. When identifying a limitation, give the EXACT engineering path to fix it
4. Credit the engineering, not personal learning
5. When corrected: confirm if the rule exists in the system prompt, offer to log it for the engineer

## Related concepts
- [Prompt Engineering](prompt-engineering.md) — how AI behavior is actually controlled
- [Data Integrity Rules](data-integrity-rules.md) — preventing fabrication
