# Round-Robin Interleave

## What it is
A pattern for processing items from multiple categories where you rotate through one from each category per pass, instead of finishing all of one category before starting the next. Used when you want visual variety, fairness, or balanced throughput.

## Tourism Translation
**"Serving appetizers to Table 1, Table 2, Table 3, Table 4, then going back to Table 1 for mains."**

You don't finish every course for Table 1 before touching Table 2. You serve one round of appetizers across all tables, then one round of entrees, then dessert. Every table progresses at the same rate. Nobody stares at an empty placemat while their neighbors are eating dessert.

## Why it matters

### When you have uneven data
Our prod DB had 524 Google reviews but only 75 Hostaway reviews at one point. If we posted them to Slack in pure chronological order, the first ~500 posts would all be green (Google) before any other color appeared. The team would scroll and see a wall of green and think "is anything besides Google working?"

Round-robin interleave fixed that: post 1 Airbnb → 1 VRBO → 1 Google → 1 Direct → repeat. Every scroll showed all 4 platforms mixing, even though Google dominated the backlog.

### The trade-off
Round-robin breaks strict chronological order. A June 2023 Google review might appear next to a December 2024 Airbnb review because each bucket was sorted separately. For our review feed, visual variety was more important than strict ordering. For a finance audit log, the opposite would be true — use pure chronological there.

### Real FLOHOM example
```js
const buckets = new Map();
for (const row of rows) {
  const key = row.platform || "other";
  if (!buckets.has(key)) buckets.set(key, []);
  buckets.get(key).push(row);
}

const platformOrder = ["airbnb", "vrbo", "google", "booking", "direct"];
const result = [];
while (result.length < limit) {
  let anyLeft = false;
  for (const platform of platformOrder) {
    const bucket = buckets.get(platform);
    if (bucket && bucket.length > 0) {
      result.push(bucket.shift());
      anyLeft = true;
    }
  }
  if (!anyLeft) break;
}
```
One pull from each bucket per round, until buckets run dry.

## In simpler terms
Dealing cards around a poker table, one at a time. Nobody waits until the dealer has finished giving all five cards to the first player — everyone gets their first card, then their second, then their third. Fair, fast, visually obvious.
