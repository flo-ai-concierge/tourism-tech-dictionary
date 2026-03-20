# OOM — Out of Memory

## What it is
When a computer runs out of RAM (working memory) and the operating system forcibly kills the program. The program doesn't get a chance to save or clean up — it just dies.

## Tourism Translation
**Overbooking.** You sold more rooms than the hotel has. When every room is full and another guest shows up with a confirmed reservation, someone has to go. The hotel can't create rooms out of thin air — it hits a hard physical limit.

The operating system is like the fire marshal: when capacity is exceeded, it shuts things down. No negotiation.

## When you'll encounter it
- Deploying a web app on a small server (like Render's 512MB Starter plan)
- Running a build process that needs more memory than available
- Processing large datasets or images

## Real example
A Next.js 16 app with Turbopack builds needs ~800MB of RAM. If your server only has 512MB, the build gets killed mid-process. The fix: either make the build use less memory (like switching to Webpack) or upgrade to a bigger server (more rooms in the hotel).

## Exit code
OOM kills show as **exit code 139** (SIGKILL) — see `sigkill.md`.

## Related concepts
- [SIGKILL / Exit Code 139](./sigkill-exit-code-139.md)
- [RAM vs Storage](./ram-vs-storage.md)
