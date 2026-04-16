# Targeted Sync

## What it is
Syncing data for just one specific record or conversation instead of running a full sync across everything. Much faster for debugging or fixing individual gaps. Instead of re-processing thousands of records to fix one, you point the sync at exactly what's broken.

## Tourism translation
Like sending housekeeping to one specific room instead of re-cleaning the entire hotel to fix one missed room. You know which room needs attention, so go directly there instead of starting from Room 1 and working through all 200.

## When you'd see it
- A guest's messages are missing — sync just their conversation
- A specific property's data is stale — refresh just that property
- Debugging a sync issue — test with one known case before running the full batch

## How it works
Accept a filter parameter (phone number, conversation ID, property ID) and run the same sync logic but scoped to just that record. Skip the full conversation scan.

## Learned from
Built ?phone=+1XXX targeted sync for QUO on Apr 16, 2026. Processing 200+ conversations took minutes and often timed out. Targeted sync for one guest completes in seconds — essential for debugging.
