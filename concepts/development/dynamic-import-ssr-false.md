# Dynamic Import with ssr:false

## What it is
A Next.js pattern that tells the framework "load this component only in the browser, never on the server." Used when the component depends on things that only exist in the browser — like `window`, `document`, or libraries that touch the DOM during import.

## Tourism translation
A tour guide who only works on-site. You can't start the tour on a phone call — everyone has to be physically in the building first. If HQ tries to run the tour remotely (server-side rendering), nothing happens.

Compare to a brochure (static HTML) which you can print from HQ and mail out before guests arrive.

## When you'd see it
- Map libraries (Leaflet, Mapbox GL) — they reference `window` at import time
- Rich text editors (Tiptap, Quill) — depend on DOM APIs
- Canvas drawing libraries
- Anything that uses `document.querySelector` or `navigator.*` at module-load time

## Why it matters
Next.js by default renders pages on the server first (for SEO + faster first paint), then "hydrates" on the client. If your component imports a library that calls `window.something` during import, the server build crashes because `window` doesn't exist in Node.js.

`ssr:false` says: "skip the server render for this component; wait until the browser is ready."

## The pattern
```jsx
import dynamic from "next/dynamic";

// Instead of: import MarinaMap from "./MarinaMap";
const MarinaMap = dynamic(() => import("./MarinaMap"), {
  ssr: false,
  loading: () => <div>Loading map…</div>,
});

export default function Page() {
  return <MarinaMap />;
}
```

The `loading:` fallback shows on the server render (and during the brief client-side load), then swaps to the real component once it's fetched.

## Trade-offs
- **Plus:** Works with browser-only libraries. No server crashes.
- **Minus:** Loses SSR for that part of the page — slightly slower first paint, worse SEO for that content.
- **Plus:** The component's code is code-split into its own bundle — only downloaded when the page actually needs it.

## Gotchas
- The dynamic import **must be at the top level of the module**, not inside a function. Next.js needs to see it statically to code-split properly.
- `ssr:false` components can't be `use server` actions. They're pure client.
- If your component sometimes needs server rendering and sometimes doesn't, split it into two components.

## Learned from
FLOHOM Marina Placement Dashboard (Apr 20, 2026). Leaflet's `L.divIcon` calls `document.createElement` during module evaluation, crashing the server build. Wrapping `MarinaMap` in `dynamic(() => import("./MarinaMap"), { ssr: false })` let the rest of the page render normally while the map lazy-loads in the browser. The server-rendered Pipeline and Groups views are unaffected — only the Map view has the ssr:false wrapper.
