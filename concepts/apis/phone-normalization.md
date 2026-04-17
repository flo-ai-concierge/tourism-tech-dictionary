# Phone Normalization (E.164)

## What it is
Stripping formatting from phone numbers so every variation of the same number looks identical to the database. `+1 (443) 825-7132`, `(443) 825-7132`, `443.825.7132`, and `4438257132` all normalize to the same 10-digit string `4438257132` (or the E.164 standard `+14438257132`).

## Tourism translation
The same guest whether they write their number on the check-in form as "Four four three, eight two five, seven one three two" or "+1-443-825-7132" or "(443) 825-7132." It's one number. Your system should treat it that way.

## When you'd see it
- Matching contacts across CRM / SMS / voice systems
- De-duplicating customer records
- SMS delivery (many APIs require strict E.164 format: `+` + country code + number)
- Click-to-call implementations

## Why it matters
Without normalization, "+1 (443) 825-7132" and "4438257132" look like two different phone numbers to your database. You'd create two guest records, miss the connection between SMS and booking, and send duplicate messages. A simple `regexp_replace(phone, '\D', '', 'g')` + `right(..., 10)` fixes 90% of the pain.

## Typical formula
```
take_last_10_digits(strip_non_digits(phone))
```
This ignores country code, spaces, dashes, parens, dots, and formatting. Good enough for matching; not good enough for dialing (you still need the `+1` for that).

## E.164 proper
The full standard adds the country code prefix: `+14438257132`. Use this for outbound calling/SMS APIs. For matching, last-10-digits is usually sufficient within a single-country deployment.

## Learned from
FLOHOM inbox merge-candidates query. When matching a Hostaway reservation's phone against a QUO SMS conversation's phone, both sides normalize via `RIGHT(REGEXP_REPLACE(phone, '\D', '', 'g'), 10)` before comparing. That's how a reservation with `+1 (443) 825-7132` matches an SMS thread with `+14438257132`.
