# E.164 Phone Number Format

## What it is
The international standard for phone numbers: a plus sign, then country code, then the number with no spaces or dashes. US/Canada numbers look like `+16672708226`. Required by virtually every SMS and voice API in the world.

## Tourism Translation
**"Like how airline tickets always use 3-letter airport codes (BWI, DCA, LAX) — one universal format so every system understands it."**

A guest might write their phone number as "(667) 270-8226" or "667.270.8226" or "6672708226" or "1-667-270-8226." These are all the same number, but different systems can't always parse different formats. E.164 is the universal format that every phone system on earth agrees on.

When your booking system needs to send an SMS to a guest, it normalizes whatever format the guest typed into E.164 first. Just like when you book a flight, the system converts "Baltimore" to "BWI" — the human-friendly version gets translated to the machine-friendly version behind the scenes.

## Why it matters

### API compatibility
QUO, Twilio, GHL, and every SMS provider require E.164 format. Send `(667) 270-8226` and the API rejects it. Send `+16672708226` and it works.

### International readiness
The format includes country code (+1 for US/Canada), so when you expand to international markets, the same format works everywhere — +44 for UK, +61 for Australia, etc.
