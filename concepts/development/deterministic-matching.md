# Deterministic Matching

## What it is
Linking two records only when they share an **exact** confirmed identifier — same email address, same phone number, same customer ID. No guessing, no "probably the same person." Either the field matches character-for-character (after normalization) or it doesn't.

## Tourism translation
Checking in a guest only if the ID matches the reservation name exactly. Driver's license says "Sarah M. Johnson," reservation says "Sarah Johnson" — that's a mismatch you escalate to the manager, not something you wave through.

## When you'd see it
- Customer data platforms linking records across channels
- De-duplication pipelines
- Any time "false positives would be worse than false negatives"
- Compliance-heavy domains (finance, healthcare, legal)

## Why it matters
Deterministic matching is boring and reliable — ~99%+ accuracy when a match fires, though it misses cases where identifiers are missing or different. It beats the alternative (probabilistic matching — guessing based on similar names, dates, locations) when mistakes are costly. Merging the wrong two guest profiles means leaking Sarah's private messages to Steve. Deterministic matching refuses to make that call unless the identifier is literally identical.

## Pair it with probabilistic (carefully)
Deterministic handles the easy 70–80% of cases. For the rest — missing phones, typo'd emails, nicknames — you fall back to probabilistic scoring with a human review step. Never let probabilistic matches auto-merge.

## Learned from
FLOHOM inbox cross-channel merging. Merge suggestions fire only on `guest_id` match or exact normalized-phone match — both deterministic. Name-based matches are collected but never shown as auto-suggestions because "Sarah Johnson" could be two different guests.
