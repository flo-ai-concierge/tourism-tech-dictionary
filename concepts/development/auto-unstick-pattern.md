# Auto-Unstick Pattern

## What it is
A self-healing mechanism that detects when a background process (like a sync engine) has been stuck in "running" status for too long and automatically resets it to "idle" so it can run again. Without this, a crashed sync stays permanently locked — no new data gets imported, and clicking "sync" does nothing because the system thinks a sync is already in progress.

## Tourism Translation
**Like a hotel elevator that auto-resets after being stuck between floors for 10 minutes.** Without the auto-reset, a stuck elevator stays stuck until a technician manually resets it — which could be hours. With the auto-reset, the elevator returns to the ground floor on its own, logs the incident, and resumes normal service. Guests might wait 10 minutes, but not 10 hours.

## Pattern
```
Before each sync run:
1. Check: is status = 'running' AND updated_at < NOW() - 10 minutes?
2. If yes → force reset to 'idle' (log a warning)
3. Proceed with normal sync
```

## Why simple timeouts aren't enough
- The process might update `updated_at` on every loop iteration — preventing the timeout from ever triggering
- A crashed process never updates anything — but if another process keeps refreshing the timestamp, the auto-unstick threshold is never reached
- Solution: use a separate `started_at` timestamp that only gets set once at the beginning of the run

## Related concepts
- Sync state lock — the lock mechanism that gets stuck
- Kill switch (env gate) — manual override to disable features
- Self-healing migration — auto-fixing database issues on startup
