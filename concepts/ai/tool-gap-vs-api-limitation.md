# Tool-Gap vs API-Limitation

## What it is
Two different reasons an AI assistant says "I can't do that" — with two completely different fixes. **Tool-gap** = the AI's own tool definition doesn't accept the field (your engineering team adds it in minutes). **API-limitation** = the external service doesn't accept the field (you contact the vendor or architect around it). AIs frequently confuse the two and confidently blame the external API when the gap is actually in their own toolbox.

## Tourism Translation
**"We don't take bookings after 8 PM."**

When the front desk says that, you need to know: is it OUR system that shuts off at 8, or did the OTA cut us off? Two different fixes:

- **OUR system shut off** (= tool-gap) — IT can flip a setting tomorrow morning. Five minutes.
- **OTA cut us off** (= API-limitation) — call the OTA account manager, escalate, maybe a contract change. Could take weeks.

If the front desk confidently says "the OTA cut us off" without checking, and you spend a week on the phone with the OTA only to discover it was actually our internal system the whole time, you've wasted a week.

## Why it matters
This was the entire root cause of the FLO task assignment incident on Apr 22, 2026. FLO told Travis "Hostaway's API doesn't support assigning tasks to specific users." That sent everyone down the wrong path — engineering started thinking about Slack DM workarounds, vendor escalations, account tier upgrades.

The truth: Hostaway's API supports it perfectly. FLO's `create_hostaway_task` tool just didn't include `assigneeUserId` in its schema. Five-minute fix in our own code.

When AI confidently states an external limitation, **it costs the team real hours chasing the wrong problem**.

## How to fix it (the FLOHOM pattern)
Two layers:

1. **Build a `my_tool_schema` introspection tool** — give the AI a way to look at its own toolbox. When asked "can you do X?", it should call `my_tool_schema(toolName)` and check whether the field is in `accepted_fields` before answering.

2. **System prompt rule** — make it mandatory:
   > "Before claiming an external API doesn't support a feature, you MUST call my_tool_schema first. If your tool doesn't accept the field, that's a TOOL-GAP (Pray adds it in minutes). If your tool sends the field but the API rejects it, that's an API-LIMITATION."

Without the rule + the tool, the AI guesses. With them, the AI says: "My current tool doesn't accept assigneeUserId — flagging for Pray to add it. Hostaway itself probably supports this, I just can't pass it through."

## Related concepts
- [Self-Introspection Pattern (my_tool_schema)](self-introspection-pattern.md) — the tool that makes this diagnosis possible
- [LLM Hallucination vs Upstream Bug](llm-hallucination-vs-upstream-bug.md) — broader pattern of misattributing AI errors
- [System Prompt](system-prompt.md) — where the diagnosis rule lives
