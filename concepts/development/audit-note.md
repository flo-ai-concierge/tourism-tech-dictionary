# Audit Note

## What it is
An automatic log entry the system writes every time a sensitive or irreversible action happens. Who did it, what they did, when, and (ideally) why or how much. Not a debug log — a permanent record intended for humans to read later.

## Tourism translation
A night auditor's log at the front desk:
> "3:42am — Suite 12 guest called, reported loud AC. Maintenance paged. — J. Wyles"

Three months later, someone investigating a refund request can read that exact line and know what happened. No guessing.

## When you'd see it
- Merging or deleting customer records
- Approving refunds or compensation
- Changing permissions
- Bulk operations (imports, syncs, batch updates)
- Any action that changes state in a way that's hard to reverse

## Why it matters
Without audit notes, you're playing detective every time something looks wrong. "Why are these two threads merged? Who merged them? When?" With audit notes: the answer is right there in the conversation history, timestamped, with an actor name. Disputes, rollbacks, and post-mortems all become boring lookups instead of forensic work.

## What makes a good audit note
- **Who**: actor name or email (not just "admin")
- **What**: specific action + object IDs (`Merged conversation #123 into this thread`)
- **When**: timestamp (usually auto from `created_at`)
- **Scope**: how many things were affected (`52 messages moved`)
- **Writable by the system, not by humans**: keep it immutable so it can't be edited after the fact

## Common pattern
A dedicated `audit_log` or `conversation_notes` table that the UI renders as a readable trail. Notes are append-only — never edit or delete them, even if the underlying record changes.

## Learned from
FLOHOM inbox merge/unmerge (Apr 17, 2026). Every merge writes a note on the target: *"Merged conversation #1411402 into this thread (52 messages moved) — Pray Nadal"*. Every unmerge writes notes on **both** sides: *"Unmerged conversation #1411402 from this thread"* on the target, *"Restored from merge with #1422877"* on the source. Complete paper trail, both directions.
