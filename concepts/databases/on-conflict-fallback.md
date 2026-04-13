# ON CONFLICT Fallback

## What it is
A database instruction that says "if this insert would create a duplicate, do something else instead of crashing." Common strategies are: update the existing record, or simply skip the insert. This prevents your application from breaking when it encounters data that already exists.

## Tourism translation
Imagine a hotel that accidentally double-books a room. Instead of telling the second guest "sorry, system error, go away" (crashing), a smart hotel either upgrades them to another room (update) or recognizes they're already checked in (skip). An ON CONFLICT fallback is that automatic recovery plan built into your reservation system.

## When you'll encounter it
- Syncing guest data from multiple booking platforms (Airbnb, VRBO, direct) — the same guest might appear from different sources
- Importing reviews or messages that might already exist in your database
- Any automated data pipeline where the same record could arrive twice

## Related concepts
- Upsert — the combined "insert or update" operation
- Idempotency — designing operations so running them twice produces the same result as running once
- Unique constraints — the rules that define what counts as a "duplicate"
