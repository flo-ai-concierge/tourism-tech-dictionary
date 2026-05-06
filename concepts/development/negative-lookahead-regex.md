# Negative Lookahead Regex

## What it is
A regex pattern that matches a string only if it is **NOT followed by** (or does not contain) a specific sub-pattern. Written as `(?!...)`. In practice: "match everything that doesn't look like this."

## The pattern
```
/((?!floex\/).)*
```
Breakdown:
- `((?!floex\/).)` — match any single character that is NOT the start of `floex/`
- `*` — repeat that for the whole string
- Result: match any path that does NOT contain `floex/` at that position

Used in Next.js `headers()` source rules to apply one header policy to all routes EXCEPT the boarding pass:
```js
// Applies to every route EXCEPT /floex/*
{ source: "/((?!floex\\/).)*", headers: [...] }
```

## Tourism translation
Imagine a hotel key card programmed to open every door **except** the spa wing. You don't list all the doors it opens (there are hundreds) — instead you define the one exception.

A negative lookahead is the "except" clause in a rule that would otherwise match everything.

## When you'll see it
- Route-specific middleware rules where you want "apply to everything except X"
- Next.js `headers()` / `rewrites()` / `redirects()` — the `source` field is a path-to-regexp pattern
- Nginx location blocks (`location !~ /admin/`)
- Any situation where whitelisting the exception is easier than listing all inclusions

## Gotcha
In `next.config.mjs`, backslashes need to be double-escaped in JS strings: `(?!floex\\/)` in the JS source compiles to the regex `(?!floex\/)`. Easy to get wrong — always test with a regex debugger if the rule behaves unexpectedly.

## Related concepts
- Positive lookahead: `(?=...)` — match only IF followed by a pattern
- Lookbehind: `(?<!...)` / `(?<=...)` — look at what came before
- Non-capturing group: `(?:...)` — group without capturing

## Learned from
FLOHOM FLOx Config admin preview panel (May 6, 2026). Needed `X-Frame-Options: DENY` on all routes globally, but `SAMEORIGIN` specifically on `/floex/*` so the admin could iframe the boarding pass. The negative lookahead pattern let a single Next.js header rule cover "all non-floex routes" without listing every individual route.
