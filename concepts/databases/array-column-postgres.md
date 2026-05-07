---
term: Array Column (PostgreSQL TEXT[])
category: databases
session: FLOTurn Phase 1 — May 2026
---

## Plain English

A database column that holds a **list of values** instead of just one. Instead of creating a separate table or row for each item, you store all the items together in one column. You can add items to the list (`array_append`), check if something is in the list (`= ANY(column)`), or count how many items are in the list.

Used in FLOTurn for: storing multiple completion photos per cleaning task (`photo_urls TEXT[]`), and multiple problem report photos (`photo_urls TEXT[]`).

## Tourism / Hospitality Analogy

A hotel room's "amenities" field that lists: WiFi, Pool, Gym, Spa — all in one box instead of needing a separate row for each amenity. You open that one box and see everything the room offers, rather than looking up a separate "room amenities" table for each room.

## Technical Detail

```sql
-- Column definition
photo_urls TEXT[] NOT NULL DEFAULT '{}'

-- Add one photo to the list
UPDATE cleaning_tasks
SET photo_urls = array_append(photo_urls, 'https://...')
WHERE id = $1;

-- Check if column is empty
WHERE array_length(photo_urls, 1) IS NULL

-- Check if a value exists in the array
WHERE 'https://...' = ANY(photo_urls)
```

## When to Use vs. Junction Table

Use an array column when:
- The items have no metadata of their own (just URLs, tags, IDs)
- You never need to query individual items in complex ways
- Order doesn't matter or can be preserved by position

Use a junction table when:
- Each item has its own fields (uploaded_by, created_at, status)
- You need to update/delete individual items efficiently
- Items are shared across multiple parent records
