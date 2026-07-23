# Maps & Data Viz

OpenLayers map theming, SVG + Canvas map rendering, choropleth patterns, Recharts/Plotly configuration, force-directed networks, and progress bar visualizations.

## Animated SVG World Map (Vector RAG)

Vector RAG's landing background renders an entire world map in **pure SVG** — no canvas, no D3, no tiles — so it stays crisp at any size and ships zero external requests. A Pacific-centered equirectangular projection maps lon/lat into an 800×400 space, clipped to a focused viewport:

```tsx
<svg viewBox="60 30 680 340"
     className="absolute inset-0 w-full h-full pointer-events-none"
     preserveAspectRatio="xMidYMid slice" aria-hidden="true">

// Pacific-centered projection (center lon -155°, lat 75°N…-55°S)
function geoToSvg(lon, lat) {
  let x = lon + 155
  if (x > 180) x -= 360
  if (x < -180) x += 360
  return [(x + 180) * (800 / 360), (75 - lat) * (400 / 130)]
}
```

**Layered map** — pre-baked Natural Earth path strings, all stroked `#3a6d8c` (a muted blue-gray, deliberately *not* the UI accent), with the home region brighter than the rest:

| Region | Land opacity / width | Border opacity / width |
|--------|----------------------|------------------------|
| Americas · Europe/Africa | `0.12` / `0.4` | `0.08` / `0.25` |
| Asia + Pacific (focus) | `0.24` / `0.4` | `0.14` / `0.25` |

**Animated hotspots** — 15 geopolitical markers animate in sequence (`stepDuration = 3s`, full loop `15 × 3 = 45s`). Each destination pulses the instant its incoming arc arrives:

```tsx
// Connecting arc: quadratic Bézier bulged perpendicular to the chord, drawn via strokeDashoffset
<motion.path d={`M ${x1} ${y1} Q ${cx} ${cy} ${x2} ${y2}`}
  fill="none" stroke="#3a6d8c" strokeWidth={0.8} pathLength={1} strokeDasharray="1"
  initial={{ strokeDashoffset: 1, opacity: 0 }}
  animate={{ strokeDashoffset: [1, 0, 0], opacity: [0, 0.35, 0] }}
  transition={{ duration: 2, times: [0, 0.5, 1], ease: 'easeInOut',
                delay: i * 3, repeat: Infinity, repeatDelay: 43 }} />

// Pulsing dot + expanding ring
<motion.circle cx={x} cy={y} r={2.5} fill="#3a6d8c"
  animate={{ opacity: [0.15, 0.45, 0.15] }}
  transition={{ duration: 2, ease: 'easeInOut', delay: pulseDelay, repeat: Infinity, repeatDelay: 43 }} />
<motion.circle cx={x} cy={y} r={8} fill="none" stroke="#3a6d8c" strokeWidth={1.5}
  initial={{ scale: 0.3, opacity: 0.45 }} animate={{ scale: 1.8, opacity: 0 }}
  transition={{ duration: 2, ease: 'easeOut', delay: pulseDelay, repeat: Infinity, repeatDelay: 43 }} />
```

`useReducedMotion()` removes every arc and ring and renders static dots at flat `opacity 0.3`. This map is the ambient hero of the [chat welcome state](chat-interfaces.md).

## OpenLayers Map Theming (DailyBrief.AI)

The dashboard overrides OpenLayers' default light controls to match the dark theme:

```css
/* Dark map viewport */
.ol-viewport {
  background: #0a0a0a !important;
}

/* Dark map controls (zoom buttons) */
.ol-control {
  background-color: rgba(20, 20, 20, 0.8) !important;
  border-radius: 4px;
}

.ol-control button {
  background-color: rgba(30, 30, 30, 0.9) !important;
  color: #fff !important;
}

.ol-control button:hover {
  background-color: rgba(59, 130, 246, 0.5) !important;
}

/* Dark attribution */
.ol-attribution {
  background-color: rgba(20, 20, 20, 0.7) !important;
  color: #a1a1a1 !important;
  font-size: 10px !important;
}

.ol-attribution a {
  color: #3b82f6 !important;
}
```

### HeatmapLayer Gotcha

OpenLayers' `HeatmapLayer` can silently fail to render colors in certain configurations. The Crisis Monitor works around this by using colored circle markers via `VectorLayer` instead:

- **Dashboard mini-map:** Uses default HeatmapLayer (works for simple display)
- **Crisis Monitor:** Uses marker-based rendering (`renderMode="markers"`) with colored circles sized by intensity

### Map Container

```css
.ol-map-container {
  width: 100%;
  height: 100%;
  min-height: 200px;
}
```

## Choropleth Maps (DailyBrief.AI)

The Crisis Monitor displays two side-by-side choropleth maps:

- **Escalating regions:** Red color scheme (conflict/escalation)
- **De-escalating regions:** Green color scheme (cooperation/de-escalation)
- Both at 400px height in a 2-column grid
- Country polygons colored by metric value
- Dark basemap matching the site background

## Canvas Choropleth + Event Overlay (Vector RAG)

