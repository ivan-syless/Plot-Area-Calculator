# Plot Area Calculator

A single-page, browser-based tool for sketching an irregular land plot from its side lengths (and, optionally, its corner angles) and instantly seeing the resulting shape, perimeter, and area. Built as one self-contained HTML file — no build step, no dependencies, no backend.

**[Live Demo](#deployment)** · Just open `plot-area-calculator.html` in any modern browser.

## Features

- **3–10 sided polygons** — works for triangles all the way up to irregular decagons.
- **Side-length driven shape** — enter each side's length and the tool solves for a closed polygon that matches.
- **Concave corners** — toggle a corner "inward" per side to model L-shapes and other non-convex boundaries.
- **Optional angle input** — enter a known interior angle at any vertex (e.g. from a survey) for an exact fit; the tool holds that angle fixed and only solves the remaining unknown corners. Angles are shown in a dedicated section labeled `α = ∠ABC`, `β = ∠BCD`, etc.
- **Fix total area** — instead of an exact size, specify a target area and let the tool scale the whole shape (preserving its proportions and angles) to match it exactly. Effective, scaled side lengths are shown alongside your inputs.
- **Live perimeter & area** — computed in real time, with independent unit selectors for length (m, cm, mm, km, ft, in, yd, mi) and area (m², ft², yd², in², km², mi², acre, hectare, cent, and ground).
- **Interactive plot** — drag any labeled vertex to flex the shape while keeping side lengths fixed; scroll/pinch or use the on-screen controls to zoom and pan.
- **Gridded, ruled canvas** — a coordinate grid and ruler give a sense of real-world scale as you work.
- **Sanity checks** — clear warnings for invalid inputs (e.g. non-positive lengths, a triangle that can't close, or a target area that can't be reached).

## Getting Started

No installation required.

1. Download or clone this repository.
2. Open `plot-area-calculator.html` directly in your browser (double-click it, or drag it into a browser window).

That's it — everything (markup, styling, and logic) lives in that one file.

## Usage

1. Set the **number of sides** (3–10) and the **unit** you'll enter lengths in.
2. Fill in a **length** for each side under "Sides & corners." Toggle a corner's switch on if the boundary turns inward there (like the inside corner of an "L").
3. *(Optional)* Turn on **Enable angles** to specify exact interior angles for one or more corners in the new "Angles" section — useful when you have survey data.
4. *(Optional)* Turn on **Fix total area** to scale the whole shape (keeping its proportions) so it matches a target area you enter.
5. Read the **perimeter** and **area** off the results cards, switching units as needed.
6. Drag any vertex on the plot to explore the shape interactively, or use **Reset shape** / **Reset view** to start over.

## How It Works

Given the side lengths and any concave/angle constraints, the app treats each corner's turn angle as an unknown and solves a small nonlinear system (via Gauss–Newton iteration) so the polygon closes into a simple loop with interior angles summing correctly. Any angle you enter explicitly is held fixed rather than optimized, so it's respected exactly in the final shape. Area and perimeter are then computed directly from the solved vertex coordinates (shoelace formula for area). When "Fix total area" is enabled, the solved shape is scaled uniformly by `sqrt(targetArea / currentArea)` so it hits the requested area while preserving all angles and proportions.

## Tech Stack

- Plain **HTML**, **CSS**, and **vanilla JavaScript** (no frameworks, no build tools)
- Inline **SVG** for the plot, grid, and rulers
- Runs entirely client-side — nothing is sent to a server

## Deployment

This is a static, single-file site, so it works out of the box with **GitHub Pages**:

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under "Build and deployment," set **Source** to "Deploy from a branch," pick your default branch and the `/ (root)` folder.
4. Save — GitHub will publish the site at `https://<your-username>.github.io/<repo-name>/plot-area-calculator.html`.

   (Optional: rename `plot-area-calculator.html` to `index.html` so it's served at the repo's root URL instead.)

## Browser Support

Works in any modern evergreen browser (Chrome, Firefox, Safari, Edge). Requires JavaScript enabled.

## License

Add a license of your choice (e.g. MIT) before publishing, if you'd like others to be able to reuse this freely.

## Contributing

Issues and pull requests are welcome — this is a small, single-file project, so most changes will touch `plot-area-calculator.html` directly.
