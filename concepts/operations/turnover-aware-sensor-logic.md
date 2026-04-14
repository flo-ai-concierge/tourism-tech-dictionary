# Turnover-Aware Sensor Logic

## What it is
Using check-in and check-out times from the reservation system to determine whether a sensor event (like a noise sensor being removed) is caused by the cleaning team or a guest. If the event happens before check-in time on check-in day → 100% cleaners. After check-out time on check-out day → 100% cleaners. Between guests (no active reservation) → 100% cleaners. During an active stay in the evening → flag for review.

## Tourism Translation
**Like a hotel security system that knows the housekeeping schedule.** If a room's door sensor trips at 1 PM and check-in isn't until 3 PM, security knows it's housekeeping — no alarm needed. If the same sensor trips at 11 PM during a guest's stay, that's worth investigating. Without the schedule context, every sensor event looks the same and generates false alerts.

## Precision signals
- `isBeforeCheckIn` — event time < check-in time on check-in day → cleaning team, 100% certainty
- `isAfterCheckOut` — event time > check-out time on check-out day → guest already left, cleaners
- `isTurnoverWindow` — no active guest, previous checked out → between-guest maintenance
- `isDaytime` (9 AM–6 PM) + active guest → probably accidental, low concern
- `isEvening` (after 6 PM) + active guest → potentially concerning, flag it

## Why it matters
- Without timing context, an AI generates vague assessments ("likely accidental")
- With precise check-in/check-out times, the AI can say definitively "this happened before the guest arrived — it's the cleaning team"
- Reduces false alerts and @channel notifications that desensitize the team

## Related concepts
- Turnover — check-out + check-in same day
- Duration tracking (paired events) — measuring time between alert and resolution
- Property cluster map — nearby properties that share context
