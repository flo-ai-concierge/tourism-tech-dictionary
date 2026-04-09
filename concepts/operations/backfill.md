# Backfill

## What it is
Going back in time to fill in historical data that was missing, skipped, or never captured. A one-time bulk operation that catches your system up to reality, after which the normal live sync can keep things current going forward.

## Tourism Translation
**"Manually entering the guest register for the last three months of stays that never got logged."**

A new GM joins and realizes the physical guest logbook has a 3-month gap. Bookings happened, guests stayed, money changed hands — but nothing was recorded. The GM sits down with old emails, Airbnb dashboards, and calendar screenshots and manually fills in every missing entry. Once the logbook is caught up, the normal daily workflow can take over.

## Why it matters

### You don't always start from zero
When a new feature launches, you often have to fill in historical data so the feature has something to work with on day one. Our `#reviews` Slack channel needed every historical review backfilled before the team could use it — otherwise the channel would only show brand-new reviews and the team wouldn't see the 1,011 reviews we already had.

### Backfill is different from sync
- **Sync** = "pull whatever's new since last time" (incremental, scheduled, ongoing)
- **Backfill** = "pull everything historical once" (one-time, exhaustive, run manually)

The two have different safety characteristics. Sync is frequent and must be cheap. Backfill is rare, runs on all of history, and must be careful not to flood downstream systems.

### Silent mode during backfill
When we backfilled 1,011 reviews into the Slack channel, we had to be careful: if each inserted review fired the normal "post to Slack" side effect, the channel would explode with 1,011 real-time notifications and @channel pings. The fix was a `silent: true` flag on the backfill path that suppressed the Slack side effect while still writing to the database.

### Real FLOHOM example
1. Forced a 5-year Hostaway review sync → pulled 874 historical reviews into the DB
2. Merged in 524 PDF-parsed Google reviews → now 1,398 total in DB
3. Triggered a Slack backfill endpoint that posted them all to #reviews in chronological order with 1.5s throttle
4. Total runtime: ~25 minutes
5. After that, the normal hourly sync handles new reviews going forward

## In simpler terms
Catching up your journal after two months of travel. You sit down with receipts and photos, write everything you remember, and once you're back in sync you write daily again like normal.
