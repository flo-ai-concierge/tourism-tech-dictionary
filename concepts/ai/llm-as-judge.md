# LLM-as-Judge

## What it is
Using one AI model to grade another AI model's responses — like having a supervisor review an employee's work. A cheaper, faster model scores the main model on accuracy, tone, helpfulness, and policy compliance.

## Tourism translation
Like having a quality inspector visit each property after housekeeping, scoring cleanliness, presentation, and guest-readiness on a 1-5 scale — without the guest ever seeing the inspector. The inspector files a report, and management reviews anything below a 3.

## When you'll encounter it
- Automated quality assurance for AI concierges or chatbots
- Building dashboards that track AI response quality over time
- Detecting hallucinations, policy violations, or off-brand tone automatically

## How it works
```
Guest asks question → Main AI (Sonnet) responds → Judge AI (Haiku) scores the response
Scores: accuracy=4, helpfulness=5, tone=4, policy=pass, overall=4
Flags: [] (no issues)
```
If the judge finds a problem (hallucination, policy violation), it triggers an alert.

## Related concepts
- [Prompt Caching](./prompt-caching.md) — the judge prompt is cached to reduce scoring cost
- [Classification Tiers](./classification-tiers.md) — routing messages by complexity
