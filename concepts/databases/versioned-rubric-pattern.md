# Versioned Rubric Pattern

## What it is
An architectural pattern where you store the *scoring system* separately from the *scores* — and the scoring system itself has versions. When someone updates the rubric, the old version stays, old scores stay tagged to it, and new scores are tagged to the new version.

## Tourism translation
Updating the star-rating criteria for hotels. If last year's 5-star rubric required 300 sqft rooms and this year requires 400 sqft, you don't retroactively downgrade every 5-star hotel from last year. You tag their score as "5-star (2024 criteria)" and start evaluating new hotels against "5-star (2025 criteria)." A guest comparing hotels can then see which rubric each score was earned against.

## When you'd see it
- Any scoring, grading, or evaluation system that evolves over time
- Compliance checklists that change year-to-year
- AI model evaluations where your grading standards tighten
- Performance reviews where the competency framework changes

## Why it matters
Without versioning, updating your rubric **silently invalidates every past score** — or forces you to re-score everything from scratch every time. With versioning, you evolve the rubric confidently because historical scores stay meaningful and comparable *within their version*.

## The schema
```sql
-- The rubric itself (attributes + max points)
CREATE TABLE rubrics (
  id SERIAL PRIMARY KEY,
  version TEXT UNIQUE NOT NULL,       -- 'v1', 'v2', 'v3'
  name TEXT NOT NULL,
  attributes JSONB NOT NULL,           -- the actual questions + weights
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMPTZ DEFAULT NOW()
);

-- Per-thing scores, each tagged to a rubric version
CREATE TABLE results (
  id SERIAL PRIMARY KEY,
  subject_id INT,                      -- the marina, property, employee, etc.
  rubric_id INT REFERENCES rubrics(id),
  scores JSONB NOT NULL,               -- the actual answers
  total_score INT,
  scored_by TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## Why the rubric goes in JSONB
The shape of a rubric — which attributes, what labels, what max points — is exactly the kind of thing you want to evolve without DB migrations. JSONB lets v2 have 20 attributes when v1 had 18, without touching the `results` table.

## Gotchas
- Your UI needs to render scores against the *specific rubric they were scored against*, not always the latest. Load the rubric by `rubric_id` every time.
- Don't let anyone edit an already-used rubric version — fork it into a new version instead. Editing would retroactively change the meaning of existing scores.

## Learned from
FLOHOM FLOscore system (Apr 20, 2026). Brian had an 18-attribute marina rubric from 2 years ago he called outdated. Instead of asking him to approve scores under the old rubric, we preserved his historical 12 scores as "FLOscore v1 (Legacy)" and built the schema to accept v2 when he updates the rubric. His old scores stay valid under v1; new scores use v2; the radar chart renders each against its own rubric's max points.
