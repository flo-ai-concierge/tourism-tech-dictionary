# KML (Keyhole Markup Language)

## What it is
An XML file format for geographic data — specifically, for marking points, lines, and shapes on a map. Originally developed by Keyhole Inc. (the company Google bought to build Google Earth). Now an open standard. When you drop pins in Google Earth or Google My Maps and export, you get a `.kml` file.

## Tourism translation
A travel scrapbook with addresses pinned inside. Your friend hands you a binder: "Here are all my favorite restaurants in Tokyo." Inside, every pin has a name, coordinates, and a little note. You can hand that same binder to someone else and they'll see exactly the same pins in the same places. That portability — one file, everyone sees the same pins — is the whole point of KML.

## When you'd see it
- A stakeholder shares a Google Earth map they've been building for years
- You need to export pins from Google My Maps
- Any GIS (geographic info system) software — they all read KML
- Data migrations from legacy mapping tools

## Why it matters
KML is how you get a human-curated map *out* of Google Earth and *into* your own database. Brian had years of marina pins in Google Earth — 90 locations with real coordinates. Rebuilding that map by hand would have taken hours; parsing the KML took a 30-line function.

## The structure
```xml
<?xml version="1.0" encoding="UTF-8"?>
<kml xmlns="http://www.opengis.net/kml/2.2">
  <Document>
    <name>FLOHOM Marina Locations</name>
    <Placemark id="abc123">
      <name>Liberty Landing Marina</name>
      <description>Suntex-owned, FLO16 placed</description>
      <Point>
        <coordinates>-74.0409,40.7119,1.4</coordinates>
      </Point>
    </Placemark>
    ... more Placemarks ...
  </Document>
</kml>
```

Each `<Placemark>` is one pin. `<coordinates>` is **longitude, latitude, altitude** (yes, longitude first — opposite of the usual lat/lng order). Multiple placemarks stack inside `<Document>`.

## Parsing gotchas
- **Placemark elements can have attributes**: `<Placemark id="abc123">` — your regex `<Placemark>` won't match. Use `<Placemark[^>]*>` or an XML parser.
- **Coordinate order is lng,lat,alt** — not lat,lng. Easy to flip and end up in the ocean.
- **HTML entities in names**: `&apos;` for apostrophes, `&amp;` for ampersands. Decode them before storing.
- **Nested documents/folders**: some KML has `<Folder>` grouping inside `<Document>`. If you care about groups, handle both levels.

## Adjacent formats
- **KMZ** — a zipped KML file. Google Earth often exports this. Unzip to get the raw KML.
- **GeoJSON** — the modern JSON equivalent. More programmer-friendly. Convert KML→GeoJSON with `togeojson` or similar.
- **GPX** — GPS-focused format used by Garmin, Strava, running apps. Same idea, different tags.

## Learned from
FLOHOM Marina Placement Dashboard (Apr 20, 2026). Brian shared his Google Earth map as `FLOHOM Marina Locations.kml` — 90 placemarks covering active FLOHOM boat positions, target marinas, and research candidates. Parsed it with a regex, pulled out 77 new marinas + 6 matches to existing records, populated lat/lng on all of them. Saved us hours of manual geocoding. Watch-out: first regex attempt missed placemarks because I didn't handle the `id="..."` attribute; second attempt missed apostrophes because I didn't decode `&apos;`.
