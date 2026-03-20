# Prompt Engineering

## What it is
The practice of writing clear, structured instructions for an AI model to get the best possible output. It's part writing, part engineering, part psychology — figuring out how to communicate with a system that's very capable but needs the right context to perform.

## Tourism Translation
**Writing the perfect property listing + house manual combined.**

A bad listing says "Nice house, great views." A great listing paints the full picture: what makes this property special, who it's perfect for, what to expect, house rules, local tips, how to reach the host. The guest (the AI model) arrives with no prior knowledge of your property — your listing is ALL they have.

Prompt engineering is writing that listing so perfectly that the guest has an amazing experience without ever needing to call you.

## Key principles (from Anthropic's own team)

### 1. The Temp Agency Test
Imagine a competent person shows up from a temp agency. They're smart, they know your industry, but they've never been to your specific hotel. What would you tell them? That's your prompt.

### 2. Don't lie — just describe the real task
Don't say "you are a teacher grading homework" when you actually want it to evaluate data quality. Just say what you actually need. Modern models understand complex tasks directly.

### 3. Give it outs
If something weird happens and the model doesn't know what to do, tell it what to do. "If the input doesn't look like a guest message, respond with UNSURE." Otherwise it'll guess — and guessing in hospitality means a guest gets wrong information.

### 4. Test with messy inputs
Real guests type with no punctuation, misspellings, incomplete sentences. Test your prompts with real-world messy input, not perfect grammar.

### 5. Read the outputs closely
Don't just check if the answer is right. Read HOW it got there. The reasoning reveals what's working and what needs fixing.

### 6. Use the model to fix itself
Give it your prompt and say "don't follow this — tell me what's unclear." When it gets something wrong, ask "why?" and "how would you rewrite my instructions to get this right?"

## Related concepts
- [Tokens and Context Window](./tokens-context-window.md)
- [Chain of Thought](./chain-of-thought.md)
