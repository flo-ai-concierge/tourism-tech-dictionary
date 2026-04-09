# Idempotent Seed Script

## What it is
A script that's safe to run multiple times — it checks if data already exists before inserting, so it never creates duplicates. "Idempotent" means "doing it twice produces the same result as doing it once."

## Tourism Translation
**"Like a housekeeper who checks if towels are already there before bringing new ones — running the checklist twice doesn't mean double towels."**

A new housekeeper might bring 4 fresh towels to every room without checking. Run that twice and you have 8 towels crammed into a small bathroom. An experienced housekeeper checks first: towels there? Skip. No towels? Bring 4. Either way, you end up with exactly 4 towels.

Idempotent seed scripts work the same way. Before inserting check-in steps for a property, the script asks: "Does this property already have steps?" If yes, skip. If no, insert. You can run the script 10 times and get the same result as running it once.

## Why it matters

### Safe re-runs
Deployments sometimes fail halfway. With an idempotent script, you just run it again without worrying about duplicates.

### Production safety
The scariest thing about running scripts against a live database is creating duplicate records that confuse guests. Idempotency eliminates that fear.

### Team-friendly
Multiple team members can run the same setup script without coordinating who already ran it.
