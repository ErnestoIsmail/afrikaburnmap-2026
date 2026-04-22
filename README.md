# AfrikaBurn 2026 interactive map

An offline-friendly interactive fork of the AfrikaBurn 2026 map, built for use before and during the burn.

This version extends the original interactive map with richer camp, artwork, mutant vehicle, and OCC detail; a linked burn schedule; live location tools; personal event tracking; and additional on-burn navigation helpers.

**Live:** https://chrislaidler.github.io/afrikaburnmap-2026/

**Original project:** https://bernardbravenboer.github.io/afrikaburnmap-2026/

## What this version adds

- Detailed info panels for theme camps, artworks, OCC locations, mutant vehicles, support camps, plazas, and toilets
- Search across map items, tags, and schedule events
- Search result list with direct jump-to-item behavior
- Linked-item buttons in details, so related camps, artworks, and support camps can jump to one another
- Burn schedule with:
  - agenda view
  - timeline view
  - day navigation across the 2026 burn week
  - event / open-time filtering
  - category filters
  - starred events
  - custom personal events
- Live GPS position on the map when geolocation is available and within the registered map area
- Optional heading indicator when the phone provides orientation data
- Recent movement trail for the live position marker
- Quick actions from current location:
  - `Find a toilet`
  - `Close event`
- Seen / Visited tracking for artworks and camps, including visible check marks in the map index
- Offline install support through a service worker and web app manifest
- About panel with source links, caveats, and version / cache information

## Main user-facing behavior

### Map interaction

- Pan and zoom the map on desktop and mobile
- Switch between standard and high-resolution map modes
- Keep the selected details panel open while panning and zooming
- Use browser back to unwind map click-throughs and panel state

### Details and linked navigation

- Tap or click a camp, artwork, mutant vehicle, OCC location, support camp, plaza, or toilet to open its info panel
- Related items can be opened directly from the details header
- Tags in the details panel act as search shortcuts
- Items with associated schedule entries show a linked `Schedule` section

### Schedule

- Burn-week schedule for the 2026 event dates
- Timeline and agenda views
- Day pills, previous / next navigation, and `Today`
- Event categories such as:
  - Burn
  - Music
  - Performance
  - Workshop
  - Wellness
  - Food & Drink
  - Service
  - Movement
  - Community
- Star items for later
- Add your own custom events locally in the browser
- Link custom events back to camps or artworks using the same ranked search logic as the main search

### GPS and local guidance

- Show current map position when geolocation is available
- Draw route hints to nearby toilets
- Draw route hints to nearby active or about-to-start events
- Mark camps as `Visited` and artworks as `Seen` when physically close enough

## Data sources

This fork is built from:

- the official AfrikaBurn 2026 site map
- the official 2026 WTF Guide
- additional structured schedule extraction
- manual cleanup and linking across camps, artworks, support camps, OCC sites, and events

The app intentionally treats some schedule information as approximate. Some entries are fixed-time events, some are open hours, and some are estimated from phrases like `late`, `sunset`, or `after dark`.

## Project structure

This is still a static site. There is no framework or build step.

Main files:

- `index.html` — UI, interaction logic, schedule rendering, GPS tools, local persistence
- `data.js` — hotspot geometry and base map item placement
- `project_details.js` — enriched blurbs and linked metadata for camps, art, OCC, mutant vehicles, and support camps
- `schedule_data.js` — structured burn schedule data
- `sw.js` — offline cache
- `manifest.json` — install metadata

Map assets:

- `2026_AfrikaBurnMap-scaled.jpg`
- `2026_Site_map_highres.jpg`
- `2026_Site_map_highres_mobile.jpg`
- `2026_Site_map_highres_overview.jpg`
- `2026_Site_map_highres_tiny.jpg`

Reference/source material:

- `WTF- 2026 - Through The Prism.pdf`
- `2026_copy_theme.txt`
- `2026_copy_art.txt`
- `2026_copy_occ.txt`
- `2026_copy_mutans.txt`

## Running locally

Use a local web server. That is the correct way to test:

- service worker caching
- install / save-for-offline prompts
- manifest behavior
- same-origin asset loading

```bash
git clone https://github.com/ChrisLaidler/afrikaburnmap-2026.git
cd afrikaburnmap-2026
python3 -m http.server 8000
```

Then open:

```text
http://localhost:8000/
```

Opening `index.html` directly via `file://` is not a good test path for offline or install behavior.

## Updating content

Typical content changes land in one of these places:

- `project_details.js`
  - update camp / artwork / OCC blurbs
  - add linked items
  - improve descriptive copy
- `schedule_data.js`
  - add or adjust events
  - fix times
  - add categories
  - link events to map codes
- `data.js`
  - adjust hotspot positions
  - fix map geometry
  - update regions / labels / placements
- `sw.js`
  - bump `CACHE_VERSION` whenever cached assets change

If you change content that is cached by the service worker, bump the cache version in `sw.js` so returning users pick up the new bundle cleanly.

## Personal data and persistence

This app stores personal state locally in the browser, including things like:

- starred schedule items
- custom events
- seen / visited state
- some local UI preferences

That data is local to the current browser and site origin. It will not automatically carry across:

- different browsers
- private browsing windows
- cleared site data
- different hosts or URLs

Offline use works as long as the app bundle has already been cached on that device.

## Credits

- Official map and WTF content: AfrikaBurn
- Original interactive map: Bernard
- This fork and ongoing community-focused updates: Chris Laidler / Greasemonkeys

## Disclaimer

This is an independent helper tool and is not an official AfrikaBurn product.

Locations, schedules, and linked details may be incomplete, approximate, or wrong. Conditions at the burn can and do change. Reality sometimes overwrites the map.

Use the map as a helper, not as the entire experience.
