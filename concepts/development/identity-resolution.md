# Identity Resolution

## What it is
Figuring out which records across different systems belong to the same person. You link them using unique identifiers like email, phone number, or a customer ID. When "Sarah Smith" on Airbnb, "+1 555-0100" on SMS, and "sarah@gmail.com" on the web chat are all the same human, identity resolution is the process that connects them.

## Tourism translation
Recognizing a returning guest. Sarah booked with you in 2024 under her maiden name, then booked again in 2026 under her married name — same phone number, same email. Identity resolution is realizing it's the same guest so you can greet her by name and skip the "first time?" questions.

## When you'd see it
- Unified inboxes stitching messages from multiple channels into one thread
- CRM systems merging duplicate contacts
- Loyalty programs recognizing the same guest across multiple properties
- Fraud detection linking suspicious behavior across accounts

## Why it matters
Without it, every channel is a silo. A guest who texts you asking about check-in, then emails asking the same question, gets answered twice by two different team members — and neither knows the other replied. The guest feels unheard. Your team wastes time.

## Deterministic vs probabilistic
- **Deterministic** = exact match (same email, same phone). 99%+ accuracy.
- **Probabilistic** = similarity scoring (same name + same city + same stay dates). Lower confidence, needs human review.

Always start deterministic. Fall back to probabilistic only with a confidence threshold and a human-in-the-loop for ambiguous cases.

## Learned from
FLOHOM inbox cross-channel merging (Apr 17, 2026). When a guest books on Airbnb and texts your QUO number, identity resolution matches the QUO `guest_phone` against the Hostaway reservation phone (last 10 digits, normalized) so their two threads can be merged into one.
