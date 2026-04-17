# Nullable Column

## What it is
A database field that's allowed to be empty (`NULL`). The value is optional — existing rows don't need to have it, and new rows can leave it blank. Compare to a `NOT NULL` column, which forces every row to have a value.

## Tourism translation
Adding a "Dietary Restrictions" field to your guest intake form. Old guest files stay blank. New guests can fill it in or not. Nobody is forced to declare a restriction just because the form now has a field for it.

## When you'd see it
- Adding a new column to an existing table with lots of rows (making it NOT NULL would require backfilling every row)
- Optional metadata (a nickname, a secondary phone, a note)
- Fields that only apply to some records (e.g., a "cancellation reason" that's only set on cancelled reservations)
- Staged migrations where you add the column first, populate it later, then tighten to NOT NULL

## Why it matters (the additive migration superpower)
Adding a nullable column is a **non-breaking change**. No existing row needs updating. No existing code path needs to be aware of it. You can ship it to production during business hours without downtime. This is why nullable columns are the safe default when evolving a schema.

Compare: adding a `NOT NULL` column requires either (a) a default value for all existing rows, or (b) a migration that backfills every row before the column is enforced. Both are riskier.

## The catch
`NULL` is not `0`, not `""`, not `false`. In SQL, `NULL = anything` is always `NULL` (never `true`). You have to use `IS NULL` / `IS NOT NULL` for comparisons. Forgetting this is a common source of "why isn't my filter working" bugs.

## Learned from
FLOHOM inbox unmerge feature. Added `messages.pre_merge_conversation_id INTEGER` (nullable) to track where merged messages came from. Existing rows stay `NULL` because they were never part of a merge. Only new merges stamp this field — zero risk to the millions of pre-existing message rows.
