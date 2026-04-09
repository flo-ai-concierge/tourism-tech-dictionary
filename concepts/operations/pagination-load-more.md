# Pagination / Load More

## What it is
Loading a long list of records in chunks (e.g., 50 at a time) instead of dumping all of them at once. The user sees the first chunk immediately, then clicks "Load More" or scrolls to fetch the next chunk.

## Tourism Translation
**"Handing the guest the first 20 activity cards, then letting them flip for more."**

Your concierge desk has 500 local activity recommendations. You don't hand the guest all 500 when they walk in — they'd run screaming. You hand them the top 20 (best-rated, most popular), and keep the rest in a drawer. If they want more, they ask, and you pull the next 20.

## Why it matters

### Page load speed
Loading 1,024 reviews at once means fetching 1,024 database rows, serializing 1,024 JSON objects, rendering 1,024 cards in the DOM, and transferring megabytes of data over the wire. Most users only look at the first 20-50 anyway. Pagination means the initial page loads in under a second.

### Scroll sanity
Even if the data were free to load, rendering 1,024 cards at once would make the scroll jittery and the browser sluggish. Pagination keeps the DOM small and fast.

### The "Load More" pattern
Instead of numbered pages (1, 2, 3...), modern UIs use a single "Load More" button at the bottom of the list. Click it → append the next 50 to what's already showing → scroll continues naturally. Simpler mental model, better on mobile.

### Real FLOHOM example
Our Reputation page was showing the default 50 reviews. Anything older required filter tricks. Now the page says "Showing 50 of 1,024 — newest first" and has a "Load 50 more" button. Click it once → 100 loaded. Click again → 150. Keep clicking until "End of list — all 1,024 mentions loaded."

### API-side implementation
The API accepts `?limit=50&offset=50` query params. First page = `limit=50&offset=0`. Second page = `limit=50&offset=50`. Third = `limit=50&offset=100`. The API also returns `totalCount` so the UI knows when to stop showing the button.

### Resets on filter change
When the user changes a filter (platform, sentiment, etc.), the list resets to page 1. Otherwise the user would see a confusing mix of "filtered + old unfiltered" results.

## In simpler terms
It's a deck of cards you flip through, not a wall of 1,024 cards nailed down all at once. Pull them out a handful at a time, when you need them.
