# National PV Roof Database — 7-slide presentation

Interactive web presentation of the geospatial workflow that builds a national
photovoltaic-panel database from open public data (LiDAR HD, cadastre, ortho).

The site is fully self-contained — no third-party CDN calls at runtime.

```
.
├── index.html              entry point — 7 scroll-snap slides
├── viewer-tiles.html       embedded · live map of LiDAR roof regions
├── viewer-panels.html      embedded · live map of the panel database
├── .nojekyll               disables Jekyll on GitHub Pages
├── data/
│   ├── tiles/              13 sample tile JSONs from dépt 82
│   ├── panels__82.geojson  full panel polygons, dépt 82 (15 MB)
│   └── panels__82.csv      panel attributes, dépt 82 (851 KB · 5 058 rows)
└── vendor/
    ├── chart.umd.min.js    Chart.js 4.4.1
    ├── katex/              KaTeX 0.16.9 (CSS, JS, woff2 fonts)
    ├── maplibre/           MapLibre GL 4.1.0 (CSS, JS) — used by the viewers
    ├── proj4.min.js        proj4js 2.9.2 — Lambert-93 ⇄ WGS-84
    ├── tailwind.min.js     Tailwind runtime — used inside the viewers
    └── fonts/              Inter, JetBrains Mono, Crimson Pro (woff2 + CSS)
```

## Slides

| #  | Title                            | What's on it |
|----|----------------------------------|--------------|
| 1  | National PV Roof Database        | Title, inputs / pipeline / output overview |
| 2  | Goal                             | Plain-language hero diagram (data → pipeline → DB) |
| 3  | The Problem                      | Size and time problem in one slide (90 TB / weeks → 20 % / 3–5 days) |
| 4  | Pipeline Overview                | Animated SVG: 3 stages, marching-ants data flow |
| 5  | Index → Download                 | 5-step indexing + animated state-machine queue |
| 6  | Roof Segmentation                | 6-step engine summary + **embedded live map** of 13 tile JSONs |
| 7  | Results · dépt 82                | Stats + tilt histogram + azimuth polar + **embedded panel viewer** |

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

The two embedded viewers fetch the bundled data files automatically; they
also support drag-and-drop if you want to load a different département.

## Deploy on GitHub Pages

1. Push this directory to a GitHub repository.
2. **Settings → Pages → Source → Deploy from a branch**, branch `main`, folder `/ (root)`.
3. The site is served at `https://<user>.github.io/<repo>/`.

The `.nojekyll` file disables Jekyll, so `vendor/` and `data/` are served verbatim.

## Navigation

| Key                         | Action                  |
|-----------------------------|-------------------------|
| ↓ ↑ → ← Space               | next / previous slide   |
| PgDn / PgUp                 | next / previous slide   |
| Home / End                  | first / last slide      |
| right-side dots             | jump to slide           |
| mouse wheel / trackpad      | scroll-snap to slides   |
