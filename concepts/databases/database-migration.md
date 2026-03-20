# Database Migration

## What it is
A structured change to your database schema — adding tables, renaming columns, changing data types. It's like remodeling the structure of your data while the application is still running.

## Tourism Translation
**Renovating while guests are staying.** You need to add a new wing to the hotel, or convert a conference room into guest rooms, or change the numbering system on all the floors. But guests are currently staying. You can't shut down the whole hotel.

A database migration is that renovation. You're changing the building's structure while it's occupied. This is why it's high-risk:
- If you knock out a wall wrong, rooms become unusable (data loss)
- If you change room numbers without updating reservations, guests can't find their rooms (broken references)
- You need a rollback plan — if the renovation goes wrong, you need to be able to undo it

## When you'll encounter it
- Adding a new feature that needs a new database table
- Changing how existing data is structured
- Adding a column (like adding a closet to every room)
- Removing a column (like removing the landline phone from every room)

## Why it's high-risk
Your database is your source of truth. If a migration corrupts data, you might lose real guest records, real reservation data, real conversations. Always:
1. Back up before migrating
2. Test on a copy first
3. Have a rollback plan

## Related concepts
- [Environment Variables](../security/environment-variables.md)
