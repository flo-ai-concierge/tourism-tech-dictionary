---
term: Seed Data
category: development
session: FLOTurn Phase 1 — May 2026
---

## Plain English

Starter data that gets loaded into a new database table during setup so the system is immediately usable — no manual entry required. Usually runs as part of the migration that creates the table. The seed is typically idempotent: it checks "is the table already populated?" before inserting, so running the migration twice doesn't create duplicates.

## Tourism / Hospitality Analogy

Pre-filling a new property management system with standard blackout dates, check-in rules, and cleaning schedules before the first guest books. The property manager doesn't want to hand the system to staff with empty tables — they set up the baseline so the team can work from day one.

## Technical Detail

In migration 044, the template tables were created and immediately seeded from the existing `cleaning_checklists` data:

```sql
-- Only seed if the new table is empty
IF (SELECT COUNT(*) FROM cleaning_checklist_templates) = 0 THEN
  -- Loop over each market that had a checklist
  FOR market_name IN SELECT DISTINCT market FROM cleaning_checklists LOOP
    INSERT INTO cleaning_checklist_templates (name, clean_type, market)
    VALUES (market_name || ' — Standard Turnover', 'standard', market_name);
    -- Copy tasks over
    INSERT INTO cleaning_checklist_template_tasks (template_id, task, sort_order, is_required)
    SELECT tmpl_id, task, sort_order, is_required
    FROM cleaning_checklists WHERE market = market_name;
  END LOOP;
END IF;
```

Result: 4 templates created with 17 tasks each, immediately usable on first deploy.
