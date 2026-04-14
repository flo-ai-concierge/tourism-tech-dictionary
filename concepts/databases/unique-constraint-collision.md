# Unique Constraint Collision (Error 23505)

## What it is
A database error that occurs when you try to insert or update a record with a value that must be unique (like an email address), but another record already has that value. PostgreSQL rejects the operation with error code 23505. The fix: catch the error and retry the operation without the conflicting field.

## Tourism Translation
**"Trying to assign Room 301 to two different guests at the same time."**

The booking system rejects it — you can't double-book a specific room. The fix isn't to force it; it's to assign the second guest to the next available room instead. Similarly, when two guest records claim the same email, the system skips the email update rather than crashing.

## Why it matters
In FLOHOM's database, the `guests` table has a unique index on email addresses. When syncing reservations from Hostaway, two different guest records occasionally share the same email (e.g., a property manager booking for multiple guests). Without handling this collision:
- The entire sync process crashes
- No new reservations sync until someone manually fixes it
- This caused a 32-day sync outage (Mar 12 – Apr 14, 2026)

The fix: wrap the UPDATE in a try/catch. If error 23505 fires, retry the update without the email field. The guest record still syncs — it just keeps its old email.

## In simpler terms
Two guests can't have the same email in the system. When they try, instead of crashing, the system says "fine, I'll update everything except the email" and moves on.
