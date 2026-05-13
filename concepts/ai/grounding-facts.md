# Grounding Facts

## What it is
Real, verified data injected into an AI prompt before it generates a response — forcing the AI to narrate around known numbers instead of searching the web or guessing.

## Plain English
Instead of asking the AI "what's the ADR in Virginia Beach?" (which makes it search, guess, or hallucinate), you first load the real ADR from your data source, then tell the AI: "The ADR is $287. Now write a market analysis." The AI becomes a narrator, not a calculator.

## Tourism Analogy
Giving your concierge a printed fact sheet before a guest call. They still write the reply themselves and use their judgment — but the prices, dates, and availability they quote come from the sheet in front of them, not from memory. The sheet grounds the answer in reality.

## Why it matters
Without grounding facts, LLMs fill gaps with plausible-sounding estimates. In market analysis (ADR, occupancy, RevPAR), a wrong number presented confidently is worse than no number at all — especially in underwriting decisions.

## How it works in FLOHOM
- Data source (AirROI API or CSV upload) provides real market metrics
- `navigator-grounding.js` formats the data as a `grounding_facts` object
- Before FLO Concierge researches AirDNA criteria, the grounding facts are injected into the prompt context
- FLO writes narrative around the real numbers; citation shows the data source and date

## Related concepts
- Context injection
- Locked values (for analyst output validation)
- Source-of-truth hierarchy

## Learned from
AirDNA → Market Navigator integration design, May 13, 2026
