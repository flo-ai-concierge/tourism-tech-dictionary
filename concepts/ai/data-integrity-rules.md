# Data Integrity Rules (AI Concierge)

## What it is
A set of non-negotiable rules that prevent an AI assistant from fabricating information. The AI must retrieve real data from a tool/database before stating any fact — never guess, infer, or pattern-match from context.

## Tourism translation
Imagine a front desk agent who "remembers" a guest's room number without checking the system. They sound confident: "You're in room 412!" But the guest was actually moved to 518. The agent guessed based on a pattern (guest last name starts with H, H guests usually go to 4th floor) instead of checking the computer.

Data integrity rules are like telling your front desk: "Before you tell ANY guest their room number, you MUST look it up in the system. Every time. Even if you're 99% sure."

## When you'll encounter it
- AI concierge gives wrong propane levels because it "remembered" instead of checking
- AI reports a property has no reservations when it's actually fully booked
- AI tells a guest the wrong check-in time because it pattern-matched from a similar property
- Any time an AI states operational data (tank levels, task status, occupancy, dates) without verifying

## The rules
1. Never output operational data without a completed tool call returning that exact data
2. Tool call FIRST, text response SECOND — zero output before the tool returns
3. Self-check every response: does every fact trace to a tool result in this session?
4. No data = say "I don't have that data" — never fill in with guesses

## Related concepts
- [Trust Gate](trust-gate.md) — validation before publishing
- [Locked Values](locked-values.md) — code-computed numbers override AI narrative
- [Narrative Guardrails](narrative-guardrails.md) — preventing AI from outrunning its data
