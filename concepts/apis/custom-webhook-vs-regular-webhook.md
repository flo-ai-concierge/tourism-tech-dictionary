# Custom Webhook vs Regular Webhook (GHL)

## What it is
In GoHighLevel, a **regular Webhook action** requires a Contact (a person with email or phone) attached to the workflow execution — if there's no Contact, the webhook is skipped silently. A **Custom Webhook action** fires independently without needing a Contact, giving full control over the HTTP request (method, headers, body).

## Tourism Translation
**"A phone system that only forwards calls if the caller is in your contacts vs one that forwards ALL calls."**

Your old phone system checks caller ID — if the number isn't in your guest database, it drops the call. But Google reviewers aren't in your guest database (they used a Google account, not a phone number). The new system forwards every call regardless of whether you recognize the number. The message gets through either way.

## Why it matters
GHL's review workflow was set up with a regular Webhook action. When Google reviews arrived, GHL tried to fire the webhook but skipped it every time with "This action requires a Contact and none has been provided." Google reviewers don't have email/phone in GHL. The Custom Webhook would have worked — but it turned out GHL doesn't expose review trigger data to Custom Webhooks either. The final solution bypassed webhooks entirely and used Gmail IMAP sync instead.
