# Silent Mode / skipSlackPost

## What it is
A flag you pass to a function or endpoint to suppress side effects (notifications, Slack posts, emails) during bulk operations. The primary work still happens — data gets written, records get created — but the downstream alerts stay quiet so you don't flood the team.

## Tourism Translation
**"Stocking all 15 minibars at once without ringing the guest-alert chime every time."**

Normally, when a minibar gets restocked, a polite chime rings in the lobby and the guest gets a notification. That's fine for one room at a time. But during quarterly inventory, you're touching all 15 rooms in 45 minutes. If the chime rang 15 times and 15 guests got notifications, the entire hotel would be annoyed.

So the GM flips a "silent inventory mode" switch. Minibars get stocked as normal, inventory gets logged, balances get updated — but no chimes, no notifications. Flip silent mode off when you're done.

## Why it matters

### Backfills without noise
During our review backfill of 1,011 historical reviews, firing the normal "post to Slack" hook on every insert would have flooded `#reviews` with 1,011 notifications and dozens of @channel alerts within minutes. Nobody wants their phone to explode because engineering ran a migration.

The backfill endpoint accepted `{ silent: true }`. Under the hood, it called `syncHostawayReviews({ skipSlackPost: true })`, which threaded the flag down into `ingestMention()`, which skipped the normal Slack hook. Data still landed in the DB. Team never saw a single alert during the backfill.

### The pattern
```js
// Signature
ingestMention(mention, { skipSlackPost: false }) // default: post to Slack
ingestMention(mention, { skipSlackPost: true })  // silent: skip the side effect

// Inside ingestMention
if (inserted.is_review && !skipSlackPost) {
  postReviewToSlack(inserted); // fire-and-forget
}
```

### Real FLOHOM example
```js
// POST /api/admin/reputation/sync-reviews
const force = body.force === true;
const skipSlackPost = body.silent === true;
const result = await syncHostawayReviews({ force, skipSlackPost });
```
One shared endpoint, two modes: normal (posts to Slack on every new review) and silent (runs quietly during bulk operations).

## In simpler terms
It's the "do not disturb" switch on your hotel room, but for systems. Everything keeps working — housekeeping still plans the day, the pool still gets cleaned — you just stop getting chimed at while it happens.
