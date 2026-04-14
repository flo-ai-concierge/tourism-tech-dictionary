# Sharp Rule (Business Logic Enforcement)

## What it is
A business rule that is enforced everywhere with zero exceptions — every webhook, every sync, every deploy, every user action. The term "sharp" means there's no ambiguity or soft edges. Example: "If a guest sent the last message and hasn't gotten a reply → the conversation is To-do. Period." This rule runs in the Hostaway webhook, GHL webhook, QUO webhook, Meta webhook, the sync engine, AND on every deploy as a data migration.

## Tourism Translation
**Like a hotel's "no room is ever marked clean until housekeeping confirms it" rule.** It doesn't matter if the guest said they barely used the room, if the front desk thinks it looks fine, or if the system glitched — until housekeeping physically inspects and marks it clean, it stays dirty in the system. The rule is enforced at every touchpoint: the PMS, the housekeeping app, the front desk terminal, and the manager's dashboard. No shortcuts, no overrides, no exceptions.

## Why it matters
- Soft rules get violated — if only 3 of 5 code paths enforce a rule, the 2 that don't become bugs
- Sharp rules are self-correcting — even if data gets corrupted, the next sync/deploy fixes it
- They simplify debugging — if the rule is sharp, violations point to a missing enforcement point, not a logic question

## FLOHOM's sharp rules
- Guest message + no reply = To-do (enforced in 6 places)
- Host reply to To-do = Done (auto-resolve)
- New guest message after Done = back to To-do

## Related concepts
- Status badge — visual representation of conversation state
- Auto-unstick pattern — fixing stuck processes automatically
