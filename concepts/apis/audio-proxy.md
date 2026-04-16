# Audio Proxy

## What it is
A server-side relay that fetches audio (or any media) from a blocked external source and re-serves it from your own domain. This bypasses CORS restrictions because the browser sees the content coming from the same origin as your web app.

## Tourism translation
Like a concierge who picks up your takeout order from a restaurant that won't deliver to the hotel. You get the food, the restaurant's no-delivery policy is respected, and you never had to leave the building.

## When you'd see it
- Playing voicemail recordings from third-party phone systems
- Embedding images or videos from CDNs that don't allow cross-origin access
- Any media that works when you open the URL directly but won't load inside your app

## Security note
Always whitelist allowed domains — don't let the proxy fetch from ANY URL, or attackers could use it to access internal services.

## Learned from
Built /api/admin/audio-proxy on Apr 16, 2026 to stream OpenPhone voicemail recordings in the FLOHOM inbox. Whitelisted to m.openph.one and storage.googleapis.com only.
