# LLM Hallucination vs Upstream Bug

## What it is
When an AI gives wrong output, the instinct is "the AI is hallucinating." Often it isn't — the AI is correctly relaying wrong information that YOUR code fed it. Before adjusting the prompt, check the data you sent the AI. The bug is upstream of the model 80% of the time.

## Tourism translation
**"The chef cooked the wrong dish."**

A guest complains they got fish when they ordered chicken. You yell at the chef. But check the order ticket first — the waiter wrote down the wrong order. The chef cooked exactly what was on the ticket. Yelling at the chef won't fix anything; you need to fix the waiter's process.

Same with AI: the model "cooked" what your code "wrote on the ticket." Always inspect the ticket (the prompt + context you sent) before assuming the chef (the model) is the problem.

## How to tell which it is

| Signal | Likely cause |
|---|---|
| AI repeatedly produces the same wrong fact | Upstream bug — you're sending the wrong fact |
| AI invents a detail that's nowhere in the prompt | True hallucination |
| AI uses a word/category from the prompt's definition list | Upstream bug — your prompt mentioned it as an option |
| AI does math that contradicts a flag you sent | Upstream bug — your flag was wrong, OR your prompt let the AI compare raw values |
| AI's answer is plausible but factually wrong | Could be either — log the full prompt and verify |

## The diagnostic step
Before changing the prompt, log the EXACT JSON you sent to the model on the failing call. Read it as if you're the model. Does it actually point to the right answer? If not, the bug is in your code — fix the data, not the prompt.

## When you'd see it
- An AI concierge gives the wrong room number → check what room number your tool actually returned.
- An AI gives wrong availability → check what your inventory query returned for that date.
- An AI makes a wrong day-of-week determination → check the timezone of the date you sent.
- An AI mentions "cleaners during turnover" when the guest is clearly there → check what relationship flag your code computed.

## Why it matters
We had FLO Minut posting "Cleaners on site during turnover" for alerts during a guest's clear active stay. Three rounds of prompt-tightening didn't fix it. Reading the actual context I was sending FLO revealed I had the WRONG `relationship` flag — a timezone bug in my code was lying to FLO. Once I fixed my code, FLO immediately produced correct output. Without checking the upstream data, I'd still be tweaking the prompt.

## Learned from
FLOHOM Minut FLO guidance (Apr 18, 2026). Two prompt-fix attempts that both failed because the actual bug was in the JS date conversion code feeding the prompt.

## Related concepts
- [`ai/data-integrity-rules`](data-integrity-rules.md) — preventing the AI from inventing facts
- [`ai/locked-values`](locked-values.md) — protecting critical numbers from AI mutation
- [`databases/utc-midnight-timezone-bug`](../databases/utc-midnight-timezone-bug.md) — common upstream bug that misleads AI
