# Stale Refactor Trap (Dead Code Path)

## What it is
When a developer rewrites a large piece of software into a cleaner architecture but never finishes the migration — the old code stays in place, the new code goes unused, and any future engineer who edits the new code makes ZERO impact on production. The old code path is silently still running everything.

## Tourism Translation
**A hotel renovates a guest room but forgets to tell reservations to stop booking the OLD room.**

The renovated room is gorgeous. New paint, new bedding, premium fixtures. But the reservations team is still booking the old, dusty version of the room because nobody updated the booking system. Guests keep getting sent to the original. The renovation team thinks they're getting glowing reviews; the reservations team is fielding complaints. Both are confused.

The renovated room is "live" in the sense that it exists — but it's "dead" in the sense that nobody routes to it.

Same in code: the new modular files exist on disk, but if nothing imports them, edits to them have zero effect.

## How it bit us on Apr 22, 2026
FLO's logic was originally in a single 5,656-line file: `floAgent.js`. On Apr 15, 2026 we did a refactor — split it into clean modules under `src/flo/`:
- `src/flo/brain/` — chat, system prompt, tool router
- `src/flo/hands/` — tool definitions, tool executor, domain handlers
- `src/flo/config/` — listings, constants, team

The new modules were beautiful. Clean separation of concerns. Easy to navigate.

But the migration was never finished. `slackBot.js`, `server.js`, and `vapiSetup.js` all still imported from the old `floAgent.js`. So 100% of FLO's production behavior — Slack, voice, smart-reply, every guest conversation — was running on the old monolith.

When we needed to fix FLO's hallucination about task assignment, I edited the modular files for ~2 hours. Pushed three commits. Nothing changed in production. Eventually I grepped for `require("./floAgent")` and discovered the truth: the modular code was completely dead.

The fix took 30 minutes once I knew where to edit. The wasted hours were entirely from editing dead code.

## How to detect it
Quick checklist for any large refactor in progress:
- `grep -r "require.*<old-file>" src/` — does anything still import the old code?
- `grep -r "require.*<new-modular-path>" src/` — does anything import the new code? If no, it's dead.
- Look at the entry points (server.js, the production cron files, the bot files) — what do they actually call?

If the old file is imported and the new files aren't, the refactor is incomplete. Edit the old file until the migration finishes — or your edits are theater.

## How to prevent it
Two patterns:

1. **Strangler-fig migration**: replace one entry point at a time. After each migration, delete the old code path that's no longer reachable. Don't leave parallel implementations running.

2. **Add a startup assertion**: if both the old and new code paths are loaded, log a loud warning at server boot. Forces the team to notice the unfinished migration.

## Related concepts
- [Burn It Down Rewrite](burn-it-down-rewrite.md) — sister pattern, the alternative to incremental migration
- [Audit Script](audit-script.md) — the diagnostic tool that proves which code is actually live
- [Module Caching (Node.js)](../infrastructure/module-caching-nodejs.md) — why even live edits don't take effect without restart
