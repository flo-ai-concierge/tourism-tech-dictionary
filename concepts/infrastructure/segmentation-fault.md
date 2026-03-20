# Segmentation Fault (Segfault)

## What it is
A crash that happens when a program tries to access memory it's not allowed to touch. Unlike OOM (running out of space), a segfault means the program tried to open a door it doesn't have permission for. The operating system kills it immediately.

## Tourism Translation
**Wrong key in the lock.** OOM is overbooking (too many guests, not enough rooms). A segfault is different — you have plenty of rooms, but the key doesn't fit the lock. The guest stands at the door, tries the key, it jams, and security removes them.

The key looks right. The door looks right. But the lock mechanism (the native code compiled for a different system) simply won't turn. No amount of jiggling will fix it — you need the right key cut for that specific lock.

## How to tell the difference: OOM vs Segfault
Both show as **exit code 139**, which makes them tricky to diagnose:

| Clue | OOM | Segfault |
|---|---|---|
| Happens after running for a while | Usually yes — memory fills up gradually | Usually instant — crashes on first contact |
| More memory fixes it | Yes | No — same crash with 10x the memory |
| Error message | Sometimes "heap out of memory" | "Segmentation fault" in logs |

**If upgrading RAM doesn't fix exit 139, it's probably a segfault, not OOM.**

## When you'll encounter it
- After a Node.js version upgrade (packages compiled for old version)
- Installing native modules (sharp, onnxruntime, puppeteer) on a different OS or architecture
- Mixing incompatible package versions

## Related concepts
- [OOM — Out of Memory](./oom-out-of-memory.md)
- [SIGKILL / Exit Code 139](./sigkill-exit-code-139.md)
- [Node.js Version Pinning](./node-version-pinning.md)
