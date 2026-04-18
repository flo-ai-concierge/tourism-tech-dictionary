# UTC Midnight Timezone Bug

## What it is
A subtle bug that hits when you store a "calendar date" (like a check-in date) in a database, then read it into JavaScript and convert it to a local timezone. Most database drivers represent a date-only column as "midnight UTC of that date." When you ask "what date is this in Eastern Time?", the answer is the day BEFORE — because midnight UTC is 8 PM the previous day in Eastern Time.

## Tourism translation
**A reservation says "Check-in: April 18."**

Your phone is set to Manila time (UTC+8). Your phone shows "April 18 at 12:00 AM."

Your housekeeper's phone in Maryland (UTC-4) shows "April 17 at 8:00 PM."

Same reservation, same exact moment in time, two different displayed days. Now imagine your code asks "is this reservation today?" — the answer depends on which timezone you ask in, and you get the wrong day half the time.

## Why it happens
- A Postgres `date` column has no time component (just "April 18").
- The Postgres driver converts this to a JavaScript `Date` object.
- JavaScript's `Date` is always a moment in time — there's no "date-only" type.
- The driver picks midnight UTC: `2026-04-18 00:00:00 UTC`.
- When you call `.toLocaleDateString("en-US", { timeZone: "America/New_York" })`, you get back "4/17/2026" because that moment in ET is the day before.

## When you'd see it
- Comparing a guest's check-in DATE to today's DATE in a specific timezone.
- Computing "is this alert on the guest's checkout day?"
- Generating reports grouped by calendar day.
- Anything where the database value is conceptually a calendar day, not a moment.

## The fix
Don't convert calendar dates through `new Date().toLocaleDateString()`. Instead, pull the UTC components directly:

```js
function pgDateString(d) {
  if (!d) return null;
  const dt = new Date(d);
  const y = dt.getUTCFullYear();
  const m = String(dt.getUTCMonth() + 1).padStart(2, "0");
  const day = String(dt.getUTCDate()).padStart(2, "0");
  return `${y}-${m}-${day}`;
}
```

This treats the value as what it actually is — a calendar day — without timezone-shifting it.

## Why it matters
We hit this in the FLOHOM Minut scanner. An alert at 10:39 PM ET on Apr 17 (during a guest's stay) was being attributed to "cleaners on site during turnover." The bug: my code thought the guest's checkout date was Apr 17 (it was actually Apr 18). For any alert past noon on what my code thought was checkout day, the cleaner-window logic flagged it. The AI was correctly relaying my flag — the flag itself was wrong.

## Learned from
FLOHOM Minut scanner (Apr 18, 2026). Cost three deploy cycles and a frustrated user before I traced it to the date conversion. Now the project's standard pattern for any "is this date X" check.

## Related concepts
- Postgres data types (date vs timestamp vs timestamptz)
- [`ai/llm-hallucination-vs-upstream-bug`](../ai/llm-hallucination-vs-upstream-bug.md) — when the AI "lies," check what you fed it first
