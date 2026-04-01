# Classification Tiers (T0/T1/T2/T3)

## What it is
A routing system that analyzes incoming messages and decides how complex they are, then sends them to the right AI "brain" for processing. Simple questions go to a fast, cheap model. Complex questions go to a powerful, thorough model. This saves money and speeds up responses.

## Tourism Translation
**A hotel's front desk triage system.**

When a guest walks up to the front desk:
- **T0 (Greeting)**: "Hi!" → Front desk smiles and says hi back. No thinking required.
- **T1 (Simple FAQ)**: "What's the WiFi password?" → Concierge answers instantly from the property handbook.
- **T2 (Needs research)**: "Can I hire a private chef?" → Concierge checks the vendor list, looks up pricing, and gives a detailed answer.
- **T3 (Complex/escalation)**: "I'm unhappy with my stay and want to discuss compensation" → Manager gets involved with full context.

The key insight: you don't need the hotel manager for every WiFi password question. Route the right question to the right person.

## Why it matters
A chef/massage question was accidentally classified as T1 (simple FAQ), so the system answered with "let me check on that" instead of providing the actual vendor info. The fix: explicitly route service-related keywords to T2 so the full knowledge bank is used.

## Related concepts
- [Prompt Engineering](./prompt-engineering.md)
- Token optimization — using cheaper models for simple tasks
