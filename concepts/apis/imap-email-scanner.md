# IMAP Email Scanner

## What it is
A program that connects to an email inbox using the IMAP protocol, reads specific emails (filtered by sender, subject, or date), extracts structured data from them, and stores it in a database. It works silently in the background — no one needs to manually read or forward the emails.

## Tourism translation
Like a concierge who checks the front desk mailbox every few hours, opens only the review notification letters (ignoring junk mail), logs each review in the guest feedback binder with the guest name, property, and star rating, then puts the letter back. The property owner never needs to touch the mailbox — the system handles it automatically.

## When you'll encounter it
- Automatically ingesting Google review notifications from your business email
- Processing booking confirmation emails from OTAs
- Extracting guest communication from email into a centralized inbox

## Related concepts
- Webhooks — a push-based alternative where the email service notifies you instead of you checking
- App passwords — special passwords for programmatic email access (not your main password)
- Email parsing — extracting structured data from unstructured email content
