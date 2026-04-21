# Radar Chart (Spider / Web Chart)

## What it is
A chart where multiple attributes are plotted as points on axes radiating out from a center, then connected into a shape. The further out on each axis, the higher the score. At a glance, you see which attributes are strong and which are weak — and the *shape* of the overall profile.

## Tourism translation
A guest-experience report card. Imagine rating a hotel on cleanliness, comfort, location, amenities, F&B, and staff. A single star rating ("4 out of 5") compresses all that into one number. A radar chart plots all six axes at once — you see that this hotel is 5/5 on cleanliness and location but only 3/5 on F&B. The shape tells the story: a balanced property makes a big even circle; a weak-on-amenities hotel has a visible dent on that axis.

## When you'd see it
- Comparing properties or marinas across many criteria
- Performance reviews with multiple competency areas
- Product feature-set comparisons
- Anything with 3-12 attributes you want to see at once

## Why it matters
Some things can't be compressed into a single number without losing the interesting parts. A 290/360 score on FLOscore is useful, but it doesn't tell you *why* it's 290. A radar chart shows you: "Great on city tier, tourism, F&B scene — weak on houseboat regs and liveaboard proximity."

Humans read shapes faster than tables. A dented radar instantly tells the viewer "there's a weakness here" without them reading any numbers.

## When NOT to use a radar chart
- Fewer than 3 attributes (use a bar chart — radar needs a polygon)
- More than ~12 attributes (too crowded to read)
- Attributes with very different scales (normalize to 0-100 first)
- Comparing many items (more than 3 overlapping radars is unreadable)

## The pattern
```jsx
<RadarChart data={[
  { attribute: "City Tier", score: 67, max: 30 },
  { attribute: "Tourism", score: 100, max: 15 },
  { attribute: "F&B Scene", score: 67, max: 15 },
  ...
]}>
  <PolarGrid />
  <PolarAngleAxis dataKey="attribute" />
  <PolarRadiusAxis domain={[0, 100]} />
  <Radar dataKey="score" fill="#5B7D7F" fillOpacity={0.35} />
</RadarChart>
```

Key design choices:
- **Normalize scores to the same scale** (0-100) so the shape is readable when attribute max-points differ
- **Show the raw value in a tooltip** so the detail is still accessible
- **Pair the radar with a table** — the radar for the shape, the table for the numbers

## Gotchas
- If one attribute has max=30 and another has max=15, raw plotting makes the larger-max attributes always dominate the shape. Normalize before plotting.
- Radar charts don't handle negative values well — use 0 as the minimum.
- Browser warnings about "chart width -1" usually mean the container hasn't settled yet — give it explicit dimensions or wait for layout.

## Learned from
FLOHOM FLOscore radar (Apr 20, 2026). Brian's 18-attribute marina rubric scored marinas on city tier (30 pts), seasonality (30), houseboat regs (30), through to liveaboard proximity (15). Raw plotting made the 30-pt attributes look dominant. Normalizing to percent-of-max produced a readable shape that Brian can glance at and immediately see a marina's profile — "Liberty Landing is strong everywhere except tourism and slip view." Paired with a two-column table showing raw scores below the radar.
