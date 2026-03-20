# Environment Variables

## What it is
Secret values stored outside your code — API keys, passwords, database URLs, tokens. They're set on the server (like Render) and your code reads them at runtime. They never go into GitHub or your codebase.

## Tourism Translation
**The safe in the back office.** Master keys, alarm codes, vendor account numbers, Wi-Fi admin passwords, safe combinations. These are written down once, locked in the office safe, and accessed only when needed. You'd never tape the alarm code to the front door or print it on the guest welcome card.

Environment variables work the same way. The API key to your Hostaway account is like the master key to all 15 properties — it must be protected, never shared publicly, and stored separately from everything else.

## When you'll encounter it
- Setting up a new service (you'll need to add env vars in Render)
- When code works locally but fails in production — often a missing env var
- When you see errors like "API key not found" or "unauthorized"
- The `.env` file on your laptop is the local copy; Render's dashboard has the production copy

## Golden rule
**Never commit secrets to GitHub.** If an API key ends up in a commit, it's public forever (even if you delete it later). Treat env vars like the master key — they stay in the safe.

## Related concepts
- [Deploy](../infrastructure/deploy.md)
