# Facade Pattern

## What it is
A thin wrapper file that re-exports functions and data from other modules, so all consumers (the files that import it) never need to change their imports. The facade doesn't contain real logic — it just points to where the logic lives. This lets you reorganize the internals without breaking anything external.

## Tourism Translation
**The hotel front desk.** Guests always come to the same front desk for everything — check-in, room service, pool towels, restaurant reservations. Behind that desk, requests get routed to housekeeping, the kitchen, the concierge, maintenance. The guest never needs to know which department handles what. If the hotel reorganizes its back-of-house staff, the guest experience at the front desk stays exactly the same.

## When you'll encounter it
- When a large file is being split into smaller modules but other files already depend on it
- When you see a file that's mostly `require()` and `module.exports` with very little logic
- When refactoring code without wanting to update every file that imports from it
