# Vector RAG Design System

> Dark, command-center interface for a retrieval-augmented intelligence assistant. The signature moment is the landing screen: a pure-SVG world map, faded to a blue-gray whisper, with hotspots that pulse and fire arcing connection lines across the Indo-Pacific while a centered prompt invites the first question. From there the same near-black palette carries a streaming chat (with collapsible history + source-document sidebars) and a dense, multi-panel live dashboard of maps, networks, and time series. Every asset is self-hosted — no external fonts, no CDNs — a hard constraint of the isolated networks it runs on.

**Stack:** React 18, Vite, TypeScript, Tailwind CSS, Framer Motion, Plotly.js, d3-geo / d3-force, react-markdown
**Fonts:** Inter (body), JetBrains Mono (mono) — self-hosted `woff2`, **no Google Fonts**
**Mode:** Dark only (dashboard ships a stashed opt-in light theme)

---

## Design DNA

Three traits define the aesthetic and should survive any adaptation:

1. **Pure black base, four-tier depth.** The page is `#000000` — not a soft charcoal. Surfaces climb in near-black steps (`#0a0a0a → #111111 → #1a1a1a`) so panels separate by luminance alone, never by color.
2. **A single cool-blue accent.** `#5c9ece` is the only brand hue. It carries links, focus rings, active states, primary buttons, chart series 0, and the map motif. Semantic red/green/amber appear only for data meaning.
3. **Self-hosted everything.** Fonts, Plotly, world-atlas geometry are all vendored into `/static/`. The design cannot depend on a runtime fetch to an outside domain.

---

## Color Palette

### Backgrounds (Four-Tier System)

