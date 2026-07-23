# Typography

Font pairings, size scales, weights, and OpenType features across all five sites.

## Font Families

| Role | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI | Vector RAG |
|------|-------------|---------------|-------------|--------------|------------|
| Body | System stack | Inter | Inter | Inter | Inter |
| Mono | `ui-monospace` | JetBrains Mono | — | JetBrains Mono | JetBrains Mono |
| Loading | None (system) | Google Fonts | Google Fonts | Google Fonts | **Self-hosted woff2** |

### Font Stacks

```css
/* Wedding CRM - System stack for fast loading */
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;

/* DailyBrief.AI */
font-family: 'Inter', system-ui, sans-serif;        /* Body */
font-family: 'JetBrains Mono', monospace;            /* Code */

/* Map Creator - Inter only */
font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;

/* Not A Doc AI - Most complete stack */
font-family: 'Inter', -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
font-family: 'JetBrains Mono', 'SF Mono', Monaco, monospace;

/* Vector RAG - identical stack to Not A Doc, but self-hosted (no Google Fonts) */
font-family: 'Inter', -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
font-family: 'JetBrains Mono', 'SF Mono', Monaco, monospace;
```

**Pattern:** Four of five sites use Inter as the primary font. Inter's clean geometry pairs well with both dark and light backgrounds. JetBrains Mono appears in all three data-heavy apps (DailyBrief, Not A Doc AI, Vector RAG) for code and data display. Wedding CRM skips custom fonts entirely for the fastest possible load.

**Self-hosted fonts (Vector RAG):** Unlike the others, Vector RAG cannot pull from Google Fonts — it deploys on isolated networks that block external domains. Both families ship as single **variable** `woff2` files served from `/static/fonts/` with `font-display: swap`:

```css
@font-face {
  font-family: 'Inter';
  font-weight: 100 900;                 /* one variable file covers all weights */
  font-display: swap;
  src: url('/static/fonts/inter-latin.woff2') format('woff2');
}
@font-face {
  font-family: 'JetBrains Mono';
  font-weight: 100 800;
  font-display: swap;
  src: url('/static/fonts/jetbrains-mono-latin.woff2') format('woff2');
}
```

## OpenType Features

Not A Doc AI **and Vector RAG** enable Inter's alternate character forms (identical settings):

