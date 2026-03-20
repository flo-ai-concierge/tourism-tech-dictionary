# Git Commit

## What it is
A snapshot of your code at a specific point in time. When you "commit," you're saving the current state of your files with a message describing what changed. Every commit has a unique ID (a hash like `db55e4f`) and a timestamp.

## Tourism Translation
**Guest checkout confirmed and recorded.** When a guest checks out, the front desk records the exact state of the stay: dates, charges, room condition, any incidents. That record is locked in, timestamped, and stored. You can always go back and look at exactly what happened during that stay.

Each commit is like a checkout record — it captures the exact state of the "property" (your code) at that moment. If something goes wrong later, you can look back at any past "checkout" to see what changed.

## When you'll encounter it
- Every time you save progress on code changes
- When reviewing what changed and when (git log)
- When you need to undo something — you can go back to a previous commit

## The commit message matters
Just like a checkout note that says "room was fine" is useless, a commit message that says "fixed stuff" helps nobody. Good commit messages explain WHY the change was made, not just WHAT.

**Bad:** "Updated code"
**Good:** "Fix Render OOM: switch to webpack build with 384MB memory limit"

## Related concepts
- [Git Push](./git-push.md)
- [Deploy](../infrastructure/deploy.md)
