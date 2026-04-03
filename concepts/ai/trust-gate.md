# Trust Gate

## What it is
A verification checklist run against AI-generated output before it reaches users. It checks that locked values are present, critical numbers fall within expected ranges, deprecated or wrong numbers don't appear in narrative text, and enforcement was applied correctly. If any check fails, the output is blocked or flagged.

## Tourism Translation
**The pre-arrival inspection checklist before a VIP guest arrives.**

Before a high-value guest checks in, you walk the property: Is the AC working? Are the towels stocked? Is the welcome basket there? Is the pool clean? You don't assume everything is fine — you verify each item against a checklist. If anything fails, you fix it before the guest sees the room.

A trust gate does the same thing for analytics reports. Before the CEO or revenue manager sees the numbers, the system verifies: Are the commission totals correct? Are deprecated metrics gone? Do the narrative sections match the data? If something fails, the report doesn't go out until it's fixed.

## Why it matters
An AI can produce a beautifully written report that contains wrong numbers. It looks professional, reads well, and is completely misleading. The trust gate catches this before it reaches decision-makers. It's the difference between "the report looks good" and "the report IS good."

## How to build one
1. Define expected ranges for every critical metric (e.g., commission should be $50K-$80K)
2. List deprecated values that should never appear (e.g., old counts, old averages)
3. Check that locked values match between the data layer and the narrative layer
4. Run it as a script or automated test — not a manual review
5. Log pass/fail results so you can track trust over time

## Related concepts
- [Locked Values](./locked-values.md)
- [Narrative Guardrails](./narrative-guardrails.md)
