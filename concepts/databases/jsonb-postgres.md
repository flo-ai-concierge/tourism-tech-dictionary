# JSONB (PostgreSQL JSON Binary)

## What it is
A PostgreSQL column type that stores JSON data in an indexed binary format. Unlike a plain TEXT column holding a JSON string, JSONB is **queryable** — you can filter, sort, and index by fields *inside* the JSON without unpacking the whole thing.

## Tourism translation
A guest-preferences folder at the front desk where each page is pre-sorted and tagged. Want to find every guest who prefers feather pillows? You flip to the "pillows" tag across all folders instead of reading every page. Storing the notes as a pile of loose paper (plain TEXT) would force you to read each folder from start to finish.

## When you'd see it
- Storing flexible per-record settings that don't deserve their own column (preferences, metadata)
- External API payloads you want to preserve whole but also query parts of (Airtable records, Hostaway responses, AI outputs)
- Schemaless-ish data that might grow new fields over time without a DB migration each time

## Why it matters
It gives you the flexibility of document databases (MongoDB) while staying in the same Postgres you already use for everything else. No second datastore, one query language, one backup.

## The SQL pattern
```sql
-- Table definition
CREATE TABLE marinas (
  amenities JSONB DEFAULT '{}'::jsonb
);

-- Insert with JSON
INSERT INTO marinas (amenities)
VALUES ('{"floating_docks": true, "pump_out": "permanent"}'::jsonb);

-- Query a field inside the JSON
SELECT * FROM marinas
WHERE amenities->>'pump_out' = 'permanent';

-- Merge new fields without overwriting
UPDATE marinas
SET amenities = amenities || '{"fuel_dock": true}'::jsonb
WHERE id = 1;
```

## JSONB vs JSON
Postgres has two JSON types:
- **JSON** — stores the raw text as-is. Faster to insert, slower to query.
- **JSONB** — parsed and stored in binary. Slightly slower to insert, much faster to query and index. **Almost always the right choice.**

## Gotchas
- `->` returns JSONB, `->>` returns text. Use `->>` when comparing to strings.
- Indexing JSONB fields requires GIN indexes for best performance.
- Don't abuse it — if a field is always present and always the same shape, give it a real column.

## Learned from
FLOHOM marinas table (Apr 20, 2026). The `amenities` and `regulatory` columns are JSONB because Brian hasn't defined the exact fields yet — we wanted to accept whatever shape he lands on without re-migrating the table. Market Reports also use JSONB for the AI-generated payload since the structure evolves.
