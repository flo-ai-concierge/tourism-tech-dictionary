# Response Status Tracking

## What it is
Knowing, at a glance, whether a message or review has already been replied to. Eliminates double-responses and makes "still needs a response" a filterable, sortable state instead of a mental load.

## Tourism Translation
**"The guest-comment card tray at the front desk."**

There are two trays: "Replied" and "Needs Response." Every morning, the front desk manager walks up, sees the Needs Response tray, answers those, and moves them to Replied. No card gets answered twice. No card gets forgotten. Anyone walking up knows exactly what's pending without reading every card.

## Why it matters

### Reviews have a natural response cycle
Every guest review has two states: unaddressed, or addressed. Without tracking the state, you rely on memory or scrolling to figure out which reviews you've already replied to. That breaks down at scale.

### Hostaway already knows
Every review object from Hostaway's API has a `revieweeResponse` field. If it's populated, we've already posted a public reply on that platform. If it's empty, we haven't. This is free intelligence — we just weren't capturing it before.

### Now we do
Our review sync now pulls `revieweeResponse` and `revieweeResponseStatus` on every tick. If the field is non-empty, we update `source_response_text` and `source_response_at` on our local mention row, and set `responded_at` (which feeds the UI banners).

### The detail page banner states
Every review detail page shows one of three banners at the top:
- ✓ **Already responded on {Platform} on {Date}** (green) — we've replied, nothing to do
- ⚠ **Awaiting response — FLO intervention needed** (red) — low rating, no response yet, urgent
- ◷ **Awaiting response** (blue) — pending but not urgent

Below the banner, when we've already responded, the actual response text is shown inline so the team can see what was said.

### The FLO card adapts
When a review is already responded to, the FLO Suggested Reply card still works but shows a warning: "This review was already responded to. Generating a new draft would be a second reply." So regenerating is possible (in case you want to update your response) but never accidental.

### Google reviews use manual Mark-as-Sent
GHL's Reputation API is behind a scope our token doesn't have, so we can't auto-pull Google response state. Instead, the team clicks "Mark as Sent" in FLO Bridge after replying on Google directly, which populates `responded_at` and flips the badge to green.

## In simpler terms
A "done" checkbox next to every item on your to-do list. Without it, you waste time figuring out what's left. With it, your eye jumps straight to what still needs your attention.
