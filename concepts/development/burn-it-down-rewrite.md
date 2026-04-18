# Burn It Down Rewrite (vs Iterative Patching)

## What it is
A judgment call about when to STOP patching a buggy module and rewrite it from scratch instead. After enough failed fixes (often 5+), each new patch makes the code messier without solving the problem. At some point, throwing away the file and writing a clean version takes less time than the next patch attempt — and produces better code.

## Tourism translation
**The leaking faucet with five Band-Aid repairs.**

Different plumbers tried different fixes: tightened the valve, replaced the washer, swapped the cartridge, sealed the joint, added a clamp. The faucet still leaks. Each repair left scars (drilled holes, exposed pipe, mismatched parts). The next plumber's choice: try repair #6 on top of five failed attempts, or rip the whole assembly out and install a new faucet?

The new faucet is faster, cleaner, and actually works. The accumulated repairs were making the underlying problem harder to diagnose, not easier.

## Signals it's time to rewrite
- Same bug "fixed" 3+ times, keeps reappearing in different forms.
- Code has accumulated workarounds, defensive checks, comments saying "TODO: real fix later."
- Each new fix breaks something else.
- File length keeps growing without features being added.
- You have to read the git log to understand why specific lines exist.
- Adding a new feature requires touching code in 5 different places.

## How to do it well
1. **Be honest with the user/stakeholder** — say "this has been patched too many times. I'm rewriting from scratch using your model."
2. **Anchor on the user's mental model** — get the explicit step-by-step they expect (FLOHOM example: 8 numbered steps from email arrival to Slack post).
3. **Start from a blank file** — don't rebuild from the old code's structure. Use the old file as historical reference, not template.
4. **Strip everything optional** — drop alert tracking, cluster lookups, complex caches. Only the user-visible behavior. Add features back if asked.
5. **Pick the simplest dedup/state model that COULD work** — start there. Add complexity only when needed.
6. **Test by re-running real production data through the new code** — not synthetic tests. The bugs lived in real-world quirks; reproduce against real-world data.

## What to keep from the old code
- The output format (if approved by user).
- The field/column names (so you don't break consumers).
- Hard-won regex patterns or parsers (they often encode quirks of upstream data).
- The integration setup (auth, env vars, scheduled triggers).

## When NOT to rewrite
- The bug is in ONE function, not the whole module.
- The module has tests that prove most behavior works.
- You don't fully understand what the old code does (don't rewrite based on guesses).
- The next patch attempt is cheap and well-scoped.

## Why it matters
The FLOHOM Minut scanner accumulated 9 attempted dedup fixes in 4 days. Each one made the file longer (973 lines), more confusing, and still produced duplicates. The 10th attempt would have been more of the same. Rewriting from scratch — anchored on the user's 8-step mental model — produced 299 lines, was ready in 30 minutes, and exposed the actual root causes (timezone bug, AI hallucination, multi-email per event) one by one in clean diffs.

## Learned from
FLOHOM Minut → Slack pipeline (Apr 18, 2026). Pray's directive: "delete everything you know about this... start from scratch... rerun the last 5 emails I received and from there I will judge if you got it correct this time."

## Related concepts
- [`development/monolithic-file`](monolithic-file.md) — when files get too big
- [`development/module-extraction`](module-extraction.md) — alternative to full rewrite when scope is clear
