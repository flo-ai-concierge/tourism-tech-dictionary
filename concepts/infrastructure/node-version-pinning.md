# Node.js Version Pinning

## What it is
Locking your application to a specific version of Node.js (the JavaScript runtime) so that every environment — your laptop, your server, your deploy pipeline — uses the same one. Without pinning, the server might pick a newer version that breaks things.

## Tourism Translation
**Making sure the contractor has the right key to the building.**

You hired a contractor (Render) to renovate your hotel (deploy your app). But when they showed up, the building management had changed all the locks to a new system (Node 22). The contractor's key (your code + packages) doesn't fit the new locks. They can't even get in the door — they just stand there jiggling the handle until security escorts them out (segfault → exit 139).

The fix: tell building management "use the old locks that work with our keys" (pin to Node 20). Contractor walks in, does all 7 renovation phases in one visit. Everything works.

You CAN upgrade to the new locks later — but only after you've cut new keys for every door (updated all packages to be compatible).

## The cascade lesson
If you planned 7 renovation phases but the contractor couldn't get in the building, nothing got done. ALL 7 phases failed — not because anything was wrong with the renovation plans, but because of the lock. Once the right key was used, all 7 phases completed in one visit. You don't redo each phase individually.

**This is how deploys work.** Each deploy builds everything. One successful deploy ships ALL the code from every previous failed attempt. The old failures are just history.

## How to pin
A `.node-version` file in your project root:
```
20
```
That's it. One line, one number. The server reads this and uses that version.

## When you'll encounter it
- Deploy suddenly fails after months of working fine (server auto-upgraded Node)
- "Segmentation fault" in build logs (incompatible native modules)
- Works on your laptop but crashes on the server (different Node versions)

## Real example (FLOHOM, Mar 21 2026)
- Render defaulted to Node.js 22.22.0
- Native modules (onnxruntime, sharp) segfaulted on install
- 7 consecutive deploys failed — looked like OOM but was actually wrong Node version
- Fix: added `.node-version` file with `20`
- All 7 deploys' worth of code shipped in one successful build

## Related concepts
- [SIGKILL / Exit Code 139](./sigkill-exit-code-139.md)
- [Deploy](./deploy.md)
- [OOM — Out of Memory](./oom-out-of-memory.md)
