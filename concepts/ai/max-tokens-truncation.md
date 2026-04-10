# Max Tokens Truncation

## What it is
When an AI model is given a maximum response length (max_tokens) that's too short, its response gets cut off mid-sentence. If the response is structured data like JSON, the truncation produces broken, unparseable output. The AI finished thinking but couldn't finish writing.

## Tourism Translation
**"A concierge writing a guest welcome letter but running out of paper."**

Your concierge has all the information and starts writing a beautiful personalized welcome letter. But you gave them a post-it note instead of a full sheet — the letter ends mid-word. The guest gets a broken, confusing message. Give the concierge enough paper (tokens) and the letter comes out complete.

## Why it matters
FLO Analyze was set to max_tokens=800. For complex inquiries (like Michele Combs asking about chef pricing, gluten-free options, birthday, AND cleaning fees), FLO's JSON response was too long and got truncated mid-output. The parser couldn't find valid JSON, so the analysis appeared to complete but showed nothing. Bumped to 1,500 tokens and added a multi-strategy parser as backup.
