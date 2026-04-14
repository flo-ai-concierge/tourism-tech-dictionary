# Duration Tracking (Paired Events)

## What it is
Tracking the elapsed time between a start event and its matching resolution event. For example, a "noisy for 10 minutes" alert fires at 11:00 PM, and "it's quiet" fires at 11:47 PM — the system calculates and reports "noise lasted 47 minutes." Uses an in-memory map keyed by property + event category.

## Tourism Translation
**"A hotel incident log that records when a disruption started and when it ended."**

When a guest complains about construction noise at 2:00 PM and the noise stops at 3:30 PM, the manager's log entry reads: "Noise disruption — 1 hour 30 minutes. Resolved." This duration helps assess severity — a 10-minute blip is different from a 3-hour party.

## Why it matters
Minut sensors send separate emails for each escalation level (10 min, 20 min, 30 min) and a separate "quiet" email when noise stops. Without duration tracking, the resolution message just says "it's quiet" — but the team doesn't know if noise lasted 11 minutes or 3 hours. With tracking, FLO can assess: "Noise lasted 2 hours 15 minutes — review VicoPhone footage and consider a guest policy reminder."

## In simpler terms
It's a stopwatch that starts when a problem begins and stops when it's resolved, so everyone knows how long the disruption actually lasted.
