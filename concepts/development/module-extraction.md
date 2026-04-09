# Module Extraction

## What it is
The process of moving code from one large file into smaller, focused files that each handle one specific job. Each new file (module) exports the functions it provides, and the original file imports from them. Done carefully, the system's behavior doesn't change at all — only the organization improves.

## Tourism Translation
**Hiring specialist staff.** A growing resort starts with a few people doing everything. Module extraction is like restructuring into departments: front desk (check-in/out), housekeeping (room prep), concierge (guest requests), maintenance (repairs), kitchen (food). Each department has clear responsibilities, can be trained independently, and can be evaluated on its own performance. The guest experience stays the same — it just runs smoother behind the scenes.

## When you'll encounter it
- During refactoring of large codebases
- When a file becomes too big to maintain safely
- When you want to test individual pieces of logic in isolation
- When multiple developers need to work on different parts without stepping on each other
