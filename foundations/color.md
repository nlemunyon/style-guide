# Color

Color palettes, semantic meanings, and opacity scales across all four sites.

## Background Tiers

Every site uses a layered background system to create depth without heavy shadows.

| Tier | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI |
|------|-------------|---------------|-------------|--------------|
| Page bg | ![](https://via.placeholder.com/12/f5f7f3/f5f7f3.png) `#f5f7f3` | ![](https://via.placeholder.com/12/0a0a0a/0a0a0a.png) `#0a0a0a` | ![](https://via.placeholder.com/12/141517/141517.png) `#141517` | ![](https://via.placeholder.com/12/0a0a0a/0a0a0a.png) `#0a0a0a` |
| Card/Surface | ![](https://via.placeholder.com/12/ffffff/ffffff.png) `#ffffff` | ![](https://via.placeholder.com/12/141414/141414.png) `#141414` | `rgba(255,255,255,0.03)` | ![](https://via.placeholder.com/12/141414/141414.png) `#141414` |
| Elevated | ![](https://via.placeholder.com/12/f8f9fa/f8f9fa.png) `#f8f9fa` | ![](https://via.placeholder.com/12/1a1a1a/1a1a1a.png) `#1a1a1a` | ![](https://via.placeholder.com/12/1a1c1e/1a1c1e.png) `#1a1c1e` | ![](https://via.placeholder.com/12/1a1a1a/1a1a1a.png) `#1a1a1a` |
| Active | ![](https://via.placeholder.com/12/f0f0f0/f0f0f0.png) `#f0f0f0` | — | `rgba(255,255,255,0.06)` | ![](https://via.placeholder.com/12/242424/242424.png) `#242424` |

**Pattern:** The three dark-mode sites all use a 3-step progression where each tier is only 6-10 lightness units apart. Wedding CRM inverts the pattern — warm tinted white as the base, pure white for surfaces.

## Accent Colors

| Purpose | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI |
|---------|-------------|---------------|-------------|--------------|
| Primary accent | ![](https://via.placeholder.com/12/7d8b6a/7d8b6a.png) `#7d8b6a` | ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) `#3b82f6` | ![](https://via.placeholder.com/12/7dad7d/7dad7d.png) `#7dad7d` | ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) `#3b82f6` |
| Accent hover | ![](https://via.placeholder.com/12/6b7f5c/6b7f5c.png) `#6b7f5c` | — | ![](https://via.placeholder.com/12/9dc49d/9dc49d.png) `#9dc49d` | ![](https://via.placeholder.com/12/2563eb/2563eb.png) `#2563eb` |
| Accent muted | `rgba(125,139,106,0.15)` | `rgba(59,130,246,0.2)` | `rgba(140,180,140,0.05)` | `rgba(59,130,246,0.15)` |
| Accent gradient | `135deg #667756→#4a5a3a→#3d4d2f` | None | `135deg #5c8a5c→#7dad7d→#9dc49d` | None |

**Pattern:** Two sites use sage/forest green, two use Tailwind blue-500. The green sites both use gradients; the blue sites use flat colors. Muted accent variants are created with 5-20% opacity of the accent color.

## Text Colors

| Role | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI |
|------|-------------|---------------|-------------|--------------|
| Primary | ![](https://via.placeholder.com/12/333333/333333.png) `#333` | ![](https://via.placeholder.com/12/ffffff/ffffff.png) `#ffffff` | ![](https://via.placeholder.com/12/f5f5f5/f5f5f5.png) `#f5f5f5` | ![](https://via.placeholder.com/12/ffffff/ffffff.png) `#ffffff` |
| Secondary | ![](https://via.placeholder.com/12/666666/666666.png) `#666` | ![](https://via.placeholder.com/12/a3a3a3/a3a3a3.png) `#a3a3a3` | ![](https://via.placeholder.com/12/9ca3a0/9ca3a0.png) `#9ca3a0` | ![](https://via.placeholder.com/12/a3a3a3/a3a3a3.png) `#a3a3a3` |
| Muted | ![](https://via.placeholder.com/12/999999/999999.png) `#999` | — | ![](https://via.placeholder.com/12/636966/636966.png) `#636966` | ![](https://via.placeholder.com/12/666666/666666.png) `#666666` |

## Semantic Colors

Used for status indicators, alerts, and data visualization.

| Semantic | Wedding CRM | DailyBrief.AI | Not A Doc AI |
|----------|-------------|---------------|--------------|
| Success bg | ![](https://via.placeholder.com/12/d4edda/d4edda.png) `#d4edda` | — | `rgba(74,222,128,0.15)` |
| Success text | ![](https://via.placeholder.com/12/155724/155724.png) `#155724` | ![](https://via.placeholder.com/12/22c55e/22c55e.png) `#22c55e` | ![](https://via.placeholder.com/12/4ade80/4ade80.png) `#4ade80` |
| Warning bg | ![](https://via.placeholder.com/12/fff3cd/fff3cd.png) `#fff3cd` | — | `rgba(251,191,36,0.15)` |
| Warning text | ![](https://via.placeholder.com/12/856404/856404.png) `#856404` | ![](https://via.placeholder.com/12/eab308/eab308.png) `#eab308` | ![](https://via.placeholder.com/12/fbbf24/fbbf24.png) `#fbbf24` |
| Error bg | ![](https://via.placeholder.com/12/f8d7da/f8d7da.png) `#f8d7da` | — | `rgba(248,113,113,0.15)` |
| Error text | ![](https://via.placeholder.com/12/721c24/721c24.png) `#721c24` | ![](https://via.placeholder.com/12/ef4444/ef4444.png) `#ef4444` | ![](https://via.placeholder.com/12/f87171/f87171.png) `#f87171` |

**Pattern:** Light mode (Wedding CRM) uses high-contrast tinted backgrounds with dark text. Dark mode sites use muted-opacity backgrounds (10-15% opacity of the semantic color) with the bright color as text.

## Border & Opacity Scales

| State | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI |
|-------|-------------|---------------|-------------|--------------|
| Default border | `#eee` / `#ddd` | `rgba(255,255,255,0.05)` | `rgba(160,170,160,0.12)` | `rgba(255,255,255,0.05)` |
| Hover border | — | `rgba(255,255,255,0.1)` | `rgba(255,255,255,0.15)` | `rgba(255,255,255,0.1)` |
| Focus ring | `rgba(125,139,106,0.15)` | `rgba(59,130,246,0.3)` | `rgba(125,173,125,0.1)` | `rgba(59,130,246,0.3)` |
| Accent border | ![](https://via.placeholder.com/12/7d8b6a/7d8b6a.png) `#7d8b6a` | `rgba(59,130,246,0.3)` | `var(--accent-primary)` | `rgba(59,130,246,0.3)` |

**Pattern:** Dark mode borders use white-based rgba (5% default, 10% hover). Map Creator tints its borders with a greenish hue (160,170,160). Wedding CRM uses traditional solid gray borders. Focus rings use 10-30% accent opacity.

## Status Pipeline (Wedding CRM)

The CRM defines a unique status color system for its sales pipeline:

| Status | Background | Text |
|--------|-----------|------|
| Lead | ![](https://via.placeholder.com/12/e9ecef/e9ecef.png) `#e9ecef` | ![](https://via.placeholder.com/12/495057/495057.png) `#495057` |
| Contacted | ![](https://via.placeholder.com/12/cce5ff/cce5ff.png) `#cce5ff` | ![](https://via.placeholder.com/12/004085/004085.png) `#004085` |
| Quoted | ![](https://via.placeholder.com/12/fff3cd/fff3cd.png) `#fff3cd` | ![](https://via.placeholder.com/12/856404/856404.png) `#856404` |
| Booked | ![](https://via.placeholder.com/12/d4edda/d4edda.png) `#d4edda` | ![](https://via.placeholder.com/12/155724/155724.png) `#155724` |
| Completed | ![](https://via.placeholder.com/12/c3e6cb/c3e6cb.png) `#c3e6cb` | ![](https://via.placeholder.com/12/155724/155724.png) `#155724` |
| Lost | ![](https://via.placeholder.com/12/f8d7da/f8d7da.png) `#f8d7da` | ![](https://via.placeholder.com/12/721c24/721c24.png) `#721c24` |

## Data Visualization Colors (DailyBrief.AI)

| Category | Color | Usage |
|----------|-------|-------|
| Conflict | ![](https://via.placeholder.com/12/ef4444/ef4444.png) `#ef4444` | Events, bars, areas representing conflict/verbal conflict |
| Cooperation | ![](https://via.placeholder.com/12/22c55e/22c55e.png) `#22c55e` | Events representing cooperation/material cooperation |
| Neutral | ![](https://via.placeholder.com/12/eab308/eab308.png) `#eab308` | Neutral/ambiguous event categories |
| Accent | ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) `#3b82f6` | Highlighted data points, selected items |

## How to Build Your Palette

### For a dark-mode app:
1. Pick a near-black base (e.g., `#0a0a0a` or `#0f0f0f`)
2. Create 2-3 surface tiers by adding 4-8 lightness units each step
3. Choose one accent color — use it at full opacity for CTAs, 15-30% for muted backgrounds
4. Set borders at 5% white opacity, increase to 10% on hover
5. Text: pure white for primary, ~64% white for secondary

### For a light-mode app:
1. Pick a tinted white base (e.g., `#f5f7f3` for warm, `#f0f4ff` for cool)
2. Use pure white for card surfaces
3. Choose a muted accent — desaturated greens/blues work best for professional tools
4. Semantic colors: pastel backgrounds with dark text for high contrast
5. Text: `#333` for primary, `#666` for secondary, `#999` for muted
