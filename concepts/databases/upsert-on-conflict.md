# Upsert (ON CONFLICT)

## What it is
A database operation that inserts a new row, but if a row with the same unique key already exists, it updates that existing row instead of creating a duplicate. The word "upsert" combines "update" and "insert."

## Tourism translation
Like updating a guest's profile when they rebook. If Sarah Smith books FLOHOM 5 again, you don't create a second guest file — you update her existing one with the new reservation dates. The guest email is the "unique key" that tells you it's the same person.

## When you'll encounter it
- Airtable guidebook sync uses `airtable_record_id` as the unique key — if the guidebook exists, update it; if not, create it
- Service sync from Airtable uses the same pattern with `airtable_record_id`
- Hostaway reservation sync uses `hostaway_reservation_id` to avoid duplicate bookings

## How it works
```sql
INSERT INTO guidebooks (airtable_record_id, title, content)
VALUES ('rec123', 'Internet', 'WiFi: FLO1 Starlink...')
ON CONFLICT (airtable_record_id) DO UPDATE SET
  title = EXCLUDED.title,
  content = EXCLUDED.content,
  updated_at = NOW();
```
If `rec123` doesn't exist: creates it. If it does: updates title and content.

## Related concepts
- [Unique Constraint Collision](./unique-constraint-collision.md) — what happens without ON CONFLICT
- [Airtable Linked Record](./airtable-linked-record.md) — the source data being upserted
