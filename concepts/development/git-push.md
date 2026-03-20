# Git Push

## What it is
Sends your local commits (saved snapshots) to a remote repository (like GitHub). Until you push, your changes only exist on your computer. After pushing, they're backed up online and visible to others.

## Tourism Translation
**Sending the checkout report to corporate headquarters.** Your hotel (local computer) recorded all the guest checkouts. But headquarters (GitHub) doesn't know about them until you send the report. Once you push, the records are in the central system — safe, backed up, and available to any other property (team member) that needs them.

## When you'll encounter it
- After committing changes locally
- Before deploying — most deploy platforms (like Render) pull from GitHub, so you need to push first
- When collaborating with others who need to see your changes

## Important
If you don't push, your commits are ONLY on your machine. If your laptop dies, those changes are gone. Pushing is your backup.

## Related concepts
- [Git Commit](./git-commit.md)
- [Deploy](../infrastructure/deploy.md)
