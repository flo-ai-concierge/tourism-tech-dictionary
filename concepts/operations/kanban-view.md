# Kanban View

## What it is
A UI layout where items move left-to-right across columns representing workflow stages. Each column is a state (e.g., "To Do," "In Progress," "Done") and each item is a card that sits in one column at a time. Originally a physical board from Toyota's factory floor — now a standard pattern for software workflows.

## Tourism translation
The housekeeping board at a hotel. Rooms start in "Dirty," move to "Being Cleaned," move to "Inspection," land in "Ready for Check-in." A glance at the board tells the supervisor how many rooms are in each state, where the bottleneck is, and whether they're on track for the 3pm rush.

Compare to a single list: "Room 412: dirty. Room 203: clean. Room 517: being inspected..." — takes 30 seconds to count how many are ready. The board gives you that answer instantly.

## When you'd see it
- Task trackers (Trello, Jira, Linear)
- Sales pipelines (leads → qualified → proposal → won)
- Content workflows (drafted → edited → published)
- Maintenance tickets (reported → diagnosed → fixed → verified)
- Marina placement: **Active → Approved → In Discussion → Target → Pipeline**

## Why it matters
Humans are good at spatial cognition. A kanban board turns a status field (which requires reading every row) into a picture (which requires glancing). You instantly see:
- Where the volume is (tall columns)
- Where the bottleneck is (one column overflowing)
- What's missing (empty columns)
- What needs attention first (items in the rightmost active column)

## The pattern
```
[ To Do (12) ]  [ In Progress (3) ]  [ Review (5) ]  [ Done (47) ]
  ┌──────┐        ┌──────┐              ┌──────┐       
  │ Card │        │ Card │              │ Card │       
  ├──────┤        ├──────┤              ├──────┤       
  │ Card │        │ Card │              │ Card │       
  └──────┘        └──────┘              └──────┘       
```

Each card carries the minimum info needed to decide what to do next: title, owner, priority, flag. Clicking a card opens the full detail.

## Design principles
- **Column count stays small** (3-6). More columns = harder to fit on screen.
- **Each item lives in exactly one column** — no ambiguity about state.
- **Column headers show the count** so you can see distribution without counting.
- **Limit cards per column if needed** (classic kanban uses WIP limits: "No more than 5 items in In Progress").
- **Sort cards within columns** meaningfully — priority, age, score.

## When NOT to use Kanban
- When items don't have a linear workflow (use tags/filters instead)
- When you have thousands of items per column (use a list + filter)
- When the states aren't mutually exclusive (use multi-select tags)

## Drag-and-drop (optional)
Many kanban boards let you drag cards between columns to change state. Nice UX but adds complexity. Start without it — just click a card to open detail and change status there. Add drag only when users ask for it.

## Learned from
FLOHOM Marina Placement Dashboard Pipeline view (Apr 20, 2026). 226 marinas across 5 statuses. A table view would have required scrolling and sorting by status to see distribution. The kanban layout (Active 7 | Approved 0 | In Discussion 2 | Target 101 | Pipeline 114) instantly shows Brian where the pipeline sits — lots of long-tail pipeline, a concentrated target bucket, seven active placements. Cards sorted by FLOscore descending within each column so the highest-scoring targets bubble to the top.
