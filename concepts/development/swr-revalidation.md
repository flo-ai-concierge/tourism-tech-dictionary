# SWR Revalidation

## What it is
A behavior in the SWR data-fetching library that automatically re-checks the server for fresh data — on a timer, when you return to the tab, or when the window regains focus. Keeps the UI in sync with the backend without you writing the polling logic yourself.

## Tourism translation
Housekeeping doing silent room checks every 30 minutes. You don't have to call down to the front desk to ask "is the mini-bar refilled yet?" — the check happens on a schedule and the information updates in the background. If you were looking at a slightly stale status ("mini-bar low"), it quietly updates to ("mini-bar refilled") the next time the check runs.

## When you'd see it
- Dashboards where numbers change over time (revenue, inbox counts, sync status)
- Admin panels that multiple people might edit simultaneously
- Any page you want fresh without forcing the user to hit refresh

## Why it matters
Without revalidation, a user who opens a tab and leaves it for an hour sees an hour-old snapshot of the data. With revalidation: they come back, the data's already fresh. **You'd never know you had stale data** unless you compared two tabs — which is the whole problem.

## The three levers
```js
const { data } = useSWR("/api/stats", fetcher, {
  refreshInterval: 30000,       // re-fetch every 30 seconds in background
  revalidateOnFocus: true,      // re-fetch when user returns to this tab
  dedupingInterval: 5000,       // don't re-fetch if called within 5s
});
```

- **refreshInterval** — time-based polling. Good for dashboards.
- **revalidateOnFocus** — event-based. Good for data another admin might have edited.
- **dedupingInterval** — the safety rail. Prevents multiple components making the same call from stampeding the server.

## Trade-offs
- **Plus:** UI always feels fresh. Zero user effort.
- **Minus:** More server load. Every open tab is polling.
- **Plus:** Still cheap if you set `dedupingInterval` — duplicate calls within the window merge into one request.
- **Minus:** Can mask bugs. If your initial fetch returned bad data, revalidation might silently fix it — or not — making intermittent issues harder to reproduce.

## Gotchas
- **`revalidateOnFocus: false` is the SWR default after some versions.** You have to opt in to get fresh-on-return.
- If you set a short `refreshInterval` (like 5s), your server logs will flood with requests. Start at 30s and tune down only if needed.
- Deploy gotcha: if a user opens a tab *before* a feature deploys and *stale SWR cache survives the deploy*, they'll see stale data until they hard-refresh. Safer default: `revalidateOnFocus: true` + `refreshInterval: 30000`.

## Learned from
FLOHOM Marina Placement Dashboard (Apr 21, 2026). A user opened `/admin/marinas` right after deploy but before the DB import finished. SWR cached the empty response and never re-fetched — showing "0 marinas" for hours until a hard refresh. Fix: enable `revalidateOnFocus: true` + `refreshInterval: 30000` so the page self-heals if the tab is left open across data updates.
