# Unicode Surrogate (Lone Surrogate)

## What it is
A broken character in text data that makes JSON parsing crash. Unicode uses pairs of special codes (surrogates) to represent complex characters like emojis. A "lone surrogate" is one half of the pair without the other — the computer can't make sense of it, so the entire request fails.

## Tourism Translation
**A guest's name with a symbol the booking system can't display — crashing the whole reservation form.**

Imagine a guest named "José" books through a channel that garbles the accent mark. When that reservation syncs to your PMS, the entire import fails — not just José's booking, but everything in that batch. One broken character takes down the whole pipeline. The fix: sanitize all incoming text before processing, like a front desk clerk who knows to type "Jose" when the system can't handle accents.

## Related concepts
- JSON (JavaScript Object Notation) — the data format that breaks
- Sanitization — cleaning data before processing
