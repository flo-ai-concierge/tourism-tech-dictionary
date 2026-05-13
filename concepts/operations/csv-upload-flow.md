# CSV Upload Flow

## What it is
A manual data pipeline where a user exports data from one platform as a CSV file, then uploads it to another system which parses and stores it — bridging two platforms that have no direct API connection.

## Plain English
Platform A has the data you need but won't give you an API. So the user logs in, downloads a spreadsheet, and hands it to your system. Your system reads the columns, extracts the numbers, and stores them so the rest of the product can use them as if they came from a live connection.

## Tourism Analogy
Downloading your Airbnb booking history as a spreadsheet and manually importing it into a new property management system. No live sync, but the data gets where it needs to go. It's a workaround — not elegant, but it works on day one with zero extra cost or integration agreements.

## When to use it
- The data source has no API, or API requires a sales process
- The user already has a paid account with export access
- Usage is infrequent enough that manual export isn't painful
- You want to validate the data before investing in a live API connection

## Tradeoffs
| Pros | Cons |
|---|---|
| Zero extra cost | Data goes stale — needs re-export to refresh |
| Works immediately | Requires user action per market |
| Uses existing account | Human error risk (wrong file, wrong filters) |
| Easy to validate | Doesn't scale to many markets |

## FLOHOM implementation plan (Option A)
- Brian exports 7 CSVs per market from AirDNA (ADR, occupancy, revenue, supply, demand, ADR by bedroom, future rates)
- Uploads via a Bridge upload UI (one folder per market)
- Parser auto-detects file type by filename, stores in `navigator_market_data` table
- Market Navigator reads stored data and injects as grounding facts before FLO runs
- Citation shows "AirDNA Research Export · uploaded [date]"

## Superseded by
AirROI API (Option C) — selected May 13, 2026. CSV flow remains as fallback if API data quality is insufficient.

## Learned from
AirDNA → Market Navigator integration design, May 13, 2026
