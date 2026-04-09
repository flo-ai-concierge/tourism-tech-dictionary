# chat.update / Edit-in-Place

## What it is
Slack's API method for editing an existing message in place, instead of deleting it and posting a new one. The message keeps its position in the channel timeline, its reactions, its thread replies — only the content changes.

## Tourism Translation
**"Updating the lobby whiteboard when the pool closes early."**

The lobby whiteboard currently says "Pool open until 10 PM." A storm rolls in, and you need it to say "Pool closed at 8 PM due to weather." You don't erase the whole board and rewrite everything else from scratch. You wipe just the pool line and rewrite it. Everyone who walks by next still sees the same board in the same place with updated info.

That's `chat.update`. Same message slot, new content.

## Why it matters

### Data changes after posting
Reviews in our system get richer over time. When a review first hits `#reviews`, we might not have the guest's name yet (it was "Anonymous guest"). An hour later, someone manually fills in the name via the admin API. Without edit-in-place, we'd either post a duplicate with the new info (spammy) or leave the old card stale forever (confusing).

With `chat.update`, we call a sync endpoint that re-renders the card with fresh data and edits it in place. The channel stays clean, the timeline stays intact, and the team sees accurate info.

### Finding the message to update
You need the `ts` (timestamp) of the original message to update it. We don't store `ts` in the DB, so our sync endpoint scans Slack channel history, reads each bot message's button URL (which contains the mention ID), and builds an in-memory map: `mentionId → ts`. Then it calls `chat.update` with the right `ts` for each mention we want to refresh.

### Real FLOHOM example
When we manually mapped 11 unmatched reviews to FLOHOM properties, we ran the sync-slack-posts endpoint with `{ mentionIds: [708, 719, 590, 682, 691, 694, 697, 698] }`. It:
1. Scanned `#reviews` history and built the mention → ts map
2. For each mention, re-rendered the full Block Kit payload with the newly-assigned property
3. Called `chat.update` with the new blocks

Result: 8 cards updated in place showing the correct property name. No duplicates, no deletions, team sees the fresh data.

### Can also delete
The same sync endpoint accepts `olderIds` for mentions removed from the DB. For those, it calls `chat.delete` instead of `chat.update` — the Slack card disappears cleanly.

## In simpler terms
It's the "Edit" button next to a message in Slack — but done programmatically by code. The message stays put; only its content changes.
