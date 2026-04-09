# Lazy Require

## What it is
Importing a module only when it's actually needed (inside a function call), not at the top of the file when the application starts. Used to break circular dependencies — when File A imports File B, and File B imports File A, one of them will see an incomplete module at startup. By making one of the imports "lazy" (deferred to runtime), both files have time to fully initialize first.

## Tourism Translation
**Calling the on-call plumber only when there's a leak.** Instead of having the plumber sit in the hotel lobby from 6 AM "just in case," you call them when a pipe actually bursts. The plumber is available (on-call), but only activated when needed. This avoids the awkward situation where the plumber shows up before the hotel is even open (circular dependency) and can't find the maintenance closet because the building manager hasn't arrived yet.

## When you'll encounter it
- When two files need to use each other's functions (circular dependency)
- When you see `function getSlackBot() { return require("./slackBot"); }` instead of a top-level `const slackBot = require("./slackBot")`
- When the app crashes at startup with "Cannot read property X of undefined" — often a circular dependency issue
