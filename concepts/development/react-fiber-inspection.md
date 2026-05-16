# React Fiber Inspection

## What it is
A debugging technique where you access React's internal memory directly through a DOM element to see exactly what data a component is working with — its props, state, and the values it used to render. Accessible via the `__reactFiber` property on any DOM node.

## Plain English
React keeps a hidden copy of all the data powering every element on screen. When the UI looks wrong and you can't tell if the problem is the data or the rendering, you can reach into that hidden copy and read the actual values the component received. It tells you the truth, not what the screen shows.

## Tourism Analogy
**"Like checking the hotel's actual reservation system when the front desk display looks wrong."**

The display board at the front desk says Room 412 is vacant. But a guest is standing there insisting they have a booking. You don't argue with the display — you check the actual reservation database. If the database says booked, the display has a rendering bug. If the database says vacant too, the problem is upstream in the booking system. React Fiber is the reservation database.

## How to use it (in browser console or preview_eval)
```javascript
// Find the DOM element you care about
const el = document.querySelector('section.bg-white');

// Get the React fiber key
const fiberKey = Object.keys(el).find(k => k.startsWith('__reactFiber'));
let fiber = el[fiberKey];

// Walk up the fiber tree until you find the component with the props you need
while (fiber) {
  if (fiber.memoizedProps?.criteria?.key === 'underwriting') {
    console.log(fiber.memoizedProps.criteria);
    break;
  }
  fiber = fiber.return;
}
```

## When to use it
- Badge/indicator not rendering despite correct API data
- Component appears to have stale data after a state update
- Debugging "the screen shows X but the API returns Y" problems
- Confirming a prop actually reached the component that should display it

## Learned from
May 14, 2026 — AirROI badge wasn't rendering. API confirmed grounding_facts was correct. Fiber inspection revealed the component had the right data — the real problem was the edit went to the wrong file path (main repo vs worktree).
