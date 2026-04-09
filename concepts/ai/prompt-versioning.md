# Prompt Versioning

## What it is
Labeling each revision of an AI's system prompt with a version number and storing that version alongside every output the AI produces. Lets you trace which rules were in effect when a specific reply was generated.

## Tourism Translation
**"Dating each revision of your check-in script."**

Your front desk script changes over time. V1 said "Welcome. Here's your key." V2 added "And here's the Wi-Fi password." V3 added a pitch for the spa. Every time you revise it, you write a date on the new version and keep the old one in a drawer.

If a guest complains "I wasn't told about the pool hours at check-in," you check the date of their stay against your script history. If you were on V1 at the time, you know the pool hours weren't in the script — it's a process gap, not a staff failure.

## Why it matters

### AI behavior evolves quickly
We shipped three versions of the FLO review-reply prompt in a single day:
- **v1** — initial "warm and human" rules
- **v2** — added "no calls to action, no promises to fix"
- **v3** — added "no em dashes, no compensation offers, handle 'tried to reach us' gracefully, accept operator context"

Each version catches new edge cases Brian flagged. If we didn't track versions, we wouldn't know which rules were active when a given reply was generated.

### Audit trail
Every draft row in `reputation_reply_drafts` stores `system_prompt_version`. If a team member later says "this reply was too defensive, why?" we can pull the draft, see which prompt version was live, and either fix the prompt or confirm the version was fine and the model just produced a one-off bad reply.

### Safe rollbacks
If v3 of a prompt starts producing worse output than v2 for some reason, you can instantly roll back to v2 without re-releasing anything: just bump the version marker in code back to v2 and redeploy.

### Real FLOHOM example
```js
const SYSTEM_PROMPT_VERSION = "flohom-reply-v3";
// ...
await query(
  `INSERT INTO reputation_reply_drafts
    (mention_id, draft_text, model, system_prompt_version, ...)
   VALUES ($1, $2, $3, $4, ...)`,
  [mentionId, draftText, MODEL, SYSTEM_PROMPT_VERSION, ...]
);
```
Every draft carries its provenance.

## In simpler terms
It's a date stamp on every recipe the kitchen uses. If a dish comes out wrong, you can trace back which version of the recipe was in the book that day.
