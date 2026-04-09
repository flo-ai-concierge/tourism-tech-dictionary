# Monolithic File

## What it is
A single giant file containing all the code for a system — everything from configuration to business logic to data definitions lives in one place. Easy to find things when it's small, but becomes fragile and hard to maintain as it grows past a few hundred lines. Changes in one section can accidentally break another.

## Tourism Translation
**One employee who does everything.** Imagine one person at a small B&B who handles check-in, cleaning, cooking, maintenance, and bookings. Works great for 1-2 rooms. Now scale that to 15 properties — that person is overwhelmed, mistakes happen, and if they call in sick, everything stops. The solution: hire specialists. Same with code — split the monolith into focused modules.

## When you'll encounter it
- When a single file grows past 500-1000 lines
- When making a small change requires reading through thousands of lines of unrelated code
- When multiple features are tangled together in one file and a bug in one breaks another
