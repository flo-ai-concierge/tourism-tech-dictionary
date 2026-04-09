# Singleton (Require Cache)

## What it is
In Node.js, when multiple files import the same module using `require()`, they all get the exact same object reference — not copies. This means if one file modifies the object, every other file sees the change. This is called a "singleton" pattern, and Node's module cache guarantees it automatically. Critical when you need shared state (like a sessions Map) that must be consistent across the entire application.

## Tourism Translation
**One master guest list for the whole hotel.** The front desk, housekeeping, the restaurant, and the valet all read from the same guest list — not photocopies. When front desk checks in a new guest, housekeeping immediately sees they need to prepare the room, and the restaurant knows there's a new dinner reservation. If each department had their own copy of the list, they'd constantly be out of sync.

## When you'll encounter it
- When multiple modules need to share the same data (sessions, configuration, caches)
- When you see `require("./someModule")` used in multiple files and wonder if they get the same instance
- When splitting a monolithic file into modules that all need access to the same Map or Set
