# RFC 5322 Message-ID

## What it is
Every email has a unique `Message-ID` header baked in by the sending mail server. It's a globally unique fingerprint per email — defined by the email standards body (RFC 5322). Format usually looks like `<random-string@sending-domain.com>`. Two distinct emails can never have the same Message-ID, even if their content is identical.

## Tourism translation
**The unique confirmation number on every reservation.**

Two siblings book the same villa for the same week through Airbnb — they each get their own confirmation number (`HMABCD123` and `HMABCD124`). Same property, same dates, same family — but different bookings, different confirmation numbers, different IDs in your system.

Email Message-IDs work the same way: the sender's mail server stamps each outgoing email with a unique ID before it ever leaves the building. Two emails about the same event = two different Message-IDs.

## When you'd see it
- Building an email scanner that needs to skip already-processed emails.
- Threading replies in an email client (each reply references the parent's Message-ID).
- Detecting duplicate emails that arrive via different paths (forwarded, BCC, mailing list).
- Audit logs that need to point to a specific email.

## How to use it
In a Node IMAP scanner, the Message-ID is exposed via `msg.envelope.messageId`:

```js
for await (const msg of client.fetch({ from: "noreply@minut.com" }, { envelope: true })) {
  const messageId = msg.envelope?.messageId;
  // Store this in a dedup table — never process the same messageId twice.
}
```

## The gotcha
Message-ID dedup is necessary but not always sufficient. Some senders dispatch two separate emails for the same event (different Message-IDs because they're truly different emails, even though the underlying event is the same). For those cases, you need a SECOND dedup layer keyed on the event itself, not the email.

We hit this with Minut sensor alerts — two emails per noise event, two different Message-IDs, both passed Message-ID dedup, both posted to Slack. Fix was adding event-level dedup as Layer 2.

## Why it matters
A correctly-implemented Message-ID dedup is the foundation for any reliable email scanner. Without it, every server restart or scan retry creates duplicates. With it, you have an exactly-once guarantee at the email level (and you can build event-level dedup on top if needed).

## Learned from
FLOHOM Gmail scanners — Minut, Google Reviews, GHL Reviews, Google Alerts. All use Message-ID dedup as Layer 1.

## Related concepts
- [`databases/two-tier-dedup`](../databases/two-tier-dedup.md) — when Message-ID alone isn't enough
- [`apis/imap-email-scanner`](imap-email-scanner.md) — fetching emails programmatically
- [`development/db-backed-dedup`](../development/db-backed-dedup.md) — persisting Message-IDs across restarts
