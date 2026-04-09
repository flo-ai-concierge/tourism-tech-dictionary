# Status Badge

## What it is
A small, colored label on a record showing its current state at a glance: "Pending," "In Progress," "Done," "Needs Attention." Users scan the badges to know what's up without reading every record.

## Tourism Translation
**"The colored magnets on a housekeeping whiteboard."**

The housekeeping board has every room listed with a colored magnet next to it:
- 🟢 Green = ready for guest
- 🟡 Yellow = cleaning in progress
- 🔴 Red = maintenance issue
- 🚩 Flag = VIP or complaint on file

A supervisor walks up and knows the whole property state in 3 seconds. No reading, no digging, just visual pattern recognition.

## Why it matters

### Scannable > readable
If every review card on the Reputation page requires reading two sentences to know "have we replied to this yet?", the team moves slowly. With a colored badge at the top right corner, the eye jumps straight to reds and yellows. Greens get ignored because they're handled.

### FLOHOM's review badges
Every review card now shows one of these badges:
- ✓ **Responded** (green) — we've already replied, either captured from Hostaway's `revieweeResponse` or via manual "Mark as Sent"
- ⚠ **Needs response** (red) — low rating (≤4★) AND no response yet, urgent
- ◷ **Awaiting** (blue) — pending but not urgent
- 🚩 **Flagged** (amber) — manually flagged, separate from response state
- 😟 **Negative / 😐 Neutral** (only shown when sentiment isn't positive)

Each badge has its own bg color, border color, icon, and text color, pulled from a single lookup table.

### The derivation is computed, not stored
The badge isn't stored in the database. It's derived at render time from `responded_at`, `source_response_text`, `review_rating`, and `is_flagged`. That means when the underlying state changes (new response synced from Hostaway, new flag set), the badge updates automatically on the next page load without needing a data migration.

### Why this beats a filter dropdown
A filter dropdown forces the user to choose one view. Badges let them see everything at once and spot the urgent items without filtering. Both are useful — badges for quick scanning, filters for focused work.

## In simpler terms
Traffic lights. You don't read each intersection's rules, you just see green/yellow/red and react. That's what a status badge does for a data table.
