# z-index & Stacking Context

## What it is
A CSS system that controls which element appears on top when two elements overlap. `z-index` is a number — higher means closer to the viewer. But it only works *within a stacking context*, which is a scope created by parent elements with certain CSS properties. A drawer with `z-index: 50` can still be covered by a map whose internal pieces have `z-index: 700` if the drawer isn't in a high-enough stacking context.

## Tourism translation
Hotel floor layout. The lobby is ground floor, meeting rooms are 2nd, penthouse is top. When a marketing photo overlays them, the penthouse covers the lobby — because it's on a higher floor.

But: if the penthouse is in a different *building* (a separate stacking context), its 12th-floor rank doesn't help — the other building's 3rd floor still shows in front if that building as a whole is positioned closer to the camera.

## When you'd see it
- Modals, drawers, tooltips that need to appear above everything else
- Dropdown menus clipped by parent elements
- Sticky headers that disappear behind map tiles
- Overlays that work in one place but not another — same z-index, different parent

## Why it matters
Every UI with layers deals with this. Map libraries like Leaflet have their own internal stacking (tiles at z-200, overlays at z-400, popups at z-700, tooltips at z-650) — if your drawer naively uses `z-50`, the map's popup can appear *above* your "on top" drawer.

Understanding stacking contexts tells you whether bumping the z-index to 9999 will actually work, or whether you need to restructure the DOM.

## What creates a new stacking context
Any of these on an element creates a new stacking context for its children:
- `position: fixed` or `sticky`
- `position: relative` + a `z-index` value (not `auto`)
- `opacity < 1`
- `transform`, `filter`, `backdrop-filter`
- `isolation: isolate`

Within that context, children's z-indexes compete with each other — not with siblings of the parent.

## The mental model
Think of stacking contexts as nested building floors:
1. The page's root is "building 1"
2. A `position: fixed` element creates "building 2" at its floor position
3. Inside building 2, children stack by their own z-index
4. But building 2 as a whole sits at its own z-index within building 1

If you want a drawer above the map, **the drawer's stacking context must outrank the map's stacking context** — not just beat an individual map layer.

## Debugging technique
Chrome DevTools → 3-dot menu → "More tools" → "Rendering" → "Layer borders" shows you the actual stacking layers. Or inspect each parent up the tree looking for `position:`, `transform:`, or `z-index:` properties.

## Gotchas
- `z-index: 9999` doesn't matter if the element isn't `position: relative/absolute/fixed/sticky`. No position → no stacking.
- A parent with `transform: translate(0)` creates a stacking context that **traps** children inside — even z-index: 99999 can't escape.
- Tailwind classes like `z-50` map to `z-index: 50` — but only take effect when paired with `position: fixed/absolute/relative`.

## Learned from
FLOHOM Marina Placement Dashboard (Apr 21, 2026). User clicked a pin on the map; the drawer opened on the right — but the Leaflet tile tooltip (z-700 internal) appeared *on top* of the drawer (z-50). Fix: bump drawer to `z-index: 1001` and backdrop to `z-index: 1000`. Tailwind's standard `z-50` class wasn't enough because Leaflet's panes defined their own stacking values higher than our Tailwind default. Direct inline style with a large number (`zIndex: 1001`) was simpler than fighting the class system.
