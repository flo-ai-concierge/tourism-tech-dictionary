# Login Wall / Paywall (Scraping Context)

## What it is
When an automated tool (like an AI web search agent) tries to fetch data from a website but gets blocked because the page requires authentication — a login, subscription, or payment — to access the content.

## Plain English
The tool visits the URL, the website says "log in first," and the tool gets nothing useful back. It either returns an error, the login page HTML, or a generic marketing page — not the actual data you need.

## Tourism Analogy
Sending a staff member to research a competitor's pricing, but they can't get in because the front desk requires a reservation number to enter. They come back with nothing useful — just a photo of the lobby door.

## Why it matters for FLOHOM
The Market Navigator was sending FLO Concierge to web-search airdna.co for STR comps and seasonality data. AirDNA requires a paid login — so the tool was hitting the paywall and either guessing or returning generic marketing content. The reports looked weak because the data source was inaccessible.

## The fix
Don't scrape authenticated sources. Instead: either connect via official API (AirROI — selected May 13, 2026), or have the user export data manually (CSV upload flow) and inject it as grounding facts before the AI runs.

## Learned from
AirDNA → Market Navigator integration debugging, May 13, 2026
