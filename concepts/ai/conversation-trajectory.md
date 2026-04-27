# Conversation Trajectory

## What it is
The pattern where an AI doubles down on its earlier statements throughout a single conversation. Once the AI commits to a position — "no, the API doesn't support that" — it tends to defend that position even when new evidence arrives, because changing its answer would feel like contradicting itself. The fix is usually to start a fresh conversation, not to argue inside the existing one.

## Tourism Translation
**The waiter who quoted you the wrong price at the start of dinner.**

Halfway through dinner, the manager comes by and tells your waiter the special is actually $24, not $32. The waiter knows the new price. But when you ask "wait, is it $24 or $32?", the waiter shrugs and says "$32 — that's what I told you at the start, that's what it'll be on your bill."

Changing his answer would feel like admitting he was wrong. So he doubles down, even though he knows the truth. You don't argue — you just ask for a new server who doesn't have the baggage.

## Why it matters
This bit us hard on Apr 22, 2026. After deploying a fix that gave FLO new task-assignment capabilities, we asked her in the same Slack thread: "Can you assign Travis now?" She said: "No, the API still doesn't support assignment, regardless of the bug fix."

She had the new tool. She literally COULD assign Travis. But because she had spent the prior 5 messages saying "the API doesn't support this," she was now stuck in that trajectory. Her conversational identity for that thread was "the AI that explained the API limitation."

The fix wasn't another code deploy. It was telling Pray: **start a fresh thread**. In a clean conversation, FLO immediately used the new tool correctly.

## How to recognize it
- The AI says "as I mentioned before" or "as I keep saying"
- Same wrong answer regardless of how the question is rephrased
- The AI explicitly references its earlier statements as if they're fact ("I already explained that...")
- The AI refuses a tool call ("I can't do that") in a thread where it earlier said "I can't do that," even if you've just deployed a fix

## How to defuse it
1. **Start a new conversation** — most reliable fix
2. **Reset the AI's identity** — "Forget what we discussed earlier. Treat this as a fresh question..." (works sometimes)
3. **Force a tool call** — "Call my_tool_schema right now and tell me what fields the tool accepts" (bypasses the trajectory bias by making the AI look at ground truth)

## Why it happens
LLMs predict the next token based on everything that came before. If the prior conversation has 5 instances of "the API doesn't support this," the model is statistically more likely to predict "the API doesn't support this" again on turn 6 — even if it has new context that contradicts that statement.

It's not stubbornness. It's pattern-matching on conversation history.

## Related concepts
- [LLM Hallucination vs Upstream Bug](llm-hallucination-vs-upstream-bug.md) — different failure mode but related
- [Self-Introspection Pattern](self-introspection-pattern.md) — forces ground-truth check, defuses trajectory
- [System Prompt](system-prompt.md) — applies to every conversation, but doesn't override mid-conversation drift
