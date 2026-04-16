# Early Exit / Bail Out

## What it is
When code checks a condition at the start of a function and returns immediately if the condition fails, skipping all the heavy processing below. This saves time and resources by not doing unnecessary work. The risk is when the early exit is too aggressive and bails out before checking alternative data sources.

## Tourism Translation
**Like a concierge who checks if a guest exists in the system before pulling up their full profile.** If the guest isn't found, they stop immediately instead of searching through every database. But if they bail out too early, they might miss that the guest's info was logged in a different system — like a phone note instead of an email record.

## When you'll encounter it
- When you see `if (!data) return` at the top of a function
- When an API returns "not found" even though the data exists in a related table
- When optimizing performance by avoiding unnecessary database queries