| Tier | Token | Hex | Swatch | Usage |
|------|-------|-----|--------|-------|
| Page | `bg.page` | `#000000` | ![](https://via.placeholder.com/12/000000/000000.png) | Root background, header, chat input bar |
| Surface | `bg.surface` | `#0a0a0a` | ![](https://via.placeholder.com/12/0a0a0a/0a0a0a.png) | Cards, dashboard panels |
| Elevated | `bg.elevated` | `#111111` | ![](https://via.placeholder.com/12/111111/111111.png) | Inputs, sidebar items, document blocks |
| Active | `bg.active` | `#1a1a1a` | ![](https://via.placeholder.com/12/1a1a1a/1a1a1a.png) | Hover/active states, inline code, dashboard `--hi` |

A recurring one-off border tone, `#1f1f1f`, is used inline for the header divider, chat-input border, and menus (slightly warmer than the tokenized `rgba(255,255,255,0.08)`).

### Text

| Token | Hex | Swatch | Usage |
|-------|-----|--------|-------|
| Text primary | `#e8e8e8` | ![](https://via.placeholder.com/12/e8e8e8/e8e8e8.png) | Headings, active nav, assistant body |
| Text secondary | `#a0a0a0` | ![](https://via.placeholder.com/12/a0a0a0/a0a0a0.png) | Labels, metadata, secondary controls |
| Text tertiary | `#606060` | ![](https://via.placeholder.com/12/606060/606060.png) | Inactive nav, hints, axis ticks |

### Accent

| Token | Value | Swatch | Usage |
|-------|-------|--------|-------|
| Accent | `#5c9ece` | ![](https://via.placeholder.com/12/5c9ece/5c9ece.png) | Primary buttons, links, focus, active send, chart series 0 |
| Accent hover | `#7ab4de` | ![](https://via.placeholder.com/12/7ab4de/7ab4de.png) | Hover on accent surfaces |
| Accent light | `#85d5f7` | ![](https://via.placeholder.com/12/85d5f7/85d5f7.png) | Wordmark, doc-download icon, KPI values |
| Accent muted | `rgba(92,158,206,0.15)` | ![](https://via.placeholder.com/12/1b2b38/1b2b38.png) | Badge/chip backgrounds, doc-index badge |
| Accent ring | `rgba(92,158,206,0.3)` | ![](https://via.placeholder.com/12/2a4a63/2a4a63.png) | Focus-visible ring, text selection |
| Map blue-gray | `#3a6d8c` | ![](https://via.placeholder.com/12/3a6d8c/3a6d8c.png) | **Landing-map** strokes, hotspot dots, arcs |

> Note the deliberate split: interactive UI uses `#5c9ece`, but the animated background map uses the muted `#3a6d8c` so the visualization never competes with foreground controls.

### Semantic

| Token | Hex | Swatch | Usage |
|-------|-----|--------|-------|
| Success | `#4ade80` | ![](https://via.placeholder.com/12/4ade80/4ade80.png) | Positive trend, low severity, `--pos` |
| Warning | `#fbbf24` | ![](https://via.placeholder.com/12/fbbf24/fbbf24.png) | Medium severity, warnings, `--warn` |
| Error | `#f87171` | ![](https://via.placeholder.com/12/f87171/f87171.png) | High severity, stop button, live dot, `--neg` |

Each has a `rgba(…,0.15)` muted variant for tinted backgrounds (`bg-accent-muted` pattern).

### Borders & Selection

| Token | Value | Usage |
|-------|-------|-------|
| Border default | `rgba(255,255,255,0.08)` | Cards, dividers |
| Border hover | `rgba(255,255,255,0.14)` | Card/interactive hover |
| Border strong | `rgba(255,255,255,0.2)` | Emphasis edges |
| Selection bg | `rgba(92,158,206,0.3)` | Text selection (`::selection`, white text) |
| Focus ring | `0 0 0 3px rgba(92,158,206,0.3)` | Global `:focus-visible` |

### Chart Sequence

Multi-series data cycles this ordered array:

| Index | Hex | Swatch |
|-------|-----|--------|
| 0 | `#5c9ece` | ![](https://via.placeholder.com/12/5c9ece/5c9ece.png) |
| 1 | `#22c55e` | ![](https://via.placeholder.com/12/22c55e/22c55e.png) |
| 2 | `#ef4444` | ![](https://via.placeholder.com/12/ef4444/ef4444.png) |
| 3 | `#eab308` | ![](https://via.placeholder.com/12/eab308/eab308.png) |
| 4 | `#a855f7` | ![](https://via.placeholder.com/12/a855f7/a855f7.png) |
| 5 | `#ec4899` | ![](https://via.placeholder.com/12/ec4899/ec4899.png) |

### Tailwind Config (tokens)

```js
// tailwind.config.js — theme.extend
colors: {
  bg:     { page: '#000000', surface: '#0a0a0a', elevated: '#111111', active: '#1a1a1a' },
  text:   { primary: '#e8e8e8', secondary: '#a0a0a0', tertiary: '#606060' },
  accent: { DEFAULT: '#5c9ece', hover: '#7ab4de', muted: 'rgba(92,158,206,0.15)', light: '#85d5f7' },
  border: { default: 'rgba(255,255,255,0.08)', hover: 'rgba(255,255,255,0.14)', strong: 'rgba(255,255,255,0.2)' },
  success:{ DEFAULT: '#4ade80', muted: 'rgba(74,222,128,0.15)' },
  warning:{ DEFAULT: '#fbbf24', muted: 'rgba(251,191,36,0.15)' },
  error:  { DEFAULT: '#f87171', muted: 'rgba(248,113,113,0.15)' },
},
fontFamily: {
  sans: ["'Inter'", '-apple-system', 'BlinkMacSystemFont', 'system-ui', 'sans-serif'],
  mono: ["'JetBrains Mono'", "'SF Mono'", 'Monaco', 'monospace'],
},
borderRadius: { sm: '8px', md: '12px', lg: '20px', pill: '100px' },
```

---

## Typography

### Font Stack (self-hosted)

| Role | Family | Source |
|------|--------|--------|
| Body | `'Inter', -apple-system, BlinkMacSystemFont, system-ui, sans-serif` | `/static/fonts/inter-latin.woff2` |
| Mono | `'JetBrains Mono', 'SF Mono', Monaco, monospace` | `/static/fonts/jetbrains-mono-latin.woff2` |

```css
@font-face {
  font-family: 'Inter';
  font-weight: 100 900;         /* single variable file */
  font-display: swap;
  src: url('/static/fonts/inter-latin.woff2') format('woff2');
}
body {
  font-feature-settings: 'cv02', 'cv03', 'cv04', 'cv11';  /* Inter character variants */
  -webkit-font-smoothing: antialiased;
}
```

Inter ships as one variable file (weights 100–900); JetBrains Mono spans 100–800. The body enables Inter's `cv02/cv03/cv04/cv11` character variants for cleaner digits and glyphs.

### Scale

| Element | Class / Style | Weight | Notes |
|---------|---------------|--------|-------|
| Landing greeting | `font-size: 3rem` | 700 | "Vector **RAG**" wordmark, `#e6edf3` + `#b0c4d4` |
| KPI / stat value | `1.5rem` / `text-3xl` | 700 | Accent `#5c9ece` numerics |
| Header wordmark | `text-lg` | 600 | `#85d5f7` + `#5ba8d4` split |
| Section / card title | `text-sm` (13px) | 600 | Dashboard `h2`, panel heads |
| Body | `text-sm` | 400 | Chat, descriptions |
| Caption / meta | `text-xs` | 400–500 | Timestamps, labels |
| Uppercase label | `text-[11px]` / mono 9–10px | 500 | Sidebar headers (`tracking-wider`), dashboard chip labels |
| Monospace data | `font-mono text-xs` | 400 | Metrics, counts, codes |

---

## Spacing & Layout

### Structural Dimensions

| Element | Dimension | Notes |
|---------|-----------|-------|
| Header height | `h-14` (56px) | Fixed, `border-bottom: 1px solid #1f1f1f` |
| History sidebar | `280px` | Left, user-toggled |
| Documents sidebar | `400px` | Right, user-toggled |
| Sidebar header | `h-10` | Uppercase `text-xs tracking-wider` |
| Chat content max-width | `max-w-7xl` | Message list + input centered |
| Chat input max height | `200px` | Auto-growing textarea |
| Dashboard card radius | `8px` (`--r`) | — |
| Dashboard padding | `16px` (`--pad`) | Inside cards |
| Dashboard gap | `14px` (`--gap`) | Between grid items |

### Border-Radius Scale

| Token | Value | Usage |
|-------|-------|-------|
| `sm` | `8px` | Dashboard cards, small buttons |
| `md` | `12px` | Modals, code blocks, chat-input wrapper (`rounded-xl`) |
| `lg` | `20px` | Cards, modals (`rounded-[20px]`) |
| `bubble` | `24px` | Chat message bubbles |
| `pill` | `100px` | Primary buttons, badges, scrollbar thumb |

### Shadows

| Token | Value |
|-------|-------|
| `soft` | `0 2px 8px rgba(0,0,0,0.3)` |
| `softLg` | `0 4px 16px rgba(0,0,0,0.4)` |
| `glow` | `0 0 20px rgba(92,158,206,0.2)` |

### Global Base Styles

```css
html, body, #root { height: 100%; overflow: hidden; }   /* app owns all scroll regions */
body { background: #000000; color: #e8e8e8; }

::selection { background: rgba(92,158,206,0.3); color: #fff; }
*:focus-visible { outline: none; box-shadow: 0 0 0 3px rgba(92,158,206,0.3); border-radius: 4px; }

/* Thin, near-invisible scrollbar */
::-webkit-scrollbar { width: 6px; height: 6px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.12); border-radius: 100px; }
::-webkit-scrollbar-thumb:hover { background: rgba(255,255,255,0.22); }
```

---

## Components

### 1. Header

Fixed 56px top bar on pure black with a `1px solid #1f1f1f` bottom rule.

**Structure:**
- **Wordmark** (left): "Vector **RAG**" — primary word `#85d5f7`, suffix `#5ba8d4`, `text-lg font-semibold tracking-tight`
- **Tab nav**: Chat · Report Builder · Dashboard (+ a Data Guide button)
- **Right cluster** (`gap-3`): language selector + user-email menu button

**Active tab** gets a subtle raised chip; inactive tabs are tertiary text brightening to secondary on hover:

```html
<!-- active -->
<button class="rounded-md px-3 py-1.5 text-sm text-text-primary"
        style="background:rgba(255,255,255,0.06); border:1px solid rgba(255,255,255,0.08)">Dashboard</button>
<!-- inactive -->
<button class="rounded-md px-3 py-1.5 text-sm text-text-tertiary hover:text-text-secondary transition-colors">Chat</button>
```

**User menu** button: transparent with `1px solid #1f1f1f`, hover → border `#5c9ece` + `rgba(92,158,206,0.08)` fill. Dropdown: `#0d0d0d` bg, `1px solid #1f1f1f`, `min-w-[140px]`, items `text-xs`, hover `rgba(255,255,255,0.05)`.

### 2. Animated World-Map Landing ★ signature

Shown by the welcome screen when a chat has no messages. A full-bleed SVG background sits behind a centered greeting and a cycling carousel of suggested questions.

**Rendering** — pure SVG, no canvas, no D3. A Pacific-centered equirectangular projection maps lon/lat into an 800×400 space, clipped to a focused viewport:

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

**Map layers** — pre-baked path strings (Natural Earth), all stroked `#3a6d8c`, `fill:none`. The home region (Asia-Pacific) is drawn brighter than the rest, so attention falls on it:

| Region | Land opacity / width | Border opacity / width |
|--------|----------------------|------------------------|
| Americas | `0.12` / `0.4` | `0.08` / `0.25` |
| Europe + Africa | `0.12` / `0.4` | `0.08` / `0.25` |
| Asia + Pacific | `0.24` / `0.4` | `0.14` / `0.25` |

**Hotspots** — 15 geopolitical markers (South China Sea, Korean Peninsula, Malacca, Guam, …). They animate in sequence: an arc travels from each hotspot to the next, and the destination dot pulses the instant the line arrives. `stepDuration = 3s`, so the full loop is `15 × 3 = 45s`.

*Connecting arc* — a quadratic Bézier bulged perpendicular to the chord (`min(dist*0.35, 40)`px), drawn by animating `strokeDashoffset`:

```tsx
<motion.path d={`M ${x1} ${y1} Q ${cx} ${cy} ${x2} ${y2}`}
  fill="none" stroke="#3a6d8c" strokeWidth={0.8} pathLength={1} strokeDasharray="1"
  initial={{ strokeDashoffset: 1, opacity: 0 }}
  animate={{ strokeDashoffset: [1, 0, 0], opacity: [0, 0.35, 0] }}
  transition={{ duration: 2, times: [0, 0.5, 1], ease: 'easeInOut',
                delay: i * 3, repeat: Infinity, repeatDelay: 45 - 2 }} />
```

*Pulsing dot + ring* — a solid dot breathing in opacity, plus an expanding ring that fades out:

```tsx
// dot
<motion.circle cx={x} cy={y} r={2.5} fill="#3a6d8c"
  animate={{ opacity: [0.15, 0.45, 0.15] }}
  transition={{ duration: 2, ease: 'easeInOut', delay: pulseDelay, repeat: Infinity, repeatDelay: 43 }} />
// ring
<motion.circle cx={x} cy={y} r={8} fill="none" stroke="#3a6d8c" strokeWidth={1.5}
  initial={{ scale: 0.3, opacity: 0.45 }} animate={{ scale: 1.8, opacity: 0 }}
  transition={{ duration: 2, ease: 'easeOut', delay: pulseDelay, repeat: Infinity, repeatDelay: 43 }} />
```

`pulseDelay` for hotspot *i* is `(i-1)*3 + 1` (hotspot 0 fires at t=0), synchronizing each pulse to its incoming arc.

**Accessibility** — `useReducedMotion()` drops all arcs and rings and renders static dots at a flat `opacity 0.3`.

**Foreground** — centered over the map (`relative z-10 text-center`):
- Greeting `h2`, `font-size: 3rem font-bold`, color `#e6edf3` with the accent word in `#b0c4d4`
- Subtitle `text-sm max-w-md`, `#848d97`
- An uppercase `text-[11px] tracking-widest` "try asking" label (`#484f58`)
- A carousel of 3 suggested-question buttons that cross-fades every **7s** (`AnimatePresence mode="wait"`, `opacity/y: 8→0`, 0.3s); buttons are plain text `#848d97` → `#e6edf3` on hover.

### 3. Chat Input

Fixed bottom bar: `shrink-0 border-t border-border-default bg-bg-page px-4 py-3`.

- **Wrapper**: `flex items-end gap-2 rounded-xl px-4 py-2.5`, bg `#0d0d0d`, border `#1f1f1f`; on focus → border `#5c9ece` + `box-shadow: 0 0 0 2px rgba(92,158,206,0.12)`
- **Textarea**: `flex-1 resize-none bg-transparent text-sm text-text-primary`, placeholder `text-text-tertiary`, auto-resize to `200px`
- **Send** (`h-8 w-8 rounded-lg`): active `bg #5c9ece / text #000`, hover `#7ab4de`, disabled `bg #1a1a1a / #555`
- **Stop** (while streaming): `bg rgba(239,68,68,0.15) / #ef4444`
- **PDF** (`h-10 w-10`): border `#1f1f1f` → hover `#5c9ece`, icon `#85d5f7`

### 4. Message Bubbles

| | User | Assistant |
|-|------|-----------|
| Align | `flex justify-end` | `flex justify-start` |
| Max width | `max-w-[90%]` | `max-w-[95%]` |
| Style | `#707070`, italic | markdown, primary text |
| Entrance | `userMessage` — x 16 + scale 0.98 → 0 | `assistantMessage` — y 8 → 0 |

Streaming shows a caret: `<span class="inline-block w-1.5 h-4 bg-accent animate-pulse">`. New user turns get extra `pt-8` lead-in.

### 5. History Sidebar (left)

280px collapsible panel of conversations.

- Header: `h-10`, `text-xs font-medium uppercase tracking-wider`
- Item: `px-2 py-2 rounded-lg`; active `bg-bg-elevated text-text-primary`; idle `text-text-secondary` → hover `bg-bg-elevated/50`
- Delete button reveals on hover: `h-6 w-6 rounded-md text-text-tertiary` → hover `text-error bg-error-muted`
- Toggle & panel animate width/opacity over `0.25s` ease `[0,0,0.2,1]`

### 6. Documents Sidebar (right)

400px panel of retrieved source documents.

- Source block: `bg-bg-elevated border border-border-default rounded-xl px-3 py-2.5`
- Index badge: `h-5 w-5 rounded-md bg-accent-muted text-xs font-medium text-accent`
- Expanded metadata: `text-xs text-text-secondary`

### 7. Reusable UI Kit

| Component | Key styling |
|-----------|-------------|
| **Button** | `primary` pill `bg-accent text-black` → hover `bg-accent-hover`; `secondary` `bg-bg-elevated border`; `ghost`; `danger` `bg-error-muted text-error`. Sizes sm/md/lg (`h-8/9/11`). Hover `y:-1`, tap `scale:0.98` |
| **Card** | `rounded-[20px] bg-bg-surface border border-border-default`, padding none/sm/md/lg, optional hover `border-border-hover` |
| **Badge** | `rounded-full px-3 py-0.5 text-xs`; variants default/accent/success/warning/error + optional dot |
| **Input / TextArea** | `h-9 rounded-lg bg-bg-elevated border`, focus `border-accent`; error `border-error` |
| **Modal** | overlay `bg-black/60` + `blur(4px)`; content `rounded-[20px] bg-bg-surface border p-6`, scale+opacity 0.2s |
| **Tabs** | `rounded-xl bg-bg-page p-1`; active pill = sliding `bg-bg-surface border` indicator |
| **Spinner** | `text-accent animate-spin`, sizes `h-4/6/8` |
| **TypingIndicator** | `text-base #e0e0e0`, fade-in + y-bounce, `aria-live="polite"` |

### 8. Markdown Renderer

Assistant answers render through react-markdown with a dark override set:

- **Inline code**: `bg-bg-active text-accent px-1.5 py-0.5 rounded font-mono text-xs`
- **Code block**: `rounded-xl bg-bg-page border`; header bar with language label + copy button; body `font-mono text-sm`
- **Tables**: `1px solid #333`, header `bg-white/[0.04]`, rows `even:bg-white/[0.02] hover:bg-white/[0.04]`
- **Headings**: h1 `text-2xl`, h2 `text-xl`, h3 `text-lg color #c8c8c8`
- **Links**: `text-accent` → underline; **blockquote**: `border-l-2 border-accent italic`
- **Doc references**: `inline-flex rounded bg-accent-muted px-1.5 py-0.5 text-xs text-accent`

### 9. Charts (Plotly)

Inline charts share one dark layout:

```js
{
  paper_bgcolor: '#141414', plot_bgcolor: '#141414',
  font: { color: '#a3a3a3', size: 11, family: 'Inter' },
  title: { font: { color: '#ffffff', size: 14, family: 'Inter' } },
  xaxis: { gridcolor: 'rgba(255,255,255,0.05)', zerolinecolor: 'rgba(255,255,255,0.05)', tickfont: { color: '#a3a3a3' } },
  yaxis: { gridcolor: 'rgba(255,255,255,0.05)', zerolinecolor: 'rgba(255,255,255,0.05)', tickfont: { color: '#a3a3a3' } },
  legend: { font: { color: '#a3a3a3' }, bgcolor: 'transparent' },
}
```

Container: `rounded-xl bg-bg-surface border`, ~400px tall, with an interpretation footnote (`text-xs text-text-secondary`) on a top border.

### 10. Dashboard

A dense, multi-row analytical surface scoped entirely under `.ap2-dash`, with its own **CSS-variable theme** (dark default; a full light theme is stashed behind `.theme-light` using OKLch). The variables mirror the app tokens so the two feel identical:

```css
.ap2-dash {
  --accent: #5c9ece; --accent-hover: #7ab4de;
  --bg: #000000; --panel: #0a0a0a; --panel-2: #111111;
  --ink: #e8e8e8; --ink-2: #a0a0a0; --ink-3: #606060;
  --line: rgba(255,255,255,0.08); --line-2: rgba(255,255,255,0.05); --hi: #1a1a1a;
  --pos: #4ade80; --neg: #f87171; --warn: #fbbf24;
  --map-land: #141414; --map-land-sel: #242424; --map-border: rgba(255,255,255,0.10);
  --r: 8px; --pad: 16px; --gap: 14px; --fs: 13px;
  --shadow: 0 1px 2px rgba(0,0,0,.5), 0 1px 0 rgba(0,0,0,.3);
}
```

**Layout grids** (`14px` gap throughout):

```css
.grid-main     { grid-template-columns: 440px 1fr 320px; }  /* brief · map · alerts+network */
.grid-bottom   { grid-template-columns: 1.25fr 1fr 1fr; }   /* time-series · actors · sentiment */
.grid-analysis { grid-template-columns: repeat(3, 1fr); }   /* three rank-bar cards */
```

**Card base**: `background: var(--panel); border: 1px solid var(--line); border-radius: var(--r); box-shadow: var(--shadow)`. Card heads use `12px 16px` padding and a `1px solid var(--line-2)` bottom rule.

**Widgets:**

- **Brief sidebar** — markdown daily summary (12.5px, line-height 1.55), escalation-watch sigma movers, "activity by area" with 6px `--accent`-filled progress bars, latest-alert list with 6px severity dots.
- **Event map** — HTML5 **Canvas choropleth** (d3-geo Mercator, bundled `world-atlas/countries-50m`, **no CDN**) fitted to an Indo-Pacific viewport `[70°E,47°N]…[156°E,16°S]`, drag-pan + wheel-zoom (1.0–8.0, default 1.18). Country fill `--map-land #141414`, selected `#242424`. An instability color ramp runs low→high: `rgb(150,166,190)` → `rgb(214,158,70)` → `rgb(201,64,54)` at `0.41` alpha. Event dots sized by fatalities, colored by event type; dots < 7 days old get a pinging glow.
- **Alerts feed** — 320px list; 7px severity circle (high `#f87171` / med `#fbbf24` / low `#4ade80`), bold location, relative time, 12px secondary text.
- **Actor network** — **d3-force** graph; node radius `3 + sqrt(degree)*1.6`, colored by actor category; links blue `#5c9ece` (red `#d1453b` when fatalities); glass tooltip (`backdrop-filter: blur(4px)`).
- **Time series** — custom SVG bar + dashed tone-line; bars `--accent` at 0.42 opacity → 1.0 on hover, 1.5px top radius; 5-line grid `rgba(255,255,255,0.05)`; mono 9px axes `#606060`.
- **Rank bars / actors / sentiment** — 7px `rounded-4px` bars on `--hi` track, mono `13px` bold values, sparklines (`#1f9488` up / `#d1453b` down).

**Event-type colors** (`Spark.tsx`):

| Type | Hex | Type | Hex |
|------|-----|------|-----|
| Battles | `#d1453b` | Riots | `#d8941f` |
| Violence against civilians | `#c2185b` | Protests | `#e6c100` |
| Explosions/Remote violence | `#e8590c` | Strategic developments | `#1f9488` |
| Maritime incident | `#2f6fd0` | Air incursion | `#7a5ae0` |

Unmapped types fall back to a deterministic HSL hash of the name. **Actor categories**: State `#5c9ece`, Rebel `#d1453b`, Militia `#d8941f`, Rioters `#fbbf24`, Protesters `#4ade80`, Civilians `#a0a0a0`, External `#7a5ae0`, Other `#606060`.

---

## Animations

Framer Motion drives every entrance; the shared easing is `cubic-bezier(0, 0, 0.2, 1)` (a decelerating "smooth-out").

| Variant | Motion | Duration |
|---------|--------|----------|
| `fadeIn` | opacity | 0.2s |
| `fadeInUp` | opacity + y 8→0 | 0.25s |
| `slideInLeft/Right` | opacity + x ±20 | 0.25s |
| `scaleIn` | opacity + scale 0.95→1 | 0.2s |
| `userMessage` | x 16 + scale 0.98 → 0 | 0.25s |
| `assistantMessage` | y 8 → 0 | 0.25s |
| `modalContent` | scale 0.95 + y 8 → 0 | 0.2s |
| `sidebar` | width 280↔0 + opacity | 0.25s / 0.2s |
| button hover / tap | y -1 / scale 0.98 | 0.15s / 0.1s |
| stagger container | children | 0.04s step |

Keyframe effects: the landing-map arcs/pulses (above); a dashboard `ap2ping` glow (`2.6s ease-out infinite`) on fresh events and the live dot; and a `ghostSweep` skeleton shimmer on loading cards. A global `prefers-reduced-motion` rule collapses all animation/transition durations to `0.01ms`.

---

## Responsive Behavior

### Chat

Both sidebars are **user-toggled**, not breakpoint-driven — history collapses `280px → 0`, documents `400px → 0`, each animating width + opacity. Message content stays centered within `max-w-7xl`.

### Dashboard

| Breakpoint | `.grid-main` | `.grid-bottom` | `.grid-analysis` |
|------------|--------------|----------------|-------------------|
| `> 1400px` | `440px 1fr 320px` | `1.25fr 1fr 1fr` | 3 columns |
| `1100–1400px` | `300px 1fr` (map-side spans, goes row) | `1fr 1fr` | 3 columns |
| `< 1100px` | `1fr` (stack) | `1fr` | `1fr` |

---

## Adaptation Guide

This system fits any dark, data-dense analyst tool where a hero visualization sets the mood and a chat or dashboard does the work. The pieces transfer cleanly:

### 1. OSINT / Intelligence Console
- Keep the animated map verbatim — swap hotspot coordinates + labels for your regions of interest.
- Chat becomes the analyst Q&A; the documents sidebar becomes your source/citation panel.
- Dashboard event types map to whatever taxonomy you track (incidents, signals, sightings).

### 2. Security Operations (SOC) Dashboard
- Recolor severity with the existing `#f87171 / #fbbf24 / #4ade80` triad.
- The d3-force actor network becomes an attack-path / asset graph; the choropleth becomes a geo-attack map.
- Time-series bars track alert volume; rank bars list top signatures or noisiest hosts.

### 3. Logistics / Fleet Monitoring (NOC)
- Map hotspots become depots or vessels with the same pulse-and-arc "activity" motif.
- KPI/stat cards show throughput, in-transit count, exceptions; sentiment panel becomes SLA health with sparklines.
- The self-hosted-everything constraint suits air-gapped ops centers.

### 4. Research / Knowledge Assistant
- Lead with the map as ambient brand motion behind the empty-state prompt, then drop it once a conversation starts.
- Lean on the markdown renderer + document sidebar; the dashboard is optional.

**In all cases keep the constants:** the `#000000` base and four-tier surfaces, the single `#5c9ece` accent (with `#3a6d8c` reserved for the background map so it never fights the UI), Inter + JetBrains Mono self-hosted, the `0,0,0.2,1` easing, and the pulse-and-arc map as the signature entrance.
