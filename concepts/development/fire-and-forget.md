# Fire-and-Forget

## What it is
Calling another system (an API, a background job, a notification) without waiting for it to complete. You trigger it, keep moving, and trust that if anything goes wrong the failure will be logged but won't block your main work.

## Tourism Translation
**"Dropping a note in the back-office inbox and walking away."**

A guest mentions they'd like extra pillows. You scribble it on a note, drop it in the housekeeping tray, and immediately continue checking in the next guest. You don't stand there watching the housekeeper read it. You trust the tray works. If the note gets lost, you'll hear about it later, but your check-in flow doesn't stop.

## Why it matters

### It keeps the main path fast
The moment a guest review lands in our database, we fire-and-forget a Slack post. The database INSERT doesn't wait for Slack to respond. If Slack is down for 10 seconds, the review still gets saved, and the Slack post retries silently in the background.

### Failure isolation
If the side effect fails, the primary operation is untouched. A broken Slack webhook doesn't corrupt review data. A down Anthropic API doesn't block the detail page from loading.

### Real FLOHOM example
In `flo-reputation.js`, after a new review is inserted:
```js
if (inserted.is_review) {
  import("./slack-reviews.js")
    .then(({ postReviewToSlack }) => postReviewToSlack(inserted))
    .catch((err) => console.error("Slack post failed:", err.message));
}
```
Notice there's no `await`. The function returns the inserted review immediately. Slack posting happens in the background. If it fails, we log and move on. The review is still in the DB.

## Why it's risky
Fire-and-forget side effects can fail silently. You need good logging and monitoring to catch failures that would otherwise go unnoticed. Don't fire-and-forget anything that absolutely must succeed (like payment processing).

## In simpler terms
It's like sending a text message and not staring at the "delivered" indicator. You sent it, you trust the phone network, you keep living your life.
