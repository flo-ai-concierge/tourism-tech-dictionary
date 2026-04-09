# Operator Context Injection

## What it is
A feature where a human operator can inject verified internal facts into an AI's prompt before asking it to generate content. The AI treats the injected facts as ground truth and weaves them into its output naturally.

## Tourism Translation
**"Telling the front desk agent what to know before they reply."**

Guest complains: "I tried to call you at 9 PM about the firepit and nobody answered."

Before the front desk agent drafts a reply, the manager walks over and says: "By the way, I already checked our phone logs and we have no record of a call from that number that night."

Now the agent knows. Their reply can gently note the fact without being accusatory: "Looking at our phone records, we don't show any missed calls from the number on your reservation that evening. We would have loved to help you troubleshoot in the moment."

That's operator context injection. The manager's verified fact shaped the reply.

## Why it matters

### AI can't know what's in your private systems
FLO can read Hostaway, Airtable, the guest platform database, and NWS weather. But she can't read Quo SMS logs, Enso messages, internal incident reports, or anything else not exposed via tool. Without injection, she's guessing on those topics.

### Injection lets humans contribute truth
On the review detail page, there's an "Operator notes for FLO" textarea. Brian or Pray can paste:
> "Checked Quo (MD + VA lines), Hostaway, and Enso — no record of calls or messages received from the guest's reservation number during her stay."

Then click "Regenerate." FLO reads the notes as part of her context, treats them as ground truth, and weaves them into the public reply without being defensive.

### Critical rule: never name the internal systems publicly
The prompt instructs FLO: "Don't reveal private details from operator context beyond what's helpful. Don't name internal systems like 'Quo' or 'Enso' by name to the public — say 'our phone and messaging records' or 'our records' instead."

So when the operator injects "Checked Quo (MD + VA lines)," FLO translates that into "Looking at our phone and messaging records" in the public reply. The fact lands without exposing internal tools to the guest.

### Real FLOHOM example
Brian's direction on Kat Jones's firepit complaint:
> "Use these findings for our response back to her in a kind message explaining according to our phone and message system we didn't receive a call or message from the phone number on the reservation."

Exactly what operator context injection is designed for. Paste the findings, click regenerate, FLO produces a warm non-defensive reply that quietly includes the phone-record fact.

## In simpler terms
It's whispering in the AI's ear before it starts talking: "Hey, by the way, here's what I know that you don't — use this."
