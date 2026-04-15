# Canonical Dedup Key

## What it is
A single standardized identifier used across multiple systems to prevent the same item from being recorded more than once. Instead of each system generating its own unique ID for the same thing, all systems use one shared format (the "canonical" key). If two systems both process the same review but use different IDs, the database can't tell they're duplicates — a canonical key solves this.

## Tourism Translation
**One universal booking reference number.** When a guest books through Airbnb, VRBO, and your direct site, each platform gives the booking a different confirmation number. If your PMS doesn't normalize these into one reference, you might think you have three separate bookings instead of one. A canonical key is like saying "all systems will identify this booking as GUEST_SMITH_JUN10" — so no matter which platform reports it, your system knows it's the same booking.
