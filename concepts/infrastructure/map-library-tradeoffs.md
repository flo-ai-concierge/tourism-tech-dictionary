# Map Library Trade-offs (Mapbox vs Leaflet)

## What it is
The choice between two dominant JavaScript libraries for rendering interactive maps. **Mapbox GL JS** is the premium option — vector tiles, customizable themes, professional polish. **Leaflet** is the open-source workhorse — simpler, free, proven. The right pick depends on setup friction, aesthetics, and scale needs.

## Tourism translation
**Mapbox** is hiring a high-end travel concierge agency. Polished service, stunning branded tours, deep customization — but you need to sign up for an account, give them a credit card, and manage an API key before they'll lift a finger.

**Leaflet + free tiles (like CartoDB)** is the public tourist info kiosk. Free to use, no paperwork, pretty good maps. You don't get the boutique styling but you're up and running in 5 minutes.

## When you'd use Mapbox GL JS
- You want a distinctive branded aesthetic (custom colors, fonts, layers)
- You need smooth 3D tilted views, vector scaling, or complex data overlays
- You're building a map-heavy product (not just a side feature)
- Enterprise deployment with 50k+ map loads/month (paid tier)
- Someone on the team is already willing to own the Mapbox account

## When you'd use Leaflet
- Map is a feature, not the product
- You want to ship tonight without a signup flow
- Free-tier friendliness matters more than polish
- You'll swap tile providers later if needed
- The sandboxed preview environment blocks external image CDNs (you control the setup)

## The tile-provider layer
Both libraries render *tiles* — pre-rendered map images loaded from a CDN. You can mix and match:
- **Mapbox Studio tiles** — high quality, requires Mapbox account
- **CartoDB Dark Matter / Positron** — free, professional-looking, no account
- **OpenStreetMap standard** — free, utilitarian look
- **Stadia Maps** — free for dev, paid for prod, beautiful options
- **Self-hosted** — if you want full control (rare)

You can use **Leaflet as the library + Mapbox tiles** — library and tiles are decoupled.

## Cost comparison (rough, April 2026)
- **Mapbox**: 50k map loads/month free, then $0.50-$5.00 per 1k loads depending on features
- **Leaflet + CartoDB**: Free for most use (attribution required)
- **Leaflet + OSM**: Free but has a tile usage policy; fine for moderate traffic
- **Stadia**: Free tier exists; paid is competitively priced

## Setup friction
- **Mapbox**: Create account → verify email → create token → add to env vars → deploy → hope CSP allows the domain → test
- **Leaflet + CartoDB**: `npm install leaflet react-leaflet` → import → render → done

For a prototype or v1, the friction delta matters.

## Aesthetic notes
- Mapbox Dark v11 is stunning — crisp labels, smooth vector rendering at all zooms
- CartoDB Dark Matter is very close on aesthetics — almost indistinguishable at typical dashboard zoom
- The difference is more visible when you zoom deep into a city (Mapbox stays sharp; raster tiles pixelate)

## Learned from
FLOHOM Marina Placement Dashboard (Apr 20-21, 2026). Started with Mapbox GL JS because Pray wanted "the best looking map." Built the whole map view, then realized we'd need to create a Mapbox account, verify email, copy a token — friction Pray couldn't complete that night (and ideally shouldn't have to for a prototype). Pivoted to Leaflet + CartoDB Dark Matter tiles (already installed via `leaflet` and `react-leaflet` dependencies). Swap took 15 minutes. Aesthetic gap: small. Setup gap: huge. The right call for a shipping-tonight situation; we can revisit Mapbox later if Brian wants the extra polish.
