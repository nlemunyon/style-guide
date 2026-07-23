# Cards

KPI cards, glass cards, white cards, accent-bordered cards, and stacked gallery cards.

## Card Variants

### White Card (Wedding CRM)

Clean, shadow-based depth on a light background:

```css
.card {
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0,0,0,0.05);
  padding: 1.5rem;
  margin-bottom: 1.5rem;
}

.card h3 {
  font-size: 1rem;
  font-weight: 500;
  color: #666;
  margin-bottom: 0.5rem;
}

.card .big-number {
  font-size: 2.5rem;
  font-weight: 300;
  color: #6b7f5c;
}
```

**Characteristics:** No border, shadow-only depth. Light weight numbers create an elegant, airy feel. Used for dashboard KPI display and content containers.

### Dark Card (DailyBrief.AI)

Border-based depth on near-black background:

```css
/* CSS version */
.card {
  background-color: #141414;
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 12px;
  padding: 1rem;
  transition: all 0.2s;
}

.card:hover {
  border-color: rgba(59, 130, 246, 0.3);
}

/* Tailwind equivalent */
/* bg-secondary rounded-xl border border-tertiary p-4
   transition-all duration-200 hover:border-accent/30 */
```

**Characteristics:** Subtle 5% white border replaces shadows. Hover reveals accent color. Compact 1rem padding for information density.

### Dark Card (Not A Doc AI)

Similar to DailyBrief but with slightly larger radius and padding:

```css
.card {
  background-color: #141414;
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 20px;
  padding: 1.25rem;
  transition: all 0.2s ease;
}

.card:hover {
  border-color: rgba(255, 255, 255, 0.1);
}
```

**Characteristics:** Larger 20px radius for softer feel. Hover brightens border without accent color. More generous padding than DailyBrief.

### Dual-Radius Cards (Vector RAG)

Vector RAG runs two card systems in one app. General UI cards echo Not A Doc AI (soft `20px`, border-only, no shadow); dashboard panels tighten to a crisp `8px` with a faint lift-shadow so they read against the pure-black base:

```jsx
/* UI card (chat, modals, sources) */
<div className="rounded-[20px] bg-bg-surface border border-border-default p-5
                transition-colors hover:border-border-hover">   {/* #0a0a0a / 8% border */}
```

```css
/* Dashboard panel */
.ap2-dash .card {
  background: var(--panel);            /* #0a0a0a */
  border: 1px solid var(--line);       /* rgba(255,255,255,0.08) */
  border-radius: var(--r);             /* 8px */
  box-shadow: var(--shadow);           /* 0 1px 2px rgba(0,0,0,.5), 0 1px 0 rgba(0,0,0,.3) */
}
.ap2-dash .card-head {                 /* 12px 16px, divider below */
  padding: 12px var(--pad);
  border-bottom: 1px solid var(--line-2);
}
```

**Characteristics:** `20px` for calm chat surfaces, `8px` for the dense analytical grid — the shared token palette keeps them feeling like one product.

### Glass Card (Map Creator)

Translucent card with backdrop blur:

```css
.form-section {
  background: rgba(255, 255, 255, 0.03);
  border-radius: 18px;
  padding: 24px;
  border: 1px solid rgba(160, 170, 160, 0.12);
  backdrop-filter: blur(20px);
}
```

**Characteristics:** Near-transparent background with green-tinted border. Backdrop blur creates frosted glass effect. 18px radius for a softer feel.

### Gallery Stacked Card (Map Creator)

Cards that layer to suggest multiple items:

```css
.city-stack {
  position: relative;
  cursor: pointer;
  transition: transform 0.3s;
}

.city-stack:hover {
  transform: translateY(-8px);
}

.stack-container {
  position: relative;
  width: 100%;
  aspect-ratio: 3/4;
}

.stack-card {
  position: absolute;
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.03);
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid rgba(160, 170, 160, 0.12);
  transition: all 0.3s;
}

/* Badge showing count */
.stack-badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background: #7dad7d;
  color: #141517;
  padding: 4px 10px;
  border-radius: 12px;
  font-size: 0.85rem;
  font-weight: 600;
}
```

**Characteristics:** Absolute positioning creates depth. 3:4 aspect ratio for map posters. Badge shows "+N" count. Dramatic 8px lift on hover.

## KPI Card (DailyBrief.AI)

The most visually sophisticated card variant — uses a gradient pseudo-element for glow:

```css
.kpi-card {
  position: relative;
  overflow: hidden;
  /* Base card styles (bg-secondary, rounded-xl, border, p-4) */
}

/* Gradient glow overlay */
.kpi-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom right, rgba(59,130,246,0.05), transparent);
  opacity: 0;
  transition: opacity 0.3s;
}

.kpi-card:hover::before {
  opacity: 1;
}
```

KPI cards display: title (text-secondary, small), value (3xl-4xl, white), subtitle, and optional trend percentage (green for positive, red for negative).

## Stat Box (Wedding CRM)

Compact centered stats for dashboard summaries:

```css
.stat-box {
  background: white;
  border-radius: 8px;
  padding: 1rem;
  text-align: center;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.stat-box .value {
  font-size: 1.8rem;
  font-weight: 300;
  color: #6b7f5c;
}

.stat-box .label {
  font-size: 0.75rem;
  color: #666;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}
```

## Card Comparison Table

| Property | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI | Vector RAG |
|----------|-------------|---------------|-------------|--------------|------------|
| Background | `#ffffff` | `#141414` | `rgba(255,255,255,0.03)` | `#141414` | `#0a0a0a` |
| Border | None | `1px rgba(255,255,255,0.05)` | `1px rgba(160,170,160,0.12)` | `1px rgba(255,255,255,0.05)` | `1px rgba(255,255,255,0.08)` |
| Radius | `12px` | `12px` | `16-18px` | `20px` | `20px` UI / `8px` dash |
| Padding | `1.5rem` | `1rem` | `24px` | `1.25rem` | `1.25rem` UI / `16px` dash |
| Shadow | `0 2px 10px rgba(0,0,0,0.05)` | None | None | None | None UI / `0 1px 2px rgba(0,0,0,.5)` dash |
| Hover effect | — | Border accent glow | `translateY(-8px)` | Border brightens | Border brightens |
| Glass | No | No | Yes (`backdrop-filter`) | No | Only on dash map/network overlays |

## How to Apply Cards

### For a CRM or admin panel:
- White cards with subtle shadow on a tinted background
- 12px radius for professional feel
- Large light-weight numbers for KPI display
- Use the stat-box pattern for dashboard summaries

### For a data dashboard:
- Dark cards with border-only depth
- Add a gradient pseudo-element for hover glow
- Compact 1rem padding for density
- Color-coded trend indicators in KPI cards

### For a creative portfolio or gallery:
- Glass cards with backdrop-filter for premium feel
- 16-18px radius for softer aesthetic
- Stack cards with absolute positioning for depth
- 3:4 aspect ratio for visual content
- Count badges on stacked items

### For a chat or AI interface:
- Larger 20px radius for friendly, approachable feel
- Subtle border that brightens on hover
- No shadow — depth comes from background tier
- If the same app also hosts a dense dashboard (Vector RAG), run a second tighter card system (8px radius, faint lift-shadow) but keep the shared token palette so both read as one product
