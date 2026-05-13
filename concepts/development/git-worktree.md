# Git Worktree

## What it is
A way to check out a second branch of your codebase into a separate folder — so you can work on two things at the same time without switching back and forth. Both folders share the same git history but have different files on disk. Changes in one don't affect the other until you deliberately merge them.

## Tourism Translation
**"Like a hotel running a live wing and a renovation wing simultaneously — same building, same ownership, but guests in the live wing don't see the construction, and the renovation crew doesn't disrupt check-ins."**

The main branch is the live hotel — guests are checking in, everything is running. The worktree is the renovation wing — you're building new rooms, testing layouts, making a mess. When the renovation is done and inspected, you open those rooms to guests (merge to main). Until then, the two wings are completely separate.

## When you'd see it
- Claude Code uses worktrees to isolate AI-generated changes from your live codebase during development
- Running a dev preview server against a feature branch while main stays untouched
- Working on two separate features at the same time without stashing/unstashing

## Gotcha
Files written to the main project path won't appear in the worktree's dev server — and vice versa. They're separate folders on disk even though they share git history. Always confirm which path your dev server is reading from.

## Learned from
May 13, 2026 — new API files were written to the main project path but the preview server ran from the worktree. The admin page returned 404 until files were copied to the correct folder.
