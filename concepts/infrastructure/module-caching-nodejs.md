# Module Caching (Node.js)

## What it is
When a Node.js server starts, it loads all its files into memory once via `require()` calls. After startup, the loaded versions stay in memory permanently — changing a file on disk does NOT change what the running server uses. To pick up code changes you have to fully restart the Node process.

This is different from "hot reload" in development tools. In production, deploys must restart the process or the new code never runs.

## Tourism Translation
**The check-in clerk memorizes the rate sheet at the start of her shift.**

At 7 AM, the night audit prints the day's rates. The check-in clerk reads them once, commits them to memory, and starts her shift. At 10 AM, the revenue manager updates the printed sheet with new pricing.

But the clerk doesn't re-read the sheet. She's been quoting from memory all morning. Every guest checking in between 10 AM and the end of her shift gets the OLD rate. The new sheet is sitting right there on the desk — she just isn't reading it.

The only fix is to clock her out and bring in a fresh clerk who reads the current sheet at the start of her shift.

Same with Node: the only fix is to restart the process. Updating files alone changes nothing.

## How it bit us on Apr 22, 2026
We deployed a major FLO behavior fix to Render. Render showed the deploy as "Live" with a green checkmark. We asked FLO if she had the new tool. She said: "I don't have a my_tool_schema tool."

For 20 minutes we thought the deploy hadn't actually finished. We re-checked Render, looked at deploy logs, retried in fresh conversations. Nothing.

The actual cause was upstream: Render's auto-deploy DID complete, but the issue was that we hadn't added the tool to the right tier in the router (different problem). The point is — when behavior doesn't match deployed code, "did the Node process actually restart?" is one of the first things to check.

If a deploy goes "Live" but behavior doesn't change:
1. Manually restart the service in the host's dashboard
2. Check the runtime logs for the startup banner — confirm the process is fresh
3. Look for telltale "loaded N modules" or "X handlers registered" startup messages

## What restart actually does
- **Terminates the running Node process** (kills all in-memory state)
- **Starts a new process** (fresh module cache)
- **Re-runs all `require()` calls** (loads code from disk)
- **Re-builds in-memory state** (sessions, caches, connections)

Anything cached in memory by the process is lost: in-memory rate limiters, session maps, prompt caches, dedup buffers. Most of this is fine — they rebuild quickly. But know what's in memory before you restart in production.

## How to think about it
"Deploying" in Node has two phases:
1. **Code phase** — new files land on the server's disk
2. **Process phase** — the server kills the old Node process and spawns a new one that reads the new files

Hosts like Render usually do both automatically. But if step 2 is delayed or skipped, your code is on disk but not running. The "deploy live" indicator only confirms step 1 in some setups.

## Related concepts
- [Stale Refactor Trap](../development/stale-refactor-trap.md) — the worse version: even after restart, the new code never runs because nothing imports it
- [Deploy Hash](../development/deploy-hash.md) — confirming WHICH code version is running
- [Prompt Caching (Claude API)](../ai/prompt-caching.md) — different cache, but same "stale until refreshed" pattern
