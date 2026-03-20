# SIGKILL / Exit Code 139

## What it is
A signal sent by the operating system to forcibly terminate a program. The program cannot catch, ignore, or handle this signal — it's an immediate shutdown. Exit code 139 means the program was killed by SIGKILL, usually due to running out of memory.

## Tourism Translation
**The fire marshal shutting down the venue.** When occupancy exceeds the legal limit, the fire marshal doesn't ask politely or give warnings. They walk in and shut it down immediately. The event is over. No appeals, no "just five more minutes."

Regular program errors are like a guest complaint — you can handle it, respond, recover. SIGKILL is the fire marshal. Game over.

## When you'll encounter it
- Server deploy logs showing "Exited with status 139"
- Build processes that crash without any error message
- Programs that just vanish without logging anything

## Why there's no error message
Because the program is killed instantly — it never gets a chance to write an error log. It's like the fire marshal pulling the power cord. The DJ didn't get to say goodnight.

## Related concepts
- [OOM — Out of Memory](./oom-out-of-memory.md)
