# Context Injection

## What it is
Pre-loading relevant data into an AI's memory BEFORE it processes a question, so it already has the answer without needing to call tools or search for information. The data is assembled automatically based on what the user is asking about and injected into the system prompt.

## Tourism Translation
**"Briefing a concierge about today's VIP arrivals before their shift starts."**

Instead of making the concierge look up every guest when they walk in, you hand them a briefing sheet at the start of their shift: "Suite 400 = the Johnsons, anniversary trip, allergic to shellfish, arriving at 3pm." When Mrs. Johnson asks about dinner, the concierge already knows to avoid seafood restaurants — no scrambling, no delays.

## Why it matters
This is the core reason Slack FLO felt "dumber" than Platform FLO. Platform FLO gets an Enriched Brief pre-loaded with guest data, reservation details, and property context. Slack FLO started from zero and had to call tools one at a time. The fix: Property Context Injection — when someone mentions "Flo 14" in Slack, the system auto-fetches that property's reservations, occupancy, and tasks BEFORE FLO starts thinking.
