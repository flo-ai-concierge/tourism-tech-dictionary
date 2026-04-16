# Background Job (Fire-and-Forget)

## What it is
Starting a long-running task on the server and immediately telling the user "started!" instead of making them wait for it to finish. The server continues processing in the background while the user can do other things. The HTTP request returns instantly.

## Tourism translation
Like a guest requesting extra towels at the front desk. The desk agent confirms "on its way!" immediately — they don't make the guest stand there while housekeeping walks to the linen closet, grabs towels, and delivers them. The guest goes back to their room, and the towels arrive in the background.

## When you'd see it
- Long data migrations or backfills that process hundreds of records
- Email sending that takes time for each recipient
- Report generation that crunches large datasets
- Any API call that would otherwise timeout

## How it works
The server starts the task as a Promise without awaiting it, returns a response to the client immediately, and the task runs to completion in the Node.js event loop.

## Learned from
QUO voicemail backfill processing 300+ calls at 1/sec was timing out as a normal HTTP request. Switched to fire-and-forget on Apr 16, 2026 — returns instantly, processes in background.
