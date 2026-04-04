# Listing ID Hallucination

## What it is
When an AI invents a property ID that doesn't exist because it was never given the list of valid IDs. The AI pattern-matches (e.g., "FLO 14 probably has ID 260014") instead of looking up the real ID (407612).

## Tourism translation
Imagine asking a new front desk agent to look up "Room 14" in the system. Instead of checking the computer, they type "14" into the room number field — but your hotel uses alphanumeric codes (room 14 is actually coded as "NH-407"). The agent guessed wrong and now they're looking at the wrong room's data.

That's listing ID hallucination. The AI guessed a property identifier instead of using the verified lookup table.

## The fix
Give the AI a strict enum (fixed list) of valid IDs with their mappings. The AI can ONLY pick from this list — it cannot fabricate a new one.

```
1=146908, 2=146944, 3=146946, 4=260001, 5=278502,
6=345316, 7=366176, 8=376368, 9=383097, 10=404358,
11=427313, 12=422608, 13=485833, 14=407612, 15=467334
```

## Real example
Travis asked FLO "how many days has FLO 14 been occupied?" FLO used listing ID `260014` — which doesn't exist. The real ID is `407612`. FLO returned "no reservations found" when FLO 14 was actually 100% occupied. Fix: added the enum to all tool schemas so FLO can only use real IDs.

## When you'll encounter it
- Any AI tool that takes a property ID as input without a constrained list
- Any integration where the AI needs to map a human-friendly name to a system ID
- API calls that silently return empty results on wrong IDs (no error, just no data)

## Related concepts
- [Data Integrity Rules](data-integrity-rules.md) — verify before stating facts
- [API Endpoint](../apis/api-endpoint.md) — how IDs are passed to external systems
