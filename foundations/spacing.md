# Spacing

Container widths, padding scales, grid systems, and information density across all five sites.

## Container Widths

| Site | Max Width | Padding | Strategy |
|------|-----------|---------|----------|
| Wedding CRM | `1200px` | `2rem` (32px) | Centered with generous margins |
| DailyBrief.AI | Full width | Sidebar + content | Fixed sidebar, fluid content |
| Map Creator | `1400px` | `0 24px` | Wider container for gallery |
| Not A Doc AI | Full width | Per-panel | Split-panel layout |
| Vector RAG | `max-w-7xl` chat / full-width dash | `16px` (dash `--pad`) | Centered chat column + full-bleed dashboard grid |

### Container CSS

```css
/* Wedding CRM - Classic centered container */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

/* Map Creator - Wider container for visual content */
.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 24px;
}

/* DailyBrief.AI - Sidebar + fluid content (Tailwind) */
/* Sidebar: 64px collapsed / 256px expanded */
/* Content fills remaining width */
```

## Grid Systems

### Wedding CRM - Auto-fit Responsive Grid

```css
/* Default responsive grid */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1.5rem;
}

/* Fixed column variants */
.grid-2 { grid-template-columns: 1fr 1fr; }
.grid-3 { grid-template-columns: repeat(3, 1fr); }
.grid-4 { grid-template-columns: repeat(4, 1fr); }

/* Form layout */
.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}
```

### DailyBrief.AI - Tailwind Grid Patterns

The dashboard uses various grid configurations per page section:

- **KPI strip:** 4-column grid (`grid-cols-4`)
- **Main content:** 2-column or 3-column with varying ratios
- **Actor analysis:** 80/20 split for charts vs insights
- **Crisis monitor:** 2-column for choropleth maps
- **News sections:** Full-width with internal tabs

### Vector RAG - Fixed-Ratio Dashboard Grids

The dashboard composes three named grids, all sharing a `14px` (`--gap`) gutter:

```css
.grid-main     { display: grid; gap: 14px; grid-template-columns: 440px 1fr 320px; }  /* brief · map · alerts */
.grid-bottom   { display: grid; gap: 14px; grid-template-columns: 1.25fr 1fr 1fr; }    /* time-series · actors · sentiment */
.grid-analysis { display: grid; gap: 14px; grid-template-columns: repeat(3, 1fr); }    /* three rank-bar cards */
```

Fixed pixel rails (`440px` / `320px`) flank a fluid `1fr` center so the map always claims the slack. The chat side, by contrast, uses no grid — a single `max-w-7xl` centered column with toggleable `280px` / `400px` sidebars.

### Map Creator - Two-Column + Gallery

```css
/* Main layout - form and preview side by side */
.main-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  padding: 24px 0;
}

/* Theme selector */
.theme-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(105px, 1fr));
  gap: 8px;
}

/* Quality options */
.quality-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 8px;
}

/* Gallery */
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 24px;
}

/* Expanded gallery modal */
.stack-expanded-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 20px;
  max-width: 1200px;
}
```

## Card Padding

| Site | Card Padding | Card Gap | Card Radius |
|------|-------------|----------|-------------|
| Wedding CRM | `1.5rem` (24px) | `1.5rem` | `12px` |
| DailyBrief.AI | `1rem` (16px) | `1rem` | `12px` |
| Map Creator | `24px` | `24px` | `16-18px` |
| Not A Doc AI | `1.25rem` (20px) | — | `20px` |
| Vector RAG | `16px` (dash) / `20px` (UI cards) | `14px` (dash) | `8px` dash · `20px` UI cards |

**Pattern:** The data-dense dashboards (DailyBrief, Vector RAG) use tighter `16px` padding; Vector RAG additionally drops its dashboard card radius to `8px` for a crisp analytical grid while keeping `20px` on general UI cards. The creative tool (Map Creator) and CRM use more generous spacing. Not A Doc AI falls in between.

## Section Spacing

