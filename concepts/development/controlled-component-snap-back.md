# Controlled Component Snap-Back

## Tech Concept
In React, a "controlled" input is one whose displayed value is always driven by code (state), not the browser's native input state. During an async operation, the state hasn't updated yet — so the input visually reverts to its old value while waiting for the server. This looks like the save didn't work, even if the save succeeds.

## Plain English
You change a dropdown to "Myrtle Beach." The page is waiting for the server to confirm. While it waits, the dropdown snaps back to "Baltimore / AAC" because that's still what the code says it should show. When the server responds, it updates to "Myrtle Beach." Users think their change was ignored.

## Tourism Analogy
Like a self-resetting thermostat that always shows the original temperature while it's processing your new setting. Guests think their adjustment was ignored, even though the system is working on it behind the scenes.

## Why It Matters
Users interpret the snap-back as a failure. They retry, submit twice, or give up thinking the feature is broken. The fix is an optimistic UI update — update state immediately before the API call.

## Example (FLOTurn Properties Tab — May 2026)
Market dropdown for FLOHOM 16 and 17 appeared to "not stick" — the dropdown was controlled by `prop.market` which didn't update until after the API responded. Fixed by applying the optimistic update pattern.

## Related Concepts
- Optimistic UI Update
- React State