The dashboard's live event map is a **d3-geo Mercator** choropleth drawn to an HTML5 Canvas (high-DPI aware), with an SVG/HTML overlay for event points and labels. Geometry is a **bundled `world-atlas/countries-50m` TopoJSON** — vendored at build time, never a CDN. The projection is fitted to an Indo-Pacific viewport `[70°E,47°N]…[156°E,16°S]`, drag to pan, wheel to zoom (`1.0–8.0`, default `1.18`).

The canvas reads its colors from CSS variables via `getComputedStyle`, so it follows the theme automatically:

```css
--map-land:     #141414;                 /* base country fill (no data) */
--map-land-sel: #242424;                 /* selected/hover country */
--map-border:   rgba(255,255,255,0.10);
```

Countries fill along an **instability ramp** (low → high) at `0.41` alpha:

```
rgb(150,166,190)  →  rgb(214,158,70)  →  rgb(201,64,54)
```

Event points are sized by fatalities (`6 + 15*severity/25`px) and colored by event type (see palette below). Points newer than 7 days get a `.fresh` pinging glow:

```css
@keyframes ap2ping {
  0%        { box-shadow: 0 0 0 0  color-mix(in srgb, var(--pc) 55%, transparent); }
  70%, 100% { box-shadow: 0 0 0 11px transparent; }
}   /* 2.6s ease-out infinite */
```

Zoom controls and tooltips use glassmorphism — `color-mix(in srgb, var(--panel) 88%, transparent)` + `backdrop-filter: blur(4px)`.

**Event-type palette:** Battles `#d1453b`, Violence vs. civilians `#c2185b`, Explosions/Remote `#e8590c`, Riots `#d8941f`, Protests `#e6c100`, Strategic developments `#1f9488`, Maritime incident `#2f6fd0`, Air incursion `#7a5ae0` (unmapped → deterministic HSL hash).

## Force-Directed Actor Network (Vector RAG)

An actor-relationship graph rendered with **d3-force**:

- **Nodes** — radius `3 + sqrt(degree) * 1.6`, filled by ACLED actor category (State `#5c9ece`, Rebel `#d1453b`, Militia `#d8941f`, Rioters `#fbbf24`, Protesters `#4ade80`, Civilians `#a0a0a0`, External `#7a5ae0`, Other `#606060`). Active node: `1.4px` white stroke, opacity 1; idle: `0.6px` dark stroke, opacity 0.85. Labels (mono 8.5px) show only for high-degree or active nodes.
- **Links** — stroke `#5c9ece` normally, `#d1453b` when the interaction involves fatalities; width `0.5 + log(weight+1)` (max 4px); opacity 0.7 active / 0.2 idle.
- **Tooltip** — pinnable glass card (`var(--panel)` + `1px var(--line)` + `0 8px 28px rgba(0,0,0,.45)`) showing Type, Events, Connections, weighted Degree, Betweenness, Eigenvector.

## Recharts Configuration (DailyBrief.AI)

### Tooltip Theming

```jsx
<Tooltip
  contentStyle={{
    background: '#141414',
    border: '1px solid rgba(255,255,255,0.1)',
    borderRadius: '8px',
    color: '#fff',
    fontSize: '12px',
  }}
/>
```

### Axis Theming

```jsx
<XAxis
  tick={{ fill: '#a3a3a3', fontSize: 11 }}
  axisLine={{ stroke: 'rgba(255,255,255,0.05)' }}
  tickLine={false}
/>

<YAxis
  tick={{ fill: '#a3a3a3', fontSize: 11 }}
  axisLine={false}
  tickLine={false}
/>
```

### Grid Lines

```jsx
<CartesianGrid
  strokeDasharray="3 3"
  stroke="rgba(255,255,255,0.05)"
  vertical={false}
/>
```

### Chart Color Sequence

