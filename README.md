# RouteWeather

A drive-route weather planner that checks weather conditions at each waypoint along your route, timed to when you'll actually be there.

## What it does

- Geocodes your origin + destination (via Nominatim/OSM)
- Routes between them (via OSRM open routing)
- Samples N waypoints evenly along the route
- Calculates your ETA at each waypoint
- Pulls an hourly weather forecast for each waypoint at that specific time (Open-Meteo)
- Color-codes conditions: clear / cloudy / rain / storm / snow / fog
- Flags rain-likely and severe weather with alert badges

## Current stack (all free, no keys required)

| Service | Purpose | API |
|---------|---------|-----|
| Nominatim (OSM) | Geocoding addresses | `https://nominatim.openstreetmap.org` |
| OSRM | Driving route + ETA | `https://router.project-osrm.org` |
| Open-Meteo | Hourly weather forecast | `https://api.open-meteo.com` |

Optional: OpenWeatherMap key for richer data (field in UI).

## Why fetches failed in Claude artifact sandbox

Claude.ai's artifact sandbox blocks cross-origin fetch to external APIs (CSP restrictions). This app works correctly when opened as a local HTML file or served from any real host.

## To run locally

```bash
# Option 1 — just open the file
open index.html

# Option 2 — serve locally (avoids any browser fetch quirks)
npx serve .
# or
python3 -m http.server 8080
```

## Build-out roadmap / next steps

### High priority
- [ ] **Google Maps integration** — swap OSRM for Google Directions API for better routing accuracy and real ETA traffic data
- [ ] **Radar overlay** — embed a radar tile layer (RainViewer free API or weather.gov) shown on a map alongside the timeline
- [ ] **Interactive map** — add Leaflet.js or Google Maps embed showing the route with color-coded weather markers at each waypoint
- [ ] **Real-time GPS sync** — on mobile, use `navigator.geolocation` to track current position and highlight the next waypoint

### Medium priority
- [ ] **Push notifications** — alert when approaching a rain/storm zone
- [ ] **Share route** — encode route + departure time in URL params for easy sharing
- [ ] **Saved routes** — localStorage persistence of recent trips
- [ ] **Wind direction** — add wind vector display (matters for cyclists/motorcyclists)
- [ ] **Radar animation** — past-hour radar loop so you can see storm movement

### Nice to have
- [ ] **PWA packaging** — manifest + service worker so it installs on phone home screen
- [ ] **Dark/light theme toggle**
- [ ] **Unit toggle** — °F/°C, mph/km/h
- [ ] **Traffic-aware ETA** — integrate Google Traffic layer for rush-hour accuracy

## File structure

```
route-weather-app/
├── index.html          ← single-file app (all CSS/JS inline)
├── README.md           ← this file
└── PROMPTS.md          ← Claude Code prompts to continue build-out
```

## Key functions in index.html

| Function | Purpose |
|----------|---------|
| `geocode(place)` | Nominatim geocoding |
| `reverseGeocode(lat, lon)` | Label waypoints with city names |
| `getRoute(from, to)` | OSRM routing, returns coords + duration |
| `sampleWaypoints(coords, n)` | Pick N evenly spaced points along route |
| `getWeatherOpenMeteo(lat, lon, time)` | Hourly forecast at specific time |
| `decodeWMO(code)` | WMO weather code → label + icon + CSS class |
| `alertLevel(w)` | Returns danger / warn / watch / null |
| `renderCard(wp, i, total, delay)` | Builds timeline card DOM element |
| `run()` | Main orchestrator |
