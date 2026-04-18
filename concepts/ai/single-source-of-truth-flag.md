# Single Source of Truth Flag (in AI Prompts)

## What it is
When prompting an AI, give it ONE canonical field that holds the answer to an important question. Don't also send raw values that would let the AI compute a different answer by reasoning over them. If you give the AI both a flag AND the raw values, the AI may ignore your flag and "do the math" itself, which often produces the wrong answer.

## Tourism translation
**"Don't give the front desk five conflicting clues — give them one definitive status."**

Imagine the front desk has to decide: is Room 412 ready for a new guest? You could give them five raw signals — last guest's checkout time, current housekeeping log, photo from the inspection, status from the property management system, and a verbal note from the lobby manager. They'll waste time reconciling them, and they'll get it wrong sometimes.

OR you could give them ONE field: `room_412_status = "ready"`. The other systems are still updated in the background, but the front desk reads ONLY that field. No reconciliation, no second-guessing, no math. They issue the key.

## The pattern
Compute the canonical answer in code. Send only that to the AI. Do NOT send the raw inputs that you used to compute it.

```js
// BAD — gives FLO ammunition to override our flag
{ 
  alertTimeET: "22:00 ET",
  checkInTime: "15:00 ET",
  checkOutTime: "10:00 ET",
  isCleanerWindow: false   // FLO ignores this and does 22 > 10 = "after checkout"
}

// GOOD — only the canonical answer
{
  relationship: "during_stay"
}
```

## When you'd see it
- AI assistants that need to decide categorical states (occupied/vacant, eligible/ineligible, on-time/late).
- Decision-making prompts where multiple signals could lead to different conclusions.
- Any case where the AI might "reason over" raw data to second-guess a pre-computed answer.

## Why it matters
We had FLO Minut deciding between four states: `during_stay`, `before_checkin`, `after_checkout`, `vacant`. The code computed the right state. But the prompt also passed raw times — alert hour, check-in hour, checkout hour. FLO consistently ignored the state flag and did math: "22:00 > 10:00, must be after checkout." Stripping the raw times from the context fixed it instantly. The state flag was always there; FLO was just using shinier toys.

## Learned from
FLOHOM FLO Minut prompt (Apr 18, 2026). Companion lesson: list ONLY the relationship values your code actually emits in the prompt. If you list four real values plus one hypothetical ("turnover"), the AI WILL use the hypothetical word verbatim.

## Related concepts
- [`ai/locked-values`](locked-values.md) — same principle but for numbers
- [`ai/data-integrity-rules`](data-integrity-rules.md) — preventing fabrication
- [`ai/llm-hallucination-vs-upstream-bug`](llm-hallucination-vs-upstream-bug.md) — when the AI "ignores" your flag, check if you also sent it the raw signals
