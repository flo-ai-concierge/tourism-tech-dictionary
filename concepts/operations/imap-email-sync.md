# IMAP Email Sync

## What it is
Reading emails from a mailbox programmatically on a schedule using the IMAP protocol. The system connects to Gmail (or any email provider), searches for specific emails by sender/subject/label, extracts structured data from the email body, and processes it — all without human interaction.

## Tourism Translation
**"Having an assistant who checks the mail room every 5 minutes, opens review letters, and files them in the right property folder."**

Instead of you manually reading every email notification, your assistant does it automatically. They open the envelope, read who wrote the review and what they said, figure out which property it's about, and file it in the correct folder. By the time you check, everything is organized.

## Why it matters
Google reviews only exist in GHL, which has no public API for reviews and its webhook was blocked (required a Contact that Google reviews don't have). Solution: GHL sends review notification emails to Gmail. Every 5 minutes, our platform reads those emails via IMAP, parses the reviewer name and review text, matches the name to a reservation to find the property, and posts it to the #reviews Slack channel with full details.
