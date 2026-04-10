# Search Query Variations

## What it is
Automatically trying different phrasings of the same search — synonyms, tense changes, name swaps, related terms — to find results that a single exact query would miss. One search call triggers multiple queries behind the scenes and combines the deduplicated results.

## Tourism Translation
**"Searching for a guest named 'Bob Smith' by also checking 'Robert Smith,' 'B. Smith,' and 'Bobby Smith' instead of giving up after one try."**

A guest calls asking about their reservation. They say "Bob Smith." Your system searches and finds nothing. A smart system also tries Robert, Bobby, R. Smith — and finds the booking under "Robert Smith." Same person, different phrasing.

## Why it matters
When Travis asked FLO "when was last pump out Flo 14," the search for "pump out Flo 14" returned noise. But "pumped out Soteria" found it immediately — same data, different words. The smart search now auto-generates variations: property name swaps (Flo 14 to Soteria), tense changes (pump out to pumped out), and related terms (pump out to black tank).
