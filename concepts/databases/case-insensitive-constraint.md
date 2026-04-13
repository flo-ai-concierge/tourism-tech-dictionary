# Case-Insensitive Unique Constraint

## What it is
A database rule that treats different capitalizations of the same text as identical. For example, "John@gmail.com" and "JOHN@gmail.com" would be considered the same value, preventing duplicate entries regardless of how the text was typed.

## Tourism translation
Think of a guest registry at a hotel front desk. When "John Smith" checks in, you don't create a new guest profile just because someone typed "JOHN SMITH" in all caps on a different reservation. The registry recognizes them as the same person. A case-insensitive constraint does this automatically in the database.

## When you'll encounter it
- Guest email deduplication — preventing the same guest from getting multiple profiles
- Username or login systems where "Admin" and "admin" should be the same account
- Property name lookups where "FLOHOM 7" and "flohom 7" should match

## Related concepts
- `ON CONFLICT` handling — what to do when a duplicate is detected
- Database indexes — how the database speeds up these lookups
