# GSM-7 vs UCS-2 Encoding

## What it is
The two alphabets SMS uses under the hood. Plain Latin text uses GSM-7, which fits 160 characters per segment. But any emoji, special symbol, or non-Latin character forces the entire message into UCS-2 encoding, which only fits 70 characters per segment. One emoji roughly triples your SMS cost because *every* segment of that message rebills at the smaller size.

## Tourism Translation
**Standard vs. oversize cargo.** A regular suitcase rides the bus trunk for one fare. Swap it for skis, a surfboard, or anything "special" and suddenly you're paying oversize fees on the *whole booking* — not just the surfboard. One 🌊 emoji in a 160-character guest message is the same move: it reclassifies the whole text as oversize, and every piece of it is now billed at the expensive rate.
