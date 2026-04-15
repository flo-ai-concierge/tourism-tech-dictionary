# Airtable Linked Record

## What it is
A field in one Airtable table that points to a row in another table, creating a relationship between them. When you link a guidebook entry to a FLOHOM property, you're creating a linked record — the guidebook "belongs to" that property.

## Tourism translation
Like a reservation linking to a specific property. One booking belongs to one FLOHOM. The reservation card has a field that says "Property: FLOHOM 5" — that's the link. Click it and you jump to the property's full record.

## When you'll encounter it
- FLOHOM Guidebooks table links each entry to the FLOHOM property table
- Services table links upsells to the properties that offer them
- Any time you see a clickable reference from one Airtable row to another

## How it works
```
Guidebooks Table:
  Title: "Internet"
  FLOHOM: [FLOHOM 01]  <-- linked record pointing to FLOHOM table

FLOHOM Table:
  FLOHOM ID: "01"
  Nickname: "Bay Escape"
  Guidebooks: [Internet, Rooftop, Rules...]  <-- reverse links auto-populated
```

## Related concepts
- [Upsert / ON CONFLICT](./on-conflict-fallback.md) — how linked records sync to PostgreSQL
