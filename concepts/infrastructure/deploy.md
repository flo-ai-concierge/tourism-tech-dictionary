# Deploy

## What it is
Taking your code from development and making it live for real users. This involves building the application (compiling it into a form the server can run) and starting it on a production server.

## Tourism Translation
**Opening the newly renovated room to guests.** You've been working on upgrades — new paint, new furniture, new fixtures. "Deploy" is the moment you mark the room as available, update the listing, and the first guest can book it. The renovation is over; it's live.

If the renovation has a problem (bad plumbing, broken AC), the guest experiences it. That's why you test before deploying — just like you'd do a walkthrough before opening the room.

## When you'll encounter it
- After pushing code to GitHub, platforms like Render automatically deploy
- When you see "Deploy started" or "Deploy failed" in Render
- When testing locally works but production doesn't — the deploy environment is different from your laptop

## Deploy vs development
Your laptop is the **model room** — you test and preview there. Production (Render) is the **actual guest room**. They look similar but have different constraints (memory, network, environment variables).

## Related concepts
- [Git Push](../development/git-push.md)
- [OOM — Out of Memory](./oom-out-of-memory.md)
- [Environment Variables](../security/environment-variables.md)
