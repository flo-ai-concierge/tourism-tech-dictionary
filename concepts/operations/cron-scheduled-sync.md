# Cron / Scheduled Sync

## What it is
A task the computer runs automatically on a schedule: "every 1 hour," "every day at 8 AM," "every Monday at 9:00." Set it once, it runs forever without manual triggers.

## Tourism Translation
**"Housekeeping showing up at 11 AM every day without being told."**

You don't text the housekeeping crew every morning. They have a schedule. 11 AM = clean the checked-out rooms. 2 PM = restock minibars. 9 PM = evening turndown. The work happens on autopilot because the schedule is a standing agreement.

Cron jobs are the same. `0 8 * * *` in cron syntax = "run this every day at 8:00 AM."

## Why it matters

### Automation without human intervention
Our Hostaway review sync runs every hour automatically. The weekly guest-relations report posts to Slack every Monday at 8 AM. The daily schedule briefing fires every morning. Nobody has to remember to trigger any of these.

### setInterval vs cron
Our implementation uses `setInterval` with a 1-hour tick rather than a true cron. The trade-off: setInterval resets whenever the server restarts (so if Render redeploys at 3:47 PM, the next sync fires at 4:47 PM, not at the top of the hour). True cron would fire at exact clock times. For our purposes, the hour-offset doesn't matter — we just want "roughly every hour."

### Real FLOHOM example
```js
const REVIEWS_SYNC_INTERVAL = 60 * 60 * 1000; // every 1 hour
setTimeout(() => syncHostawayReviews(), 180_000);  // initial run 3 min after boot
setInterval(() => syncHostawayReviews(), REVIEWS_SYNC_INTERVAL);
```
Fire-and-forget scheduling. The server runs the sync on this interval for the life of the process.

## In simpler terms
It's an alarm clock that actually does the work when it rings, instead of just waking you up.
