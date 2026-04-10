# Deduplication Key

## What it is
A unique fingerprint for each record so the same item isn't imported twice when data comes from multiple sources or syncs run repeatedly. The key is constructed from stable, unique attributes of the data (like author + body text hash) and checked before inserting.

## Tourism Translation
**"Stamping each guest review with a unique code so if the same review arrives from two sources, you only file it once."**

A guest leaves a 5-star Google review. The notification arrives via email AND via your booking system. Without a dedup stamp, you'd file it twice — inflating your review count and confusing the team. With a dedup key (like "lapaul_gray_very_nice_stay"), the second arrival is recognized as a duplicate and skipped.

## Why it matters
Google reviews now enter FLOHOM through Gmail sync (primary) and potentially through Hostaway (secondary). Without deduplication, every review would appear twice in the #reviews Slack channel. The dedup key combines the reviewer name + first 50 characters of the review body into a unique source_id. If the same review arrives from both sources, only the first one is ingested.
