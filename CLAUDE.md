# RouteWeather

Drive-route weather planner — check weather at each waypoint along your route, timed to your actual arrival.

## Product

- **Free tier**: full core functionality, shows Google AdSense banner ads
- **Pro tier**: paid ($4.99/mo or $39/yr), removes ads, unlocks: saved routes, more waypoints (up to 20), URL sharing, offline PWA

## Stack (target)

- **Frontend**: React + Vite (currently single HTML file — refactor is Phase 2)
- **Backend**: Cloudflare Workers or Vercel Edge (lightweight — just auth + subscription check)
- **Auth**: Clerk or Supabase Auth (social login, no password friction)
- **Payments**: Stripe (subscriptions) or Lemon Squeezy (simpler)
- **Hosting**: Vercel (free tier deploys from GitHub)
- **Ads**: Google AdSense (free tier only)
- **APIs used** (all free, no keys for core):
  - Nominatim/OSM — geocoding
  - OSRM — driving routing
  - Open-Meteo — hourly weather
  - RainViewer — live radar overlay
  - Optional: Google Maps Directions (traffic-aware ETA)

## File structure (current — single HTML)

```
route-weather/
├── index.html        ← working single-file app
├── README.md
├── PROMPTS.md        ← Claude Code build prompts
├── CLAUDE.md         ← this file
└── docs/
    └── MVP.md        ← product roadmap
```

## Build phases

See `docs/MVP.md` for the phased roadmap.

## Key rules

- Free tier never gets gated on core features (routing + weather) — only extras
- Never hardcode API keys; use env vars
- No backend required for Phase 0–1 (pure static)
- Phase 2+ adds a thin backend only for auth + subscription status

## Commands (Phase 2+, after React refactor)

```bash
npm run dev      # Vite dev server
npm run build    # production build
npm run preview  # preview build
```
