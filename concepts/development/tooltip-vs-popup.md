# Tooltip vs Popup

## What it is
Two different UI patterns that look similar but serve different purposes. A **tooltip** is a small hover-only preview showing minimal info. A **popup** is a larger click-triggered panel — can contain actions, forms, links. Choosing the right one matters because using both for the same thing creates redundant, confusing UI.

## Tourism translation
**Tooltip** = the name tag on a staff member's uniform. You glance, you read "Josh — Operations," you move on. You don't interact with the name tag.

**Popup** = pulling Josh aside to have a conversation. "Hey Josh, can you tell me about room 412?" Now you're interacting — you expect a back-and-forth.

If you put the name tag *and* pulled him aside every time someone glanced at his uniform, it'd be exhausting and redundant. That's what a click-triggered popup next to a full-screen drawer with the same data feels like.

## Key differences

| | Tooltip | Popup |
|---|---|---|
| Trigger | Hover (automatic) | Click (intentional) |
| Content | Name, label, short note | Actions, forms, summaries |
| Dismissal | Move mouse away | Click outside or close button |
| Interactivity | None (can't click content) | Clickable (buttons, links) |
| Size | ~100px | ~300px |
| Mental model | "Preview" | "Dialog" |

## When to use which

**Tooltip:**
- Map pins, avatars, icons that benefit from a label on hover
- Truncated text where the full value should appear on hover
- Disabled buttons explaining *why* they're disabled
- Quick glance data

**Popup:**
- Multi-option actions ("Share via email / link / download")
- Filter/search panels attached to a button
- Forms for quick edits without leaving the page
- **Where you'd otherwise need a full modal**

## The redundancy trap
If clicking something *already* triggers a bigger UI (like a side drawer or modal), **don't also show a popup on that same click**. You're showing the user the same information twice in two shapes, with a confusing "Open Details" button in the popup that appears to do nothing because the drawer is already open.

Pick one:
- Hover tooltip + click → drawer (most common pattern)
- Click popup + "Open full details" button → drawer (only if the popup has content that's NOT in the drawer)

## Mobile consideration
Tooltips don't work well on touch — there's no "hover." On mobile, either:
- Show the preview content always (inline, not on hover)
- Use a long-press or tap for the tooltip
- Skip the tooltip entirely and rely on the drawer/popup

## Learned from
FLOHOM Marina Placement Dashboard (Apr 21, 2026). Original design had a Leaflet popup on pin click *and* a side drawer opening at the same time. Both showed the same marina info. The popup had an "Open Details →" link that appeared to do nothing — because the drawer was already open. Pray flagged the confusion. Fix: removed the popup entirely. Pin click → drawer opens. Hover → small tooltip with name, city, and FLOscore. One click, one result. Much cleaner.
