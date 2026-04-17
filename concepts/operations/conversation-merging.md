# Conversation Merging

## What it is
Stitching two or more communication threads into a single unified timeline. A guest who texts you on SMS, then follows up on Airbnb, then emails — all three become one conversation view. Messages stay in their original chronological order; the channel each came from is preserved as metadata.

## Tourism translation
Combining two folders for the same guest family at the front desk into one master file. Sarah stayed in March under her work email, then rebooked in July under her personal email — same person, so the two files get clipped together. But every document keeps its original date stamp so you can trace the history.

## When you'd see it
- Unified inboxes (Front, Help Scout, Intercom, Gladly)
- CRM contact merging
- Support ticket consolidation
- Any system where one entity interacts via many channels

## Why it matters
Without merging, every channel is a silo. Your team answers the same question three times because SMS, email, and web chat each show a fragment of the conversation. The guest feels unseen. With merging, anyone opening the thread sees the whole story — including what the guest said two months ago on a different channel.

## Design principles (learned the hard way)
- **Preserve origin**: every message should remember what channel it came from (badge, divider, color).
- **Make merges reversible**: stamp each migrated message with its `pre_merge_conversation_id` so you can unmerge later without guessing.
- **Use deterministic matching only for auto-suggest**: never auto-merge on fuzzy name matches — the cost of a wrong merge (leaking guest A's messages into guest B's thread) is high.
- **Tombstone the source**: leave a redirect behind so new messages to the merged-away thread route to the target.
- **Audit everything**: write a note on both sides recording who merged what and when.

## Learned from
FLOHOM inbox merging (Apr 17, 2026). Hostaway threads (Airbnb/VRBO/Direct) and QUO SMS threads for the same guest can now be merged into one timeline. The merged thread shows channel chips at the top, channel-switch dividers between messages, and per-source unmerge buttons for reversal. Each migrated message carries a `pre_merge_conversation_id` so unmerge restores them exactly.
