# Ephemeral Filesystem

## What it is
A temporary storage area on a server that gets wiped every time the application restarts or redeploys. Files saved here look permanent but disappear without warning.

## Tourism translation
Imagine writing guest preferences on a whiteboard at the front desk. It works great — until the night cleaning crew erases the whiteboard every night. Next morning, all the notes are gone.

That's an ephemeral filesystem. Your app writes data to a file on the server, but every time the server redeploys (which can happen daily or even hourly), everything is wiped clean.

The fix: write important data to a database (PostgreSQL, etc.) instead of a file. That's like putting guest preferences in the computer system instead of on the whiteboard — it survives the cleaning crew.

## When you'll encounter it
- Propane tank levels saved to a JSON file on Render → wiped on every deploy
- Upload folders that accumulate files → gone after restart
- Cache files that need to persist → disappear unexpectedly
- Any "save to file" operation on a cloud hosting platform (Render, Heroku, Railway)

## The fix
Move persistent data from files to a database. The file was convenient for development but is not reliable in production.

## Real example
FLOHOM's propane tracker stored tank levels in `.propane-tracker.json`. The team reported levels on March 8. By the next deploy, the file was reset to `{}`. FLO told the team "no data recorded" — because it was literally erased. Fix: moved to PostgreSQL.

## Related concepts
- [Database Migration](../databases/database-migration.md) — moving data to a persistent store
