# Tool Tiering

## What it is
Loading only the tools an AI assistant needs for a specific request, instead of giving it every tool every time. With 40+ tools, sending all of them on every request burns context tokens and can confuse the model. Tiering filters down to what's relevant — usually a small "always loaded" set plus context-specific specialist groups.

Different from [classification-tiers](classification-tiers.md), which routes incoming MESSAGES to different brains. Tool tiering decides which TOOLS the brain has access to once the message has been routed.

## Tourism Translation
**The morning shift cleaner doesn't carry every tool in the property.**

A housekeeper preparing for the 9 AM turn doesn't carry the full maintenance toolkit, the marina key fobs, the upsell-display materials, the pet-cleanup supplies, AND the extra linen cart. She carries:

- **Always**: vacuum, cleaning chemicals, gloves, trash bags (every room needs these)
- **Sometimes**: pet-stain enzymes (only if guest had a pet), extra linens (only if it's a 4-guest unit)
- **Rarely**: maintenance tools (only if a work order is queued)

The cart is lighter, she moves faster, and she's not constantly rummaging through irrelevant gear. The "always" set is small. The "sometimes" set loads based on the property's specifics.

## Why it matters
LLMs have a context window — a maximum amount of text they can process per request. Every tool definition you include eats into that window. With 40+ FLOHOM tools, sending all of them costs ~6,000 tokens before the conversation even starts. That's expensive AND it dilutes the AI's attention.

But cut too many tools and the AI fails: "I don't have a my_tool_schema tool" — even though it exists in the codebase, because the router filtered it out before the AI saw it.

The trick is finding the right tier for each tool.

## How it works in FLOHOM
Three tiers (`floAgent.js:5000`):

1. **ALWAYS_TOOLS** (~12 tools) — loaded on every conversation:
   - get_property_knowledge, check_availability, generate_booking_link, escalate_to_human, my_tool_schema, etc.
2. **SPECIALIST_GROUPS** (~14 tools, grouped) — loaded based on keywords in the recent conversation:
   - "task" / "assign" / "fix" → loads task tools
   - "guest" / "stayed before" → loads guest intel tools
   - "propane" / "tank" → loads field ops tools
3. **RARELY_TOOLS** (~15 tools) — only loaded for internal/team channels:
   - log_finding, save_to_knowledge_base, slack search, etc.

For internal sources (Eye, Autonomous, briefings) — full toolset, no restrictions.

## The trap we fell into
On Apr 22, 2026 we added `my_tool_schema` to FLO_TOOLS but forgot to add it to any tier in the router. Result: FLO loaded it in `FLO_TOOLS` array but the router filtered it out before sending to Claude. FLO honestly answered "I don't have that tool" — and we spent 30 minutes debugging the deploy before realizing the issue was in the tier list, not the deploy.

**Lesson**: any new tool MUST also be added to a tier. The router is invisible to the AI.

## Related concepts
- [Classification Tiers](classification-tiers.md) — sister concept, routes messages instead of tools
- [Self-Introspection Pattern](self-introspection-pattern.md) — example of a tool that MUST be in ALWAYS tier
- [Context Injection](context-injection.md) — different optimization, same goal of keeping context lean
