# DailyBrief.AI Design System

> Ultra-dark intelligence dashboard for analyzing 4.3M+ global events from GDELT. The aesthetic is command-center minimal -- high contrast data on near-black backgrounds. The design prioritizes information density while maintaining readability through a three-tier background system.

**Live:** [dailybrief.ai.ext.io](https://dailybrief.ai.ext.io)
**Stack:** React 18, Vite, Tailwind CSS, Recharts, OpenLayers, react-force-graph-2d, react-markdown
**Fonts:** Inter (body), JetBrains Mono (monospace)

---

## Color Palette

### Backgrounds (Three-Tier System)

The entire UI builds on three progressively lighter near-black surfaces. This creates depth without introducing color noise.

| Tier | Token | Hex | Swatch | Usage |
|------|-------|-----|--------|-------|
| Primary | `bg-primary` | `#0a0a0a` | ![](https://via.placeholder.com/12/0a0a0a/0a0a0a.png) | Page background, viewport, scrollbar track |
| Secondary | `bg-secondary` | `#141414` | ![](https://via.placeholder.com/12/141414/141414.png) | Cards, panels, sidebar |
| Tertiary | `bg-tertiary` | `#1a1a1a` | ![](https://via.placeholder.com/12/1a1a1a/1a1a1a.png) | Elevated surfaces, inputs, scrollbar thumb, hover states |

### Text

| Token | Hex | Swatch | Usage |
|-------|-----|--------|-------|
| Text primary | `#ffffff` | ![](https://via.placeholder.com/12/ffffff/ffffff.png) | Headings, KPI values, active nav labels |
| Text secondary | `#a3a3a3` | ![](https://via.placeholder.com/12/a3a3a3/a3a3a3.png) | Body text, descriptions, timestamps, attribution |

### Accent & Semantic

| Token | Hex | Swatch | Usage |
|-------|-----|--------|-------|
| Accent (blue) | `#3b82f6` | ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) | Active states, links, KPI highlights, chart accent |
| Accent glow | `rgba(59, 130, 246, 0.2)` | ![](https://via.placeholder.com/12/1a3a6b/1a3a6b.png) | Hover glow on KPI cards, pulse animation |
| Conflict (red) | `#ef4444` | ![](https://via.placeholder.com/12/ef4444/ef4444.png) | Conflict events, Material Conflict quad class, negative tone |
| Cooperation (green) | `#22c55e` | ![](https://via.placeholder.com/12/22c55e/22c55e.png) | Cooperation events, Material Cooperation quad class, positive tone |
| Neutral (yellow) | `#eab308` | ![](https://via.placeholder.com/12/eab308/eab308.png) | Verbal events, warnings, neutral indicators |

### Borders & Selection

| Token | Value | Usage |
|-------|-------|-------|
| Border default | `rgba(255, 255, 255, 0.05)` | Card borders, dividers |
| Border hover | `rgba(255, 255, 255, 0.1)` | Card hover state |
| Accent border | `rgba(59, 130, 246, 0.3)` | Active card border, focused inputs |
| Selection bg | `rgba(59, 130, 246, 0.3)` | Selected rows, active filters |

### Tailwind Config (colors)

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: '#0a0a0a',
        secondary: '#141414',
        tertiary: '#1a1a1a',
        accent: '#3b82f6',
        conflict: '#ef4444',
        cooperation: '#22c55e',
        neutral: '#eab308',
      },
    },
  },
}
```

---

## Typography

### Font Stack

| Role | Family | Import |
|------|--------|--------|
| Body | `Inter, system-ui, sans-serif` | Google Fonts |
| Mono | `'JetBrains Mono', monospace` | Google Fonts |

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet">
```

### Scale

| Element | Class / Style | Weight | Notes |
|---------|---------------|--------|-------|
| KPI value | `text-3xl` / `text-4xl` | 700 | Large numeric displays |
| Page heading | `text-2xl` | 700 | Page titles in navbar area |
| Section heading | `text-lg` / `text-xl` | 600 | Card titles, section labels |
| Body | `text-sm` / `text-base` | 400 | Default content |
| Caption | `text-xs` | 400 | Timestamps, labels, metadata |
| Monospace data | `font-mono text-xs` | 400 | Event codes, actor codes, data freshness |

No special OpenType features are used in this application. The type system relies entirely on weight and size contrast against the dark backgrounds.

---

## Spacing & Layout

### Structural Dimensions

| Element | Dimension | Notes |
|---------|-----------|-------|
| Sidebar collapsed | `64px` (w-16) | Icon-only mode |
| Sidebar expanded | `256px` (w-64) | Full labels visible |
| Navbar height | `h-16` (64px) | Fixed top bar |
| Card padding | `p-4` (16px) | Standard internal spacing |
| Grid gap | `gap-4` (16px) | Between cards and sections |
| Card border-radius | `rounded-xl` (12px) | All card surfaces |

### Grid System

Page content uses full-width responsive grids. Layouts are built with Tailwind grid utilities:

```html
<!-- KPI row -->
<div class="grid grid-cols-2 md:grid-cols-4 gap-4">

<!-- Two-column split (e.g., chart + leaderboard) -->
<div class="grid grid-cols-1 lg:grid-cols-2 gap-4">

<!-- Three-column layout -->
<div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-3 gap-4">
```

All page content sits to the right of the sidebar and below the navbar. There is no maximum content width -- layouts expand to fill the viewport.

---

## Components

### 1. Sidebar

Fixed left navigation. Collapses to 64px icon-only mode, expands to 256px with labels.

**Structure:**
- Logo at top: "Daily**Brief**.AI" (bold on "Brief")
- Icon navigation items with labels
- Active state: blue background + left accent border + animated dot indicator
- Footer: data freshness timestamp in monospace

```css
/* Active nav item */
.nav-item-active {
  background: rgba(59, 130, 246, 0.15);
  border-left: 3px solid #3b82f6;
}

/* Animated activity dot */
.nav-dot {
  width: 6px;
  height: 6px;
  border-radius: 9999px;
  background: #3b82f6;
  animation: pulse-glow 2s ease-in-out infinite;
}
```

**Collapse behavior:** On collapse, labels fade out and only icons remain. The sidebar width transitions smoothly via `transition-all duration-200`.

### 2. Navbar

Horizontal top bar with contextual controls.

**Elements:**
- Simple/Detailed toggle (switches between minimal and full filter display)
- Country filter dropdown (ISO codes, multi-select)
- Date presets: `24h`, `7d`, `30d`, `3m`, `6m`
- Custom date range picker

**Date preset buttons:**

```html
<button class="px-3 py-1 rounded-lg text-sm transition-all duration-200
  bg-tertiary text-secondary hover:text-white
  data-[active=true]:bg-accent data-[active=true]:text-white">
  7d
</button>
```

In "simple" mode, filter controls collapse and only the page title and essential actions remain visible.

### 3. Cards (Base)

The foundational container for all dashboard content.

```css
.card {
  background: #141414;
  border-radius: 12px;              /* rounded-xl */
  border: 1px solid rgba(255, 255, 255, 0.05);
  padding: 16px;                    /* p-4 */
  transition: border-color 200ms;
}

.card:hover {
  border-color: rgba(59, 130, 246, 0.3);
}
```

Tailwind equivalent:

```html
<div class="bg-secondary rounded-xl border border-white/5 p-4
            transition-all duration-200 hover:border-accent/30">
```

### 4. KPI Cards

Specialized cards for headline metrics. Feature a gradient pseudo-element and hover glow.

```css
.kpi-card {
  position: relative;
  overflow: hidden;
  background: #141414;
  border-radius: 12px;
  border: 1px solid rgba(255, 255, 255, 0.05);
  padding: 16px;
}

/* Gradient overlay from top-left */
.kpi-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    135deg,
    rgba(59, 130, 246, 0.05) 0%,
    transparent 50%
  );
  pointer-events: none;
}

/* Glow on hover */
.kpi-card:hover {
  box-shadow: 0 0 20px rgba(59, 130, 246, 0.15);
  border-color: rgba(59, 130, 246, 0.3);
}
```

**KPI value text:** `text-3xl` or `text-4xl`, `font-bold`, `text-white`. Sub-labels use `text-xs text-secondary`.

### 5. Mini World Map (OpenLayers)

Dark-themed map component on the Live Reporting page. Uses a custom dark tile source with forced dark styling on all OL controls.

```css
/* Force dark viewport */
.ol-viewport {
  background: #0a0a0a !important;
}

/* Dark controls (zoom, rotate) */
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

/* Subtle attribution */
.ol-attribution {
  background-color: rgba(20, 20, 20, 0.7) !important;
  color: #a1a1a1 !important;
  font-size: 10px !important;
}
```

**Important note on HeatmapLayer:** OpenLayers `HeatmapLayer` silently fails to render color in certain configurations. The Crisis Monitor page uses a marker-based rendering mode (`renderMode="markers"`) instead, which draws colored circles via `VectorLayer`. The Dashboard mini-map retains the default heatmap mode.

### 6. Quad Class Pie Chart (Recharts)

Donut-style pie chart showing the four CAMEO quad classes.

| Quad Class | Color | Hex |
|------------|-------|-----|
| Verbal Cooperation | Green | `#22c55e` ![](https://via.placeholder.com/12/22c55e/22c55e.png) |
| Material Cooperation | Blue | `#3b82f6` ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) |
| Verbal Conflict | Yellow | `#eab308` ![](https://via.placeholder.com/12/eab308/eab308.png) |
| Material Conflict | Red | `#ef4444` ![](https://via.placeholder.com/12/ef4444/ef4444.png) |

Custom tooltip and legend use the same dark card styling (`bg-secondary`, `border-white/5`).

### 7. Event Type Leaderboard

Ranked list of top event types with horizontal bar indicators.

```html
<div class="flex items-center gap-3">
  <span class="text-xs text-secondary w-6 text-right font-mono">1</span>
  <div class="flex-1">
    <div class="flex justify-between mb-1">
      <span class="text-sm text-white">Make public statement</span>
      <span class="text-xs text-secondary font-mono">124,503</span>
    </div>
    <div class="h-1.5 bg-tertiary rounded-full overflow-hidden">
      <div class="h-full bg-accent rounded-full" style="width: 100%"></div>
    </div>
  </div>
</div>
```

Bar fill color is `bg-accent` (#3b82f6). Background track is `bg-tertiary`.

### 8. Trending Actors

Similar leaderboard layout, displaying actor names with event counts and tone indicators. Positive tone appends a green dot, negative tone a red dot.

### 9. News Sections

Tabbed news display with National/International tabs and sort mode toggles.

**Tab styling:**

```html
<button class="px-4 py-2 text-sm rounded-t-lg transition-all duration-200
  text-secondary hover:text-white
  data-[active=true]:bg-secondary data-[active=true]:text-white
  data-[active=true]:border-b-2 data-[active=true]:border-accent">
  National
</button>
```

**Image galleries** display alongside article summaries. Images use `rounded-lg overflow-hidden` with a subtle border.

### 10. Crisis Monitor

Two main visualization types:

**Marker-based heatmap:** Colored circle markers on an OpenLayers map. Each marker is sized by event count and colored by tone (red for conflict, green for cooperation, yellow for mixed). This replaces `HeatmapLayer` which has rendering issues.

**Choropleth maps:** Two side-by-side maps showing escalating and de-escalating regions. Country fills use gradient scales:
- Escalation: transparent to `#ef4444` ![](https://via.placeholder.com/12/ef4444/ef4444.png)
- De-escalation: transparent to `#22c55e` ![](https://via.placeholder.com/12/22c55e/22c55e.png)

### 11. Actor Analysis

**Donut chart:** Actor type distribution (government, military, rebel, etc.) using Recharts `PieChart` with `innerRadius`.

**Horizontal bar chart (Goldstein scale):** Bars extend left (negative, red) and right (positive, green) from a center axis. Chart width is constrained to 80% of the container. Key Actor Insights panel occupies the remaining 20% on the right.

**Timeline charts:** Cooperation vs Conflict and Actor Type breakdowns displayed as side-by-side `AreaChart` components from Recharts.

### 12. Daily Brief (AI Narratives)

AI-generated intelligence reports rendered via `react-markdown`.

**KPI strip** at the top shows key metrics for the selected country in a horizontal row of compact KPI cards.

**Markdown heading styles:**

```css
/* Custom heading styles within AI reports */
.narrative h2 {
  font-size: 1.25rem;
  font-weight: 700;
  color: #ffffff;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  padding-bottom: 0.5rem;
  margin-top: 1.5rem;
  margin-bottom: 1rem;
}

.narrative h3 {
  font-size: 1.1rem;
  font-weight: 600;
  color: #3b82f6;
  margin-top: 1.25rem;
  margin-bottom: 0.75rem;
}

.narrative p {
  color: #a3a3a3;
  line-height: 1.7;
  margin-bottom: 0.75rem;
}

.narrative strong {
  color: #ffffff;
}
```

Accompanying data tables (events, interactions, actors, GKG themes/persons/orgs/quotes) use the standard card + table styling.

---

## Custom Scrollbar

Applied globally. Matches the three-tier background system.

```css
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: #0a0a0a;
}

::-webkit-scrollbar-thumb {
  background: #1a1a1a;
  border-radius: 9999px;
}

::-webkit-scrollbar-thumb:hover {
  background: #a3a3a3;
}
```

The scrollbar is intentionally subtle at rest (`#1a1a1a` thumb on `#0a0a0a` track) and becomes visible on hover (`#a3a3a3`). This keeps the interface clean while still providing scroll affordance when needed.

---

## Animations

### Tailwind Config

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      keyframes: {
        'pulse-glow': {
          '0%, 100%': {
            boxShadow: '0 0 20px rgba(59, 130, 246, 0.3)',
          },
          '50%': {
            boxShadow: '0 0 40px rgba(59, 130, 246, 0.6)',
          },
        },
        'fade-in': {
          '0%': {
            opacity: '0',
            transform: 'translateY(10px)',
          },
          '100%': {
            opacity: '1',
            transform: 'translateY(0)',
          },
        },
      },
      animation: {
        'pulse-glow': 'pulse-glow 2s ease-in-out infinite',
        'fade-in': 'fade-in 0.3s ease-out',
      },
    },
  },
}
```

### Transition Standard

All interactive elements use `transition-all duration-200` (200ms). This applies to:

- Card border color changes on hover
- Button background/text color changes
- Sidebar expand/collapse width
- Nav item active state changes
- Filter dropdown open/close
- KPI card glow effect

```html
<!-- Standard transition pattern -->
<div class="transition-all duration-200 hover:border-accent/30">
```

### Fade-In on Mount

Cards and sections use the `fade-in` animation on initial render:

```html
<div class="animate-fade-in">
  <!-- Card content -->
</div>
```

### Pulse Glow

Used on the active sidebar navigation dot and optionally on KPI cards to draw attention:

```html
<span class="animate-pulse-glow inline-block w-1.5 h-1.5 rounded-full bg-accent"></span>
```

---

## Responsive Behavior

### Sidebar

| Viewport | Behavior |
|----------|----------|
| Desktop (default) | Expanded (256px) with labels |
| Narrow / user toggle | Collapsed (64px), icon-only |

The sidebar collapse is user-toggled, not breakpoint-driven. Content area adjusts via `ml-16` (collapsed) or `ml-64` (expanded).

### Grid Layouts

| Breakpoint | KPI Grid | Content Grid |
|------------|----------|--------------|
| `< md` | 2 columns | 1 column |
| `md` | 4 columns | 2 columns |
| `xl` | 4 columns | 3 columns |

### Navbar Filters

In "simple" mode (toggled via a switch in the navbar), date presets, country filters, and advanced controls hide. Only the page title and the simple/detailed toggle remain visible. This is useful for presentation or focused analysis.

---

## Global Filter System

All pages share filter state through React Context (`FilterContext`). Filters propagate automatically via `getApiParams()` to every API call.

| Filter | Type | Options |
|--------|------|---------|
| Date range | Preset / custom | 24h, 7d, 30d, 3m, 6m, custom |
| Countries | Multi-select | ISO country codes |
| Event types | Multi-select | CAMEO root codes |
| Quad class | Multi-select | 1 (Verbal Coop), 2 (Material Coop), 3 (Verbal Conflict), 4 (Material Conflict) |
| Tone range | Slider | -100 to 100 |
| Goldstein range | Slider | -10 to 10 |

Active filters appear as pills in the navbar with a dismiss button. Filter pills use:

```html
<span class="inline-flex items-center gap-1 px-2 py-0.5 rounded-full text-xs
  bg-accent/20 text-accent border border-accent/30">
  USA
  <button class="hover:text-white">&times;</button>
</span>
```

---

## Chart Theming (Recharts)

All Recharts components follow the same dark theme:

```jsx
// Tooltip
<Tooltip
  contentStyle={{
    backgroundColor: '#141414',
    border: '1px solid rgba(255, 255, 255, 0.1)',
    borderRadius: '8px',
    color: '#ffffff',
    fontSize: '12px',
  }}
  labelStyle={{ color: '#a3a3a3' }}
/>

// Axis
<XAxis
  stroke="#a3a3a3"
  tick={{ fill: '#a3a3a3', fontSize: 11 }}
  axisLine={{ stroke: 'rgba(255, 255, 255, 0.1)' }}
  tickLine={false}
/>

// Grid
<CartesianGrid
  strokeDasharray="3 3"
  stroke="rgba(255, 255, 255, 0.05)"
/>

// Legend
<Legend
  wrapperStyle={{ color: '#a3a3a3', fontSize: '12px' }}
/>
```

Standard chart color sequence for multi-series data:

| Index | Color | Hex | Usage |
|-------|-------|-----|-------|
| 0 | Blue | `#3b82f6` | ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) Primary series |
| 1 | Green | `#22c55e` | ![](https://via.placeholder.com/12/22c55e/22c55e.png) Cooperation / positive |
| 2 | Red | `#ef4444` | ![](https://via.placeholder.com/12/ef4444/ef4444.png) Conflict / negative |
| 3 | Yellow | `#eab308` | ![](https://via.placeholder.com/12/eab308/eab308.png) Neutral / verbal |
| 4 | Purple | `#a855f7` | ![](https://via.placeholder.com/12/a855f7/a855f7.png) Additional series |
| 5 | Cyan | `#06b6d4` | ![](https://via.placeholder.com/12/06b6d4/06b6d4.png) Additional series |

---

## Tables

Data tables use alternating row backgrounds and hover highlights:

```css
.table-row {
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  transition: background-color 200ms;
}

.table-row:hover {
  background: rgba(59, 130, 246, 0.05);
}

.table-header {
  color: #a3a3a3;
  font-size: 0.75rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.05em;
  padding: 0.75rem 1rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.table-cell {
  padding: 0.75rem 1rem;
  font-size: 0.875rem;
  color: #ffffff;
}
```

Tailwind equivalent:

```html
<thead>
  <tr class="border-b border-white/10">
    <th class="text-xs text-secondary font-medium uppercase tracking-wider px-4 py-3 text-left">
      Column
    </th>
  </tr>
</thead>
<tbody>
  <tr class="border-b border-white/5 transition-all duration-200 hover:bg-accent/5">
    <td class="px-4 py-3 text-sm text-white">Value</td>
  </tr>
</tbody>
```

---

## Adaptation Guide

This design system adapts well to any dark, data-dense dashboard. The three-tier background system, accent color, and component patterns transfer directly.

### 1. Cybersecurity Operations Dashboard (SIEM/SOC)

- Swap conflict/cooperation for `threat`/`resolved` using the same red/green tokens
- KPI cards become threat count, mean time to respond, active incidents, blocked IPs
- Crisis Monitor map becomes a geo-attack map with the same marker-based rendering
- Actor Analysis becomes threat actor profiling with the same donut + bar layout
- Daily Brief becomes automated threat intelligence summaries

### 2. Financial Trading Terminal

- KPI cards: portfolio value, daily P&L, open positions, margin usage
- Conflict/cooperation colors map to loss/gain
- Timeline charts become candlestick or line charts with the same axis theming
- News sections become market news feeds with sentiment indicators
- The Goldstein scale bar chart pattern works for sector performance comparison

### 3. Server Monitoring / DevOps Dashboard

- Three-tier backgrounds keep long monitoring sessions comfortable
- KPI cards: uptime, error rate, request latency, active alerts
- Heatmap becomes a service dependency map or geographic latency map
- Event leaderboard becomes top error types or slowest endpoints
- Crisis Monitor becomes an incident timeline with severity coloring
- Scrollbar and animation patterns transfer directly

### 4. Real-Time Analytics Platform

- KPI cards: active users, events/sec, conversion rate, revenue
- Quad class pie becomes a traffic source or user segment breakdown
- Actor network graph becomes a user journey or funnel visualization
- The filter system (date presets, multi-select dropdowns) applies to any analytics tool
- News sections become an activity feed or event log

**In all cases:** keep the `#0a0a0a` base, the `#3b82f6` accent, the 200ms transitions, and the card hover glow. These are the constants that define the DailyBrief aesthetic.
