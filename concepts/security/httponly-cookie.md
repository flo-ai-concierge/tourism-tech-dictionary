# httpOnly Cookie

## What it is
A browser cookie that is automatically sent with every HTTP request to the server, but cannot be read by JavaScript on the page. Set via the `HttpOnly` flag when the server creates the cookie.

## Plain English
The browser holds onto the session token and sends it silently with every request. But if you type `document.cookie` in the browser console, it won't show up — JavaScript is blind to it. This protects the token from being stolen by malicious scripts.

## Tourism Analogy
**"Like a hotel keycard that unlocks doors but has no markings on it — staff can't read your room number off it, but the door reader knows exactly who you are."**

Every time you tap the keycard, the lock recognizes you and opens. But if someone picks your pocket, they can't read anything useful off the card — it has no visible room number. The security is in the invisibility.

## Why it matters
- `document.cookie` returning empty string does NOT mean you're logged out
- The cookie is still being sent with requests — you'll see 200 OK responses, not 401s
- This is the correct behavior — it means session security is working

## Common confusion
When Claude tested the admin session locally, `document.cookie` returned `""` even though the session was valid. This is correct — the `admin_session` cookie is `HttpOnly`, so JavaScript can't see it but the browser sends it with every API call.

## Learned from
May 14, 2026 — AirROI badge testing session. Misread empty `document.cookie` as a missing session, but 200 OK responses on API calls confirmed the cookie was being sent correctly.
