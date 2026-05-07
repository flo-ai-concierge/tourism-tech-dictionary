---
term: Checklist Templates
category: development
session: FLOTurn Phase 1 — May 2026
---

## Plain English

Named, reusable task lists that can be applied automatically to new jobs. Instead of storing one flat list of tasks per market, a template system lets you define templates with **dimensions** — like clean type (standard/deep/inspection), property type (1BR/suite), and market — so the right template gets pulled for the right situation.

When a new job is created, the system finds the matching template and copies its tasks into the job's checklist. Changing the template doesn't affect jobs already in progress.

## Tourism / Hospitality Analogy

A hotel's SOP (Standard Operating Procedure) binder. "Standard Turnover — 1BR Suite" has a different checklist than "Deep Clean — Penthouse." Housekeeping supervisors don't rewrite the checklist from scratch each time — they pull the right SOP for the job type and hand it to the cleaner. Updating the SOP binder for the next batch doesn't change what the current crew is working from.

## Technical Detail

In FLOTurn:
```
cleaning_checklist_templates
  id, name, clean_type, property_type, market, is_active

cleaning_checklist_template_tasks
  id, template_id, task, sort_order, is_required, reference_photo_url
```

When a job is created, `instantiateChecklist(jobId, market)`:
1. Finds the active standard template for that market
2. Copies its tasks into `cleaning_tasks` for the job
3. Falls back to legacy `cleaning_checklists` if no template found

The reference_photo_url field lets admins attach a "what good looks like" photo to each task, which cleaners can see when doing the task.

## Dimensions

| Dimension | Values | Purpose |
|---|---|---|
| `clean_type` | standard, deep, inspection | How thorough the clean is |
| `property_type` | 1br, 2br, suite, etc. | Property size affects task list |
| `market` | Baltimore / AAC, Virginia Beach, etc. | Market-specific requirements |
