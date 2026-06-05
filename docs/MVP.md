# RouteWeather — MVP Roadmap

> A standalone marketable drive-route weather planner.
> Free (ads) + Pro ($4.99/mo, no ads + extras).

---

## Phase 0 — Ship the current app (this week)

**Goal:** Get something live with ads before writing new code.

- [ ] Deploy `index.html` to Vercel or Netlify (zero config — just drag the folder)
- [ ] Register a domain: `routeweather.app` or `routeweather.io` (~$12/yr on GoDaddy)
- [ ] Add Google AdSense banner (one banner below the route bar — non-intrusive)
- [ ] Add a simple "Go Pro — remove ads" CTA button that links to a waitlist (Typeform or Tally.so)
- [ ] Add URL params for route sharing (`?from=Austin,TX&to=Houston,TX&depart=...`)
- [ ] Set up Google Analytics (free, single script tag)

**Exit criteria:** Live URL, real ads loading, sharing link works, first 10 visitors.

---

## Phase 1 — Leaflet map + radar (week 2)

**Goal:** Visually compelling — a map makes it shareable and screenshot-able.

- [ ] Add Leaflet.js map above the timeline (CDN, no build step needed)
- [ ] Draw the driving route as a polyline
- [ ] Place colored weather markers at each waypoint (green=clear, blue=rain, red=storm)
- [ ] Add RainViewer live radar overlay tile layer (free API, toggle button)
- [ ] Refine mobile layout (stack map above cards on small screens)
- [ ] Add "Copy share link" button + toast notification
- [ ] Add "Driving conditions" summary per card: Excellent / Good / Caution / Dangerous

**Exit criteria:** Route on a map with radar, shareable link, looks good on mobile.

---

## Phase 2 — PWA + offline (week 3–4)

**Goal:** Install on phone home screen, works without signal.

- [ ] Add `manifest.json` (name, icons, theme, display:standalone)
- [ ] Add service worker (cache app shell + recent weather responses)
- [ ] Create SVG app icon (192×192, 512×512)
- [ ] Add "Install app" prompt
- [ ] Saved routes via localStorage (store last 5 routes)
- [ ] Unit toggle: °F/°C, mph/km/h (localStorage preference)
- [ ] Wind direction display (cardinal: N, NE, SE...)

**Exit criteria:** Installs on Android/iOS from browser, works offline for recent routes.

---

## Phase 3 — Monetization wiring (week 4–5)

**Goal:** Actual Pro subscriptions flowing.

### Architecture (keep it simple)
- **No backend initially** — use Lemon Squeezy's hosted checkout + license key approach
- After payment, user gets a license key → enter it in the app → stored in localStorage
- Pro status check: `localStorage.getItem('routeWeatherPro') === 'valid'`
- This is good enough until you have real user scale (~100+ paying users)

### Free vs Pro gates
| Feature | Free | Pro |
|---------|------|-----|
| Core routing + weather | ✓ | ✓ |
| Waypoints | up to 8 | up to 20 |
| Ads | 1 banner | None |
| Saved routes | 0 | Up to 20 |
| URL sharing | ✓ | ✓ |
| Offline PWA | ✓ | ✓ |
| Live GPS tracking | — | ✓ |
| Advanced wind/UV data | — | ✓ |

### Tasks
- [ ] Set up Lemon Squeezy product ($4.99/mo, $39/yr)
- [ ] Add license key entry modal in app
- [ ] Implement Pro gate logic in JS (localStorage key check)
- [ ] Update AdSense to only load for non-Pro users
- [ ] Add Pro landing section / pricing page (can be bottom of app page)
- [ ] Set up email capture (Mailchimp or ConvertKit free tier) for announcements

**Exit criteria:** Someone can pay $4.99, get a key, enter it, and ads disappear.

---

## Phase 4 — React refactor + real backend (month 2)

**Goal:** Proper codebase ready for bigger features.

- [ ] Migrate to React + Vite
- [ ] Component structure: `RouteForm`, `MapView`, `WeatherTimeline`, `WaypointCard`
- [ ] API layer: `src/api/geocode.js`, `route.js`, `weather.js`
- [ ] Add Clerk or Supabase Auth (social login)
- [ ] Replace license key approach with server-side subscription check (Stripe + Cloudflare Worker)
- [ ] Google Maps Directions API fallback (traffic-aware ETA)

---

## Phase 5 — Growth features (month 3+)

- [ ] Live GPS "Track my drive" mode (geolocation, highlight next waypoint, "you are here" marker)
- [ ] Push notifications when approaching rain/storm zone
- [ ] Radar animation (past 6 frames loop)
- [ ] Multiple route stops (A→B→C→D)
- [ ] Public route gallery / popular routes
- [ ] React Native / Expo mobile app (reuse the API layer)

---

## Revenue model

| Tier | Price | Features |
|------|-------|----------|
| Free | $0 | Full core, 1 AdSense banner, up to 8 waypoints |
| Pro | $4.99/mo or $39/yr | No ads, 20 waypoints, saved routes, GPS tracking, advanced data |

**Target:** 1,000 free users → 2% conversion → 20 Pro users → ~$100/mo. 
Scale: 10k free, 5% → 500 Pro → ~$2,500/mo. All free APIs until serious scale.

---

## Domain + branding

**Recommended name:** `routeweather.app`  
**Tagline:** *Know the weather before you hit the road.*  
**Logo:** Map pin + cloud icon, dark theme (matches existing design)

---

## First 3 actions right now

1. `git init` + push to GitHub (public repo — builds trust/SEO)
2. Connect repo to Vercel → live in 2 minutes
3. Register `routeweather.app` on GoDaddy or Namecheap
