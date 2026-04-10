# React State Mutation

## What it is
Changing data directly in a way that React can't detect, so the screen doesn't update even though the underlying data changed. React compares the old object reference to the new one — if they're the same reference, React assumes nothing changed and skips re-rendering.

## Tourism Translation
**"Updating a guest's room assignment in your notebook but forgetting to tell the front desk."**

You crossed out "Room 204" and wrote "Room 307" in your personal log. But the front desk still has the old card showing Room 204 — they keep sending people to the wrong room. The fix: write a brand new assignment card and hand it to the front desk directly.

## Why it matters
In the FLOHOM pipeline, FLO Analyze completed and saved the recommendation data, but the card on screen never showed the result. The code was modifying the existing data object directly (mutation) instead of creating a new one. React saw the same object reference and skipped the update — so the analysis was done but invisible. Fixed by creating a fresh copy of the data with the changes applied.
