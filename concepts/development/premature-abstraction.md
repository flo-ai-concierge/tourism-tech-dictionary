# Premature Abstraction

## What it is
Building a generalized, flexible solution for a problem you don't actually have yet. Instead of writing three specific lines of code for three known cases, you invent a "framework" or "abstraction layer" that could theoretically handle ten cases — most of which will never come up.

## Tourism Translation
**Installing 50 specialty tea options in every guest room because someone, someday, might want lapsang souchong.**

Versus stocking the three teas most guests actually ask for. The 50-tea setup looks thorough and "complete." But 47 of those boxes will expire unopened, take up counter space, and make the room feel cluttered. Meanwhile the three teas guests actually want are buried in the clutter.

Good hospitality — and good engineering — starts with what guests actually need, not what they might hypothetically want.

## Why it matters
Premature abstraction is one of the most common reasons software gets slow, confusing, and hard to change. Every extra layer of "flexibility" is:
- More code to read
- More places for bugs to hide
- More mental overhead for the next person
- A constraint on future direction (abstractions lock in assumptions)

The guiding rule: **"Three similar lines is better than a premature abstraction."** If you have three concrete cases, write three concrete solutions. If the pattern emerges over time, refactor into an abstraction THEN — when you know what the abstraction should actually look like.

## Real example
After fixing FLO's turnover blindness (Apr 20, 2026), the obvious next step looked like "generalize the hedge pattern to all turnover-sensitive questions — key pickup timing, housekeeping access, etc."

But we had zero evidence those other cases were failing. The fix we shipped already covered early check-in, early parking, early access, and late checkout. Generalizing further without real failures would be building for imaginary requirements. The right call: ship what we have, watch real traffic for 1-2 weeks, then decide what to add based on actual data.

## Related concepts
- [Burn It Down Rewrite](burn-it-down-rewrite.md) — when the opposite happens (too many patches layered on)
- [Early Exit Bail-Out](early-exit-bail-out.md) — simplicity over complexity
- [Facade Pattern](facade-pattern.md) — a GOOD abstraction, when there's real evidence for it