| Index | Color | Usage |
|-------|-------|-------|
| 0 | ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) `#3b82f6` | Primary data series |
| 1 | ![](https://via.placeholder.com/12/22c55e/22c55e.png) `#22c55e` | Cooperation / positive |
| 2 | ![](https://via.placeholder.com/12/ef4444/ef4444.png) `#ef4444` | Conflict / negative |
| 3 | ![](https://via.placeholder.com/12/eab308/eab308.png) `#eab308` | Neutral / warning |
| 4 | ![](https://via.placeholder.com/12/a855f7/a855f7.png) `#a855f7` | Category 5 |
| 5 | ![](https://via.placeholder.com/12/ec4899/ec4899.png) `#ec4899` | Category 6 |

### Chart Types Used

| Chart | Library | Page |
|-------|---------|------|
| KPI strip | Custom JSX | Daily Brief, Live Reporting |
| Pie/Donut | Recharts `PieChart` | Live Reporting (quad class), Actor Analysis (types) |
| Bar (horizontal) | Recharts `BarChart` | Actor Analysis (Goldstein scale) |
| Area (stacked) | Recharts `AreaChart` | Actor Analysis (actor types over time) |
| Line | Recharts `LineChart` | Actor Analysis (cooperation vs conflict) |
| Time series | Recharts `LineChart` | Trends (event volume, tone) |

## Plotly Configuration (Vector RAG)

Vector RAG renders inline chat charts with **Plotly.js** (self-hosted, `async`-loaded, all calls `typeof`-guarded). One shared dark layout — note the chart surface `#141414` sits *above* the card, matching DailyBrief's Recharts tooltip color:

```js
{
  paper_bgcolor: '#141414', plot_bgcolor: '#141414',
  font:   { color: '#a3a3a3', size: 11, family: 'Inter' },
  title:  { font: { color: '#ffffff', size: 14, family: 'Inter' } },
  xaxis:  { gridcolor: 'rgba(255,255,255,0.05)', zerolinecolor: 'rgba(255,255,255,0.05)', tickfont: { color: '#a3a3a3' } },
  yaxis:  { gridcolor: 'rgba(255,255,255,0.05)', zerolinecolor: 'rgba(255,255,255,0.05)', tickfont: { color: '#a3a3a3' } },
  legend: { font: { color: '#a3a3a3' }, bgcolor: 'transparent' },
}
```

The dashboard's own charts (time-series, sentiment sparklines) are hand-built **SVG** rather than Plotly — bars in `--accent` at 0.42 opacity → 1.0 on hover with a 1.5px top radius, a 5-line grid at `rgba(255,255,255,0.05)`, and mono 9px axes in `#606060`. Both share the ordered chart sequence `#5c9ece #22c55e #ef4444 #eab308 #a855f7 #ec4899` (identical to DailyBrief.AI).

## Progress Bars

### Map Creator - Generation Progress

```css
.progress-container {
  width: 80%;
  max-width: 300px;
  margin-bottom: 20px;
}

.progress-bar {
  width: 100%;
  height: 6px;
  background: rgba(160, 170, 160, 0.12);
  border-radius: 3px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(135deg, #5c8a5c 0%, #7dad7d 50%, #9dc49d 100%);
  border-radius: 3px;
  transition: width 0.3s ease-out;
  width: 0%;
}

.progress-text {
  display: flex;
  justify-content: space-between;
  margin-top: 8px;
  font-size: 0.75rem;
  color: #636966;
}
```

### Not A Doc AI - Reorder Probability Bars

Color-coded progress bars for ML predictions (implemented with Tailwind classes):

```jsx
<div className="h-2 rounded-full bg-surface-hover overflow-hidden">
  <div
    className={`h-full rounded-full ${
      score > 0.7 ? 'bg-success' :
      score > 0.4 ? 'bg-accent' :
      'bg-warning'
    }`}
    style={{ width: `${score * 100}%` }}
  />
</div>
```

Color thresholds: >70% green (success), >40% blue (accent), <40% yellow (warning).

### Vector RAG - Rank Bars

The dashboard's ranking widgets (fatalities by country, actor activity, sentiment) use a consistent thin-bar row: a `7px` tall, `rounded-4px` accent fill on a `--hi (#1a1a1a)` track, with the value in mono `13px` bold:

```css
.rank-row { display: grid; grid-template-columns: minmax(0,1.4fr) 1.6fr auto; align-items: center; }
.rank-bar { height: 7px; border-radius: 4px; background: var(--hi); }
.rank-bar > i { display: block; height: 100%; border-radius: 4px; background: var(--accent); }
.rank-val { font-family: var(--font-mono); font-size: 13px; font-weight: 600; text-align: right; }
```

Sentiment rows append a `52px` sparkline (minimal SVG polyline) — `#1f9488` for an up-trend, `#d1453b` for down.

### Not A Doc AI - Feature Importance Bars

Animated bars for ML feature weights:

```jsx
<motion.div
  className="h-2 rounded-full bg-accent"
  initial={{ width: 0 }}
  animate={{ width: `${importance * 100}%` }}
  transition={{ duration: 0.5, delay: index * 0.1 }}
/>
```

## Timer Display (Map Creator)

Large countdown/elapsed timer during poster generation:

```css
.timer {
  font-size: 2rem;
  font-weight: 600;
  color: #7dad7d;
  margin-bottom: 8px;
  font-variant-numeric: tabular-nums;  /* Fixed-width digits */
}
```

`font-variant-numeric: tabular-nums` prevents the timer from jumping as digits change width.

## How to Apply Data Viz

### For a dark-mode dashboard:
- Override map library controls to match your dark theme
- Use 5% white opacity for grid lines and axis lines
- Dark tooltip backgrounds (#141414) matching your card color
- Semantic color coding: red=negative, green=positive, yellow=neutral, blue=primary
- For an air-gapped/isolated deployment (Vector RAG): bundle map geometry (`world-atlas` TopoJSON) and chart libs locally, never a CDN; read canvas colors from CSS variables so the map follows the theme; glassmorphism (`color-mix` + `blur(4px)`) for map/network controls and tooltips

### For progress indicators:
- 6px height bar with accent gradient fill
- Smooth width transition (0.3s ease-out)
- Percentage + step label below the bar
- Use `tabular-nums` for timer displays

### For ML/analytics visualizations:
- Color-code thresholds (green >70%, blue >40%, yellow <40%)
- Animate bar widths on mount with staggered delays
- Keep bar heights consistent (h-2 / 8px)
