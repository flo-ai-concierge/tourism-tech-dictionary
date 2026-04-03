# Locked Values (Enforcement Layer)

## What it is
A pattern where critical numbers are computed in code (not by AI), then passed to an AI model as read-only facts. After the AI generates its response, the system overwrites any AI-computed numbers with the pre-computed locked values. The AI can explain, compare, and recommend — but it cannot change the numbers.

## Tourism Translation
**The night auditor's final folio vs. the front desk agent's estimate.**

When a guest checks out, the front desk agent might say "your total is around $1,200." But the night auditor's system has already computed the exact total — $1,147.63 — based on actual room charges, taxes, minibar, parking. The night auditor's number is the locked value. It doesn't matter what the front desk agent *thinks* the total is. The system enforces the real number.

In AI-powered analytics, the same principle applies: the database computes the real commission, the real revenue, the real occupancy. The AI explains what those numbers mean and what to do about them — but it cannot override the audited total.

## Why it matters
AI models are excellent narrators but unreliable calculators. They can add wrong, hallucinate totals, or reference outdated numbers from their training. If your revenue report says "$2.4M in commission leakage" because the AI computed it wrong, that's a trust-destroying mistake. Locked values prevent this by making it physically impossible for the AI to output the wrong number.

## Key principles
1. **Code computes, AI narrates** — never the reverse
2. **Enforcement runs after AI output** — catch and correct any drift
3. **Log corrections** — when the AI tried a different number, record what it said vs. what was locked, so you can improve the prompt over time
4. **Cap editorial estimates** — AI can suggest "potential revenue," but cap it against locked actuals so it can't claim $100K opportunity when total revenue is $60K

## Related concepts
- [Trust Gate](./trust-gate.md)
- [Narrative Guardrails](./narrative-guardrails.md)
