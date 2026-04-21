# Cross-System Bridge

## What it is
A pattern where two separate features or systems link to each other through a shared identifier (like a city name, a guest email, or a reservation ID). Clicking a thing in System A jumps you to the matching thing in System B, and vice versa. The systems stay logically separate — they don't merge — they just know how to find each other.

## Tourism translation
A connecting door between the concierge desk and the booking office. Both departments have their own processes, files, and staff. But when the concierge pulls up a guest's name, one click opens the booking office's file for that same guest — and vice versa. Same guest, same key, two specialized views.

Compare to merging the departments (a monolith) or making everyone walk around the building every time (no bridge).

## When you'd see it
- Dashboards that reference each other (Marinas ↔ Market Reports, Guests ↔ Reservations ↔ Conversations)
- CRM integrations (GHL contact ↔ our guest profile)
- Related-content strips ("Other reservations for this guest", "Marinas in this city")
- Any "View [related thing]" button that jumps to a different section

## Why it matters
It lets each feature stay small and focused while still giving users the "connected" experience they need to do their job. Keeps the architecture simple: each system owns its data, the bridge is just a join-by-identifier.

## The bridge mechanics
Two pieces:
1. **An identifier both systems can agree on** — usually a natural key like a city name, an email, or a hostaway_id.
2. **A lookup from one side to the other** — an API endpoint that takes the identifier and returns matches.

```js
// From Marinas → Navigator: "Show me the market report for this marina's city"
GET /api/admin/market-reports?city=Miami,FL

// From Navigator → Marinas: "Show me marinas we're tracking in this report's city"
GET /api/admin/marinas/by-city/Miami,FL
```

The UI renders a small "bridge widget" on each side: a card with the matched content and a link to jump over.

## Designing good bridges
- **Always two-way.** If Navigator can link to Marinas, Marinas must link to Navigator. Otherwise users get stuck.
- **Fuzzy match on the identifier.** "Miami, FL" and "Miami" and "miami fl" should all find the same report. Use `ILIKE`, `LOWER()`, or normalize on write.
- **Fail gracefully.** If there's no match on the other side, show a helpful next step ("Generate a market report for this city →") instead of an error or empty state.
- **Don't duplicate data across the bridge.** Pull live from the source; don't copy. Otherwise the two sides drift.

## Gotchas
- Fuzzy matching can give false positives. "Portland" could mean OR or ME. Always include state when possible.
- If the identifier changes on one side (marina gets renamed), the bridge breaks. Prefer stable IDs over labels when you can.
- Bridges are a symptom of good domain separation, but if you find yourself building dozens of bridges between the same two systems, reconsider whether they should be one system.

## Learned from
FLOHOM Navigator ↔ Marinas bridge (Apr 20, 2026). Rock 1 (Market Navigator) and Rock 2 (Marina Placement Dashboard) were originally scoped as separate features. On the data review, we realized Brian's workflow always crosses between them — he's evaluating a marina AND needing market research for its city. Built the bridge by joining on `marina.city ≈ market_reports.city`. Marinas get a "Market Report" tab; market reports get a "Marinas we're tracking" strip. Same info surfaces from both directions. The Regulatory tab goes further — it *auto-pulls* regulatory data from the market report, so the two systems don't just link, they enrich each other.
