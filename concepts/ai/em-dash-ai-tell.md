# Em Dash as AI Tell

## What it is
A typography habit (the long horizontal dash, "—") that large language models overuse in their writing. When humans see an em dash in a casual reply, especially one followed by hedge-phrasing, they instinctively sense "this was written by AI." Banning em dashes from AI output is a cheap way to make the writing feel more human.

## Tourism Translation
**"A canned phrase that screams 'this was written by a template, not a human.'"**

You know the phrases: "Reaching out to touch base on..." "We value your feedback." "Your satisfaction is our top priority." Any staff member who uses these phrases in a direct conversation sounds robotic. They're not wrong, they're just unmistakably not natural.

The em dash is the punctuation version of that. It's grammatically correct but so overrepresented in AI output that readers have learned to spot it.

## Why it matters

### Brian's specific feedback
> "Can you also update Claude to remove the m dashes from our responses. Whenever I see a m dash, I know it's an AI response."

That's direct. Em dashes are the #1 tell. Brian can instantly clock any FLO output containing them as AI-generated, which undermines the whole point of a warm human-sounding reply.

### The fix
Bake it into the system prompt as a hard rule:

> **PUNCTUATION — CRITICAL:**
> NEVER use em dashes (—) or en dashes (–) anywhere in the reply. These are telltale signs of AI-generated text. Use regular hyphens (-), commas, periods, semicolons, or rewrite the sentence to avoid needing a dash at all.

Claude respects explicit prohibitions in the system prompt reliably. One line blocks every em dash in every future draft.

### Why AI models love em dashes
Training data. Most high-quality written English (essays, journalism, books) uses em dashes liberally for parenthetical asides. When you ask an AI to write in "high-quality prose," it defaults to the style it saw most. Em dashes are a feature of that style — but they're wildly out of proportion compared to casual writing, SMS, and most customer-service replies.

### Other AI tells
- Starting replies with "Certainly!" or "I'd be happy to help with that"
- "Feel free to reach out if..." (ironically, Brian banned this separately)
- "delve into," "leverage," "utilize," "robust"
- Lists that start with "First," "Second," "Third"
- "It's important to note that..."

Every one of these can be rule-banned in the system prompt.

## In simpler terms
It's the Comic Sans of punctuation marks when AI uses it. Technically correct, instantly recognizable, impossible to unsee.
