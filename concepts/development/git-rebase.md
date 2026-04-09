# Git Rebase

## What it is
Replaying your commits on top of someone else's newer commits, so the project history stays clean and linear. When you've been working on changes and someone else pushed new code to the same branch, `git rebase` takes your work, temporarily removes it, applies their changes first, then re-applies yours on top. If both of you changed the same lines, you'll need to resolve "conflicts" — deciding which version to keep.

## Tourism Translation
**Re-writing your schedule around newly confirmed bookings.** You planned renovations for Rooms 3-5 next week. But while you were planning, two new guest bookings came in for Room 3 and Room 4. Rebase means: accept the new bookings first (they're already confirmed), then reschedule your renovation around them. If there's a conflict (renovation overlaps a booking), you resolve it — maybe push the renovation to the following week. Same tasks, updated timeline.

## When you'll encounter it
- When `git push` fails because the remote has newer commits
- When you see "Updates were rejected because the remote contains work that you do not have locally"
- When collaborating with another person or AI that pushes to the same branch
- During the `git pull --rebase` workflow (pull others' changes, replay yours on top)
