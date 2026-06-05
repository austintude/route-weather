# Claude Code Prompts — RouteWeather Build-out

Use these prompts in Claude Code to continue development. Run them in order or pick the ones you need.

---

## 1. Add Leaflet map with route + weather markers

```
Add an interactive map to index.html using Leaflet.js (CDN).
- Show the driving route as a polyline
- Place a marker at each waypoint with a popup showing temp, condition, and ETA
- Color each marker by condition: green=clear, blue=rain, red=storm, gray=clouds
- Map should render above the timeline cards
- Keep all existing functionality intact
```

---

## 2. Add RainViewer radar overlay

```
Add a live radar tile overlay to the Leaflet map using the RainViewer API.
- Fetch the latest radar frame timestamp from https://api.rainviewer.com/public/weather-maps.json
- Add it as a tile layer on the map with ~50% opacity
- Add a toggle button to show/hide radar
- Show a timestamp for when the radar frame is from
```

---

## 3. Add Google Maps / Directions API support

```
Add optional Google Maps Directions API support to index.html.
- Add a Google Maps API key field in the settings area (store in localStorage)
- When a key is present, use the Directions API instead of OSRM for routing
- Fall back to OSRM if no key is provided
- Use traffic-aware duration_in_traffic for ETA calculations when possible
- Keep the existing UI and timeline rendering unchanged
```

---

## 4. Convert to PWA

```
Convert index.html into a PWA so it can be installed on a phone home screen.
- Create a manifest.json with name, icons, theme color, display: standalone
- Create a service-worker.js that caches the app shell and API responses
- Add the manifest link and service worker registration to index.html
- Create a simple 192x192 and 512x512 SVG icon for the app
- Make sure it works offline for recently fetched routes
```

---

## 5. Add live GPS tracking (mobile)

```
Add a "Track my drive" mode to index.html using the browser Geolocation API.
- Button to start GPS tracking
- Poll navigator.geolocation every 30 seconds
- Highlight the next upcoming waypoint on the timeline
- Show distance and ETA to next waypoint
- Show a "you are here" marker on the map
- Stop tracking button
```

---

## 6. Add URL sharing

```
Add route sharing via URL params to index.html.
- When a route is loaded, update the URL with ?from=...&to=...&depart=...&density=...
- On page load, read those params and auto-populate the form
- Add a "Copy link" button that copies the current URL to clipboard
- Show a toast notification when copied
```

---

## 7. Refactor to React + Vite

```
Refactor this single-file app into a React + Vite project.
- Create a proper Vite project structure
- Extract each major piece into components:
  - <RouteForm /> — input card
  - <RouteBar /> — summary stats
  - <WeatherTimeline /> — the list of cards  
  - <WaypointCard /> — individual card
  - <MapView /> — Leaflet map
- Move API calls into a /src/api/ directory (geocode.js, route.js, weather.js)
- Use useState and useEffect appropriately
- Keep all existing functionality and visual design
```

---

## 8. Add wind + severe weather details

```
Enhance the weather data shown in each waypoint card.
- Add wind direction (cardinal: N, NE, SE etc) alongside wind speed
- Add UV index for daytime waypoints
- Add visibility distance
- If precipitation > 0, show estimated accumulation
- Add a "driving conditions" summary label: Excellent / Good / Caution / Dangerous
  based on a combination of wind speed, precipitation, and weather code
- Color the card left border by driving conditions severity
```
