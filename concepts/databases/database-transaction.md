# Database Transaction (BEGIN / COMMIT / ROLLBACK)

## What it is
A way to wrap a series of database writes so they either **all succeed together** or **all fail together** — never a half-finished state. You say `BEGIN`, do your work, and either `COMMIT` (save everything) or `ROLLBACK` (throw it all away). If anything crashes mid-way, the database automatically rolls back, leaving no trace.

## Tourism translation
A restaurant ticket. Either the whole order goes to the kitchen and hits the table together, or the waiter cancels the ticket and nothing cooks. You can't have the salad go out without the entrée. The table gets the complete experience or none of it.

## When you'd see it
- Money transfers (debit one account AND credit another, never just one)
- Merging records (move messages AND update tombstone AND write audit note — all or nothing)
- Anything that modifies multiple related rows
- Operations where a mid-flight crash would leave inconsistent data

## Why it matters
Imagine merging two conversations without a transaction: you move 52 messages to the target, the database crashes before you can set the tombstone flag on the source — now you have 52 messages missing from one thread and duplicated in another, with no way to untangle which is which. Transactions prevent that entire category of bug.

## The three commands
- `BEGIN` — "start recording my changes, don't save them yet"
- `COMMIT` — "save everything I did, make it permanent"
- `ROLLBACK` — "throw away everything, act like I did nothing"

Most languages wrap this in a `try/finally` — if any step throws, roll back; otherwise commit.

## Tip for testing
Wrap your destructive test queries in `BEGIN...ROLLBACK` to exercise the full logic against real data without actually changing anything. Inspect results mid-transaction, then roll back to leave the database untouched.

## Learned from
FLOHOM inbox merge/unmerge endpoints. Both wrap the full operation (move messages, tombstone source, recalculate metadata, write audit note) in a single transaction. A round-trip test used `BEGIN ... ROLLBACK` against real production data to prove the logic works without modifying anything.
