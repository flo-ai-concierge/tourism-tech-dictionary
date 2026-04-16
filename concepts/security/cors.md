# CORS (Cross-Origin Resource Sharing)

## What it is
A browser security rule that blocks web pages from loading resources (audio, images, data) from a different domain unless that domain explicitly allows it via special HTTP headers. The server has to say "yes, this website is allowed to use my stuff."

## Tourism translation
Like a resort's pool that only lets registered guests in. If an outside restaurant wants to send drinks to the pool, the pool management has to approve that restaurant specifically. Without approval, the delivery gets turned away at the gate — even if the drink is perfectly fine.

## When you'd see it
- Playing audio/video from external CDNs in your web app
- Loading images from third-party storage
- Making API calls from the browser to a different domain
- The browser console shows "blocked by CORS policy" errors

## How to fix it
Either the external server adds CORS headers (they allow your domain), or you proxy the content through your own server so the browser sees it coming from the same domain.

## Learned from
OpenPhone voicemail recordings hosted on m.openph.one couldn't play in the FLOHOM inbox because OpenPhone's CDN didn't send CORS headers. Fixed by proxying audio through /api/admin/audio-proxy.
