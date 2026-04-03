# Source-of-Truth Hierarchy

## What it is
A ranked list that defines which system wins when two systems disagree about the same fact. The transactional system (where money and bookings actually flow) always beats the knowledge system (where notes and context are stored). This prevents stale notes from overriding current reality.

## Tourism Translation
**The PMS reservation record vs. the manager's notebook.**

Your property manager's notebook says "Port Noir was sold to Dwight in February, no more bookings." But the PMS shows 13 confirmed nights and $7,948 in revenue for Port Noir this year. Which one do you believe? The PMS — because that's where real money flows. The notebook is useful context, but it's not the system of record.

In hospitality tech, the hierarchy is:
1. **PMS / booking system** (reservations, revenue, guest data) — this is truth
2. **Channel APIs** (real-time availability, pricing) — this is current state
3. **Knowledge bases / Airtable** (context, property notes, team intel) — this is helpful but subordinate
4. **Meeting notes / internal docs** — this is the weakest source; useful for "why" but never for "what"

## Why it matters
When systems disagree and there's no hierarchy, people make decisions based on whichever source they saw last. A revenue report might say "Port Noir has zero bookings" because it read a stale knowledge base entry, while the actual PMS shows active bookings. Without a hierarchy, the wrong source wins by accident.

## Key principles
1. **Transactional systems beat knowledge systems** — always
2. **If a note contradicts a database record, the database wins** — investigate the note, don't override the record
3. **Label the source** — when presenting data, say where it came from so the reader knows its authority level
4. **Stale knowledge is dangerous** — schedule regular audits of knowledge bases against transactional truth
5. **Document the hierarchy** — write it down so every team member and every AI system follows the same rules

## Related concepts
- [Database Migration](../databases/database-migration.md)
- [Locked Values](../ai/locked-values.md)