```css
/* Not A Doc AI / Vector RAG - Inter character alternates */
body {
  font-feature-settings: 'cv02', 'cv03', 'cv04', 'cv11';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

| Feature | Effect |
|---------|--------|
| `cv02` | Alternate 'a' (single-storey) |
| `cv03` | Alternate 'g' |
| `cv04` | Alternate 'i' |
| `cv11` | Single-storey 'l' |

These alternates make Inter feel more geometric and modern — a good match for AI/tech interfaces.

## Size Scales

### Headings

| Element | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI | Vector RAG |
|---------|-------------|---------------|-------------|--------------|------------|
| Page title (h1) | 1.8rem / 400 | Varies by page | 2.5rem / 700 | — | 3rem / 700 (landing greeting) |
| Section title (h2) | 1rem / 500 | — | 2rem / 700 | — | 13px / 600 (card head) |
| Card title (h3) | 1rem / 500 | — | — | — | 13px / 600 |
| Navbar brand | 1.5rem / 300 | — | 0.65rem / 600 | — | 1.125rem (`text-lg`) / 600 |

**Pattern:** Wedding CRM uses lighter weights (300-400) for a refined feel. Map Creator uses heavy weights (700) for visual impact. DailyBrief uses Tailwind utility classes rather than fixed sizes.

### Body & UI Text

| Element | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI | Vector RAG |
|---------|-------------|---------------|-------------|--------------|------------|
| Body text | Default / 1.6 lh | Default / 1.5 lh | 0.9rem / 1.6 lh | Default | 14px (`text-sm`) |
| Labels | — | — | 0.7rem / 600 | 0.75rem / 500 | 11px uppercase / mono 9-10px |
| Badges | 0.75rem / 500 | — | — | 0.75rem / 500 | 0.75rem (`text-xs`) / 500 |
| Table headers | 0.85rem / 500 | — | — | — | `text-xs` uppercase / 500 |
| Small text | 0.8rem | — | 0.6-0.65rem | — | `text-xs` (12px) |
| Chat message | 14px / 1.65 lh | — | — | — | 14px (`text-sm`) |
| Chat expanded | 15px / 1.7 lh | — | — | — | markdown / 1.6 lh |

## Weight Scale

| Weight | Wedding CRM | Map Creator | DailyBrief.AI | Not A Doc AI | Vector RAG |
|--------|-------------|-------------|---------------|--------------|------------|
| 300 (Light) | Navbar brand, big numbers | Imported | — | — | — |
| 400 (Regular) | Page headers, body | Body text | Body | Body | Body, chat |
| 500 (Medium) | Card titles, buttons, badges | Theme names, quality | — | Badges | Labels, badges, nav |
| 600 (Semibold) | Chat roles, guide headings | Labels, buttons, headings | — | — | Wordmark, card/section titles |
| 700 (Bold) | — | h1, h2 | — | — | Landing greeting, KPI/stat values |

**Pattern:** Wedding CRM spans 300-500 (light and airy). Map Creator uses 300-700 (high contrast between labels and headings). The data apps (DailyBrief, Not A Doc) keep weights simple at 400-500; Vector RAG reaches 700 but only for the hero greeting and numeric KPI values.

## Letter Spacing

| Context | Wedding CRM | Map Creator |
|---------|-------------|-------------|
| Navbar brand | `2px` | — |
| Table headers | `0.5px` | `1px` |
| Labels | — | `1px` + uppercase |
| Logo/brand | — | `3px` + uppercase |
| Chat header | `-0.01em` | — |

**Pattern:** Both production apps use positive letter-spacing on small uppercase text (labels, headers). Wedding CRM uses tighter spacing (`-0.01em`) for chat interface readability. Map Creator applies the widest spacing (`3px`) to its brand identity.

## Line Heights

| Context | Value | Used By |
|---------|-------|---------|
| Body text | 1.6 | Wedding CRM, Map Creator, Vector RAG (markdown) |
| Chat messages | 1.65 (normal), 1.7 (expanded) | Wedding CRM |
| Code blocks | 1.5 | Wedding CRM (chat) |
| Compact UI | 1.3-1.4 | Map Creator (cheat sheet), Vector RAG (dashboard 1.4-1.55) |

## Text Transforms

| Transform | Usage |
|-----------|-------|
| `uppercase` + wide spacing | Labels (Map Creator), table headers (Wedding CRM), brand text |
| `capitalize` | Theme names in gallery (Map Creator) |
| `text-transform: none` | Default for all body and heading text |

## Gradient Text

Map Creator uses gradient text for its main heading:

```css
h1 {
  background: linear-gradient(135deg, #5c8a5c 0%, #7dad7d 50%, #9dc49d 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

This technique only works on block-level elements and requires a solid fallback for older browsers.

## How to Choose Your Type System

### For a professional tool (CRM, admin panel):
- Use the system font stack for speed and native feel
- Keep weights between 300-500 for a clean, professional look
- Use 0.85rem uppercase with letter-spacing for table headers and labels
- Line-height 1.6 for comfortable reading

### For a data-dense dashboard:
- Use Inter for consistency across operating systems
- Add JetBrains Mono for code, data values, timestamps
- Enable OpenType alternates (`cv02-cv11`) for a distinctive feel
- Keep sizes compact — 12-14px body with 1.5 line-height

### For a creative tool:
- Use Inter with heavy weights (700) for headlines
- Apply gradient text to the main title
- Use wide letter-spacing (1-3px) on small uppercase labels
- Separate hierarchy with dramatic size jumps (0.65rem labels → 2.5rem headings)
