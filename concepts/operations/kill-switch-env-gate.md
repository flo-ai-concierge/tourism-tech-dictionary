# Kill Switch (Environment Variable Gate)

## What it is
A setting that must be explicitly turned ON before a feature runs in production. The code is deployed and ready, but it does nothing until an administrator flips the switch. Implemented as an environment variable check — if `FEATURE_ENABLED=true` isn't set, the feature returns immediately without executing.

## Tourism Translation
**"The 'Vacancy' sign you flip manually at the front desk."**

The rooms are cleaned, beds are made, minibar is stocked — everything is ready. But the hotel isn't accepting guests until the manager walks to the front desk and flips the sign from "No Vacancy" to "Vacancy." The infrastructure is complete, but the decision to go live is a deliberate human action.

Kill switches work the same way. The auto-nudge system is deployed, tested, and waiting. But it sends zero emails until the operator adds `AUTO_NUDGE_ENABLED=true` to the server configuration. One line change, instant activation. Another line change, instant shutdown.

## Why it matters

### Safety for guest-facing features
Deploying code and activating it are two separate decisions. You want the code live so it's tested in production, but you don't want it acting on guests until you've reviewed how it works. Kill switches create that gap.

### Instant rollback
If something goes wrong, you don't need to redeploy code or revert commits. Just remove the environment variable — the feature stops immediately on the next cycle.

### Staged rollout
You can activate features one at a time, monitor each, then move to the next. Much safer than flipping everything on at once.
