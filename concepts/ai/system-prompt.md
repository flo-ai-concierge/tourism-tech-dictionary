# System Prompt

## What it is
The permanent instructions given to an AI model at the start of every conversation. Defines its personality, rules, voice, allowed behavior, and forbidden actions. Unlike the user message (which changes every turn), the system prompt is constant for every request.

## Tourism Translation
**"The employee handbook a new housekeeper reads on their first day."**

The handbook says: "Your tone is warm but professional. Never enter a room without knocking. Always knock three times. If a guest is present, apologize and come back later. Do not discuss other guests. Your shift starts at 9 AM. Sign off every note with your initials."

That's the permanent context. Every action the housekeeper takes is shaped by that handbook. When a guest asks them a question, they don't need to re-read the whole handbook — it's already internalized.

The system prompt is the handbook for FLO.

## Why it matters

### Behavior control
A good system prompt is the difference between FLO sounding like a corporate template and sounding like a real FLOHOM team member. Our review-reply prompt includes rules like:
- "Warm, sincere, unmistakably human, not corporate"
- "60-120 words total, 2-3 short paragraphs"
- "Address guest by first name only"
- "Never use em dashes (—)"
- "Never ask the guest to contact you"
- "Sign off EXACTLY: '- The FLOHOM Crew'"

Each rule is there because Brian or Pray flagged a specific behavior they didn't want.

### Rules beat examples
You can train an AI by showing it examples ("here's a good reply, here's a bad reply"), but rules are more efficient and more reliable. "Never use em dashes" is one line that catches every em dash, forever. Showing 20 good examples without em dashes is slower and less certain.

### Real FLOHOM example
The FLO review-reply system prompt is 600+ words, covering voice rules, punctuation rules, what to do on positive vs negative reviews, how to handle "the guest says they tried to reach us" scenarios, operator context injection, and a long NEVER list. Every new constraint goes into the prompt, not into the application code.

### Versioning matters
We version the system prompt (`flohom-reply-v1`, `v2`, `v3`) and store the version with every generated draft. If Brian ever says "the reviews from last Tuesday had a weird tone," we can look up which prompt version was live then and audit the rules.

## In simpler terms
It's the permanent briefing you give a new hire before their first shift. Everything else they do is shaped by that briefing.
