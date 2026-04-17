# Tombstone Routing

## What it is
After you merge or delete a record, you leave a "gravestone" behind — a row that's no longer active but still exists and points to where the new/combined record lives. When something new arrives addressed to the old record, the tombstone redirects it to the right place.

## Tourism translation
When you renumber Room 12 to Suite 205, you leave a small note on the old door: "Guest moved to Suite 205, forward all calls, packages, and room service there." The old room is still labeled — but anything addressed to it gets redirected automatically.

## When you'd see it
- Merged customer records where new orders might still arrive under the old ID
- Email aliases where the old address forwards to the new one
- URL redirects after a website restructure
- Soft-deleted records with forwarding pointers
- HTTP 301 "Moved Permanently" responses

## Why it matters
Without tombstone routing, new activity for a merged record becomes an orphan. Imagine merging Sarah's two guest files into one master, but then a new email from her arrives addressed to the old file — and it just... disappears because the system doesn't know where to put it. Tombstones close that gap.

## How it's usually implemented
Keep the old record but set flags on it:
- `merged_into_id` → points to the surviving record
- `original_id` → preserves the external ID for lookup
- Active queries filter out tombstones (`WHERE merged_into_id IS NULL`)
- Inbound webhooks check for tombstones and follow the pointer

## Learned from
FLOHOM inbox merge/unmerge (Apr 17, 2026). When a QUO SMS conversation is merged into a Hostaway conversation, the QUO row is tombstoned (`merged_into_id` set). The QUO webhook and sync engine both check for tombstones — if an incoming SMS matches a tombstoned conversation, the message routes to the merge target instead of landing in the dead row.
