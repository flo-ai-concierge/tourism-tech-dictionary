# Optimistic UI Update

## Tech Concept
Updating the UI immediately when a user takes an action — before waiting for the server to confirm it worked. If the server responds with an error, the change is rolled back.

## Plain English
You flip a switch and the light turns on right away. The system is confirming in the background. If something went wrong, the light turns back off and you get an error message. The user never sits there watching a spinner for something that should feel instant.

## Tourism Analogy
Like when a hotel front desk immediately hands you a room key the moment you say you're checking in — they trust it'll work out. If the key card machine fails, they take the key back and troubleshoot. No awkward standing there waiting.

## Why It Matters
Without optimistic updates, controlled inputs (like dropdowns) snap back to their old value during the API call — making it look like the save didn't work even when it's just slow. Optimistic updates make the UI feel fast and responsive.

## Example (FLOTurn Properties Tab — May 2026)
When a cleaner selects a new market from the dropdown, the property immediately moves to that market group — before the PATCH API responds. If the API fails, the property snaps back and an error banner appears.

## Pattern
```js
const prev = state;
setState(optimisticValue);   // update immediately
try {
  await api.save(value);
} catch {
  setState(prev);            // revert on failure
  showError();
}
```

## Related Concepts
- Controlled Component Snap-Back
- Silent Error Swallowing
