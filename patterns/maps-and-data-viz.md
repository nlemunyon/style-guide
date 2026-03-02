# Maps & Data Viz

OpenLayers map theming, choropleth patterns, Recharts configuration, and progress bar visualizations.

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

### For progress indicators:
- 6px height bar with accent gradient fill
- Smooth width transition (0.3s ease-out)
- Percentage + step label below the bar
- Use `tabular-nums` for timer displays

### For ML/analytics visualizations:
- Color-code thresholds (green >70%, blue >40%, yellow <40%)
- Animate bar widths on mount with staggered delays
- Keep bar heights consistent (h-2 / 8px)