| Site | Section Margin | Header Margin |
|------|---------------|---------------|
| Wedding CRM | Card: `margin-bottom: 1.5rem` | Page header: `margin-bottom: 2rem` |
| Map Creator | Header: `padding: 32px 0 24px` | Gallery section: `padding: 48px 0` |
| Not A Doc AI | — | — |

## Information Density Comparison

| Metric | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI | Vector RAG |
|--------|-------------|---------------|-------------|--------------|------------|
| Density | Medium | High | Medium | Low | Low (chat) / High (dashboard) |
| Primary use | Tables + cards | Charts + KPIs + maps | Form + gallery | Chat + panels | Chat + panels, and charts + maps + networks |
| Whitespace | Generous | Moderate | Moderate | Generous | Generous (chat) / Moderate (dashboard) |
| Items per row | 2-4 | 4-6 | 2 (main), auto-fill (gallery) | 1-2 panels | 1-2 (chat) / 3 (dashboard rows) |

**Pattern:** Vector RAG is two densities in one app — a calm, generous chat surface and a tight, information-rich dashboard — unified only by the shared token palette.

## Chat Widget Dimensions

Wedding CRM defines precise chat dimensions that transition between two modes:

```css
/* Normal mode */
.chat-widget {
  width: 520px;
  height: 640px;
  border-radius: 16px;
}

/* Content width constraint */
.chat-messages-inner { max-width: 680px; }

/* Expanded mode */
.chat-widget.expanded {
  width: 100vw;
  height: 100vh;
  border-radius: 0;
}
.chat-widget.expanded .chat-messages-inner { max-width: 720px; }

/* Sidebar (expanded only) */
.chat-sidebar { width: 260px; }

/* Mobile */
@media (max-width: 768px) {
  .chat-widget {
    width: calc(100vw - 16px);
    height: calc(100vh - 80px);
  }
}
```

## Full-Page Chat Dimensions (Vector RAG)

Where Wedding CRM is a floating widget, Vector RAG is a full-page chat that owns the viewport (`html, body, #root { height: 100%; overflow: hidden }` — the app manages every scroll region):

```css
/* Fixed header */
header { height: 56px; }                      /* h-14, border-bottom 1px #1f1f1f */

/* Centered message column */
.messages-inner { max-width: 80rem; }         /* max-w-7xl */

/* Toggleable sidebars (animated width, not breakpoint-driven) */
.history-sidebar   { width: 280px; }          /* left  — collapses to 0 */
.documents-sidebar { width: 400px; }          /* right — collapses to 0 */

/* Input bar */
.chat-input { padding: 12px 16px; }           /* px-4 py-3, textarea auto-grows to 200px max */
```

## Stat Box Layout

The Wedding CRM stat boxes use a compact centered layout:

```css
.stats-row {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 1rem;
}

.stat-box {
  background: white;
  border-radius: 8px;
  padding: 1rem;
  text-align: center;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
}

.stat-box .value { font-size: 1.8rem; font-weight: 300; color: #6b7f5c; }
.stat-box .label { font-size: 0.75rem; text-transform: uppercase; letter-spacing: 0.5px; }
```

## Aspect Ratios

| Element | Ratio | Site |
|---------|-------|------|
| Map poster preview | 3:4 | Map Creator |
| Gallery thumbnails | 3:4 | Map Creator |
| Banner items | 120px × 160px (3:4) | Map Creator |

## How to Choose Your Spacing System

### For information-dense tools (dashboards, analytics):
- Use 16px (1rem) as the base unit
- Card padding: 16px, gap: 16px
- Tight grids with 4+ columns
- Sidebar navigation to maximize content area

### For content-focused tools (CRM, admin):
- Use 24px (1.5rem) as the base unit
- Card padding: 24px, gap: 24px
- Max-width container (1200px) for comfortable reading
- 2-4 column grids with auto-fit

### For creative tools (editors, generators):
- Use 24px as the base unit
- Wider container (1400px) for visual content
- Two-column layout: controls + preview
- Gallery grids with auto-fill for responsive image display
