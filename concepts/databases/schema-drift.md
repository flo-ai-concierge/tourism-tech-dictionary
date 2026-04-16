# Schema Drift

## What it is
When the database schema definition file (the "blueprint") says a column or table exists, but the actual production database doesn't have it. This happens when someone adds a column to the schema file but never runs the migration on the live database. Code that references the missing column crashes at runtime.

## Tourism translation
Like when the property blueprint shows a room has a TV mounted on the wall, but nobody actually installed one during construction. The guidebook tells guests to use the TV, but there's nothing there. The blueprint lied.

## When you'd see it
- "column X does not exist" errors that work fine locally but crash in production
- Features that worked in development but fail after deployment
- Schema files that have been updated but the production DB hasn't been altered

## How to prevent it
Use a migration system (not raw SQL files) so schema changes are tracked and applied consistently. Or at minimum, always run ALTER TABLE on production whenever you update the schema file.

## Learned from
Voicemail insert failed on production (Apr 16, 2026) with "column meta_attachment_type does not exist" — the column was in schema-pg.sql but never added to the Render production database.
