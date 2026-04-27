# Self-Introspection Pattern (my_tool_schema)

## What it is
A meta-tool that lets an AI inspect its own toolbox. Instead of guessing what fields a tool accepts, the AI calls `my_tool_schema(toolName)` and gets back the exact list of accepted fields, types, and required-vs-optional flags. Pairs with a system prompt rule that forces the AI to call it before claiming external limitations.

## Tourism Translation
**Before telling a guest "we don't offer airport pickup," the front desk actually checks the services binder.**

A great clerk doesn't guess what the property offers. When a guest asks something unusual — "do you have child seats? cribs? a portable grill?" — the clerk pulls out the services binder and looks. If it's there, great. If it's not, they say "we don't offer that, but I can flag it to the manager to add."

Self-introspection is giving the AI that binder. Without it, the AI just makes up confident answers based on what feels right. With it, the AI reads its actual capabilities before responding.

## Why it matters
Modern AI assistants have dozens of tools. The AI sees them as a list of names and descriptions, but it doesn't always remember the exact field-level details. When asked "can you set X?", the AI's instinct is to answer from memory — and memory is fuzzy. It might confidently say "no, that's not supported" when the field is actually right there in the tool schema.

The fix: turn introspection into a tool the AI can call. Now the AI doesn't have to remember — it can look up the truth in real time.

## How it works in FLOHOM
The `my_tool_schema` tool was added to FLO's toolbox on Apr 22, 2026 after FLO falsely claimed Hostaway's API didn't support task assignment.

```
Input:  my_tool_schema(toolName: "create_hostaway_task")
Output: {
  tool_name: "create_hostaway_task",
  accepted_fields: [
    { field: "title", type: "string", required: true, ... },
    { field: "assigneeUserId", type: "number", required: false, ... },
    { field: "supervisorUserId", type: "number", required: false, ... },
    ...
  ],
  required_fields: ["title"],
  self_diagnosis_note: "If a user wants to pass a field that's NOT in accepted_fields, this is a TOOL-DEFINITION gap, not an external-API limitation."
}
```

The tool was added to the **ALWAYS_TOOLS tier** so it loads in every conversation — without that, the tool tiering would filter it out and FLO couldn't call it when she needed it most.

## Why it must be in ALWAYS tier
Tool tiering normally loads only context-relevant tools per request. If `my_tool_schema` were in a "self-awareness" or "rare" tier, FLO wouldn't have access to it during a guest conversation about task assignment — exactly the moment when she needs to verify her capabilities. ALWAYS tier costs ~200 extra tokens per request, well worth the trade.

## Related concepts
- [Tool-Gap vs API-Limitation](tool-gap-vs-api-limitation.md) — the diagnostic this tool enables
- [Tool Tiering](tool-tiering.md) — why ALWAYS-tier placement matters
- [System Prompt](system-prompt.md) — the rule that forces the AI to actually use this tool
