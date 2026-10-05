# Smart Escape — Interactive Evacuation Route Simulator

A frontend-only web app that imports a local `building.json`, draws the building as an SVG map, and finds the lowest-cost evacuation route to an open exit. Routes recalculate instantly whenever hazards change.

## Features
- Import `building.json` by file picker or drag and drop (read locally, never uploaded)
- Full schema validation with bilingual error messages
- SVG map with weighted corridors, node types, and animated route highlight
- Block/unblock rooms, junctions and corridors; close/reopen exits
- Reset restores the exact `initial_state` of the imported file
- Route summary, step list, total cost, corridor count, live status badge, legend, toasts
- বাংলা / English switch, responsive layout, keyboard-accessible controls

## Run locally
Open `index.html` in a browser. No build step and no dependencies. It also deploys as-is to GitHub Pages, Netlify, Vercel or Cloudflare Pages.

## Import `building.json`
Click **Import building.json** or drop the file onto the dashed panel. **Load Sample Dataset** feeds a built-in sample through the same importer.

## Algorithm
Dijkstra's algorithm on an undirected adjacency list; route cost is the sum of corridor costs (never drawn length). Tie-breaking is deterministic:
1. Lowest total cost.
2. Equal cost: lexicographically smallest exit ID.
3. Equal-cost paths to the same exit: lexicographically smallest node-ID sequence (a second Dijkstra from the exit, then a forward walk choosing the smallest neighbour ID on a shortest path).

## Hazard behavior
- **Blocked node:** cannot be entered or crossed; all its corridors are unusable.
- **Blocked edge:** only that corridor is removed.
- **Closed exit:** never a destination (it may still be physically passed through).
- **Blocked start:** shows "Starting location blocked"; no other start is chosen silently.

## Bangla / English
All UI text, statuses and validation errors are translated. Dataset names and labels are shown unchanged.

## Technologies
HTML, CSS, vanilla JavaScript, SVG. No external dependencies.

## AI tool used
Claude (Anthropic).

## Most useful prompt
The full contest brief: hard constraints, exact hazard rules, exact tie-breaking, required sample checks, and a "no hard-coded routes" requirement.

## Known limitations
- Hazards are edited via the control panel only (no map-click hazard toggling).
- No progress saving, alternative routes, or PNG export.
- The built-in sample is a stand-in matching the contest's expected sample results; judges' own files are handled by the same generic importer.

## Live deployment
https://activecyberguard.github.io/vibe_coding_demo/
