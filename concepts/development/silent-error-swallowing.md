# Silent Error Swallowing

## Tech Concept
A `catch {}` block that catches errors but does nothing with them — no log, no user message, no retry. Failures disappear silently. The user takes an action, nothing happens, and they have no idea why.

## Plain English
Something breaks in the background and the code just ignores it. No error message, no warning, no feedback. The user is left confused wondering if their action worked or not.

## Tourism Analogy
Like a concierge who receives a failed booking request, says nothing to the guest, and just nods politely. The guest has no idea their reservation didn't go through — until they arrive and there's no room waiting for them.

## Why It Matters
Silent errors are the hardest bugs to debug because there's no evidence they happened. They also destroy user trust — the UI looks like it worked, but nothing actually changed.

## Example (FLOTurn Cleaners — May 2026)
The "Create & Send Portal Link" form had `catch { /* ignore */ }` in the POST handler. When `createCleaner()` threw a DB error, the response body was empty. The client called `.json()` on an empty response, producing "Unexpected end of JSON input." Fixed by wrapping in try/catch and always returning a JSON error object.

## The Fix
```js
// Bad — swallows everything silently
try { await doSomething(); } catch { }

// Good — surface errors to the user
try {
  await doSomething();
} catch (err) {
  console.error(err);
  showErrorMessage(err.message || "Something went wrong");
}
```

## Related Concepts
- Optimistic UI Update
- Error Boundaries
