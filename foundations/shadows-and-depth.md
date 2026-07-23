# Shadows & Depth

Shadow systems, glass effects, layered depth, and glow effects across all five sites.

## Shadow Comparison

| Purpose | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI | Vector RAG |
|---------|-------------|---------------|-------------|--------------|------------|
| Card default | `0 2px 10px rgba(0,0,0,0.05)` | None (border-only) | None (border-only) | None (border-only) | Dash: `0 1px 2px rgba(0,0,0,.5)`; UI cards: border-only |
| Card hover | — | Border brightens | Border + `translateY(-8px)` | Border brightens | Border brightens (8%→14%) |
| Stat box | `0 1px 3px rgba(0,0,0,0.1)` | — | — | — | — |
| Chat widget | `0 20px 60px rgba(0,0,0,0.15)` | — | — | — | — |
| Button glow | — | — | `0 4px 20px rgba(125,173,125,0.3)` | — | — |
| Accent glow | — | `0 0 20px rgba(59,130,246,0.2)` | `0 0 20px rgba(125,173,125,0.3)` | `0 0 20px rgba(59,130,246,0.2)` | `0 0 20px rgba(92,158,206,0.2)` |
| Expanded hover | — | — | `0 20px 40px rgba(0,0,0,0.3)` | — | — |
| Chat toggle | `0 4px 20px rgba(74,90,58,0.4)` | — | — | — | — |

**Pattern:** Light-mode (Wedding CRM) relies on traditional box-shadows for depth. Dark-mode sites avoid shadows on cards (they'd disappear into the dark background) and instead use borders with subtle opacity changes. Glows and accent shadows create visual hierarchy in dark mode. Vector RAG is a hybrid: general UI cards are border-only (like the other dark sites), but its dashboard panels add a faint `0 1px 2px rgba(0,0,0,.5)` shadow to lift cards off the pure-black base where a border alone reads too subtly.

## Depth Strategies by Mode

### Light Mode (Wedding CRM)

Depth is created through shadow intensity:

```css
/* Level 1: Subtle card */
box-shadow: 0 2px 10px rgba(0,0,0,0.05);

/* Level 2: Stat box */
box-shadow: 0 1px 3px rgba(0,0,0,0.1);

/* Level 3: Floating element (chat widget) */
box-shadow: 0 20px 60px rgba(0,0,0,0.15), 0 0 0 1px rgba(0,0,0,0.05);

/* Level 4: Chat toggle (elevated + glow) */
box-shadow: 0 4px 20px rgba(74, 90, 58, 0.4), 0 0 0 0 rgba(102, 119, 86, 0.4);
```

### Dark Mode (DailyBrief.AI, Not A Doc AI)

Depth is created through background tier + border opacity:

```css
/* Level 1: Page background */
background: #0a0a0a;

/* Level 2: Card surface */
background: #141414;
border: 1px solid rgba(255, 255, 255, 0.05);

/* Level 3: Elevated surface */
background: #1a1a1a;
border: 1px solid rgba(255, 255, 255, 0.1);

/* Level 4: Accent highlight */
border-color: rgba(59, 130, 246, 0.3);
box-shadow: 0 0 20px rgba(59, 130, 246, 0.2);  /* glow */
```

### Pure-Black Four-Tier (Vector RAG)

Vector RAG starts from `#000000` and climbs four luminance steps, with borders one notch stronger than the other dark sites (8% vs 5%) so edges survive the black base:

```css
/* Level 1: Page background */
background: #000000;

/* Level 2: Card surface */
background: #0a0a0a;
border: 1px solid rgba(255, 255, 255, 0.08);

/* Level 3: Elevated (inputs, sidebar items) */
background: #111111;

/* Level 4: Active / hover */
background: #1a1a1a;

/* Accent highlight (focus, active send) */
border-color: #5c9ece;
box-shadow: 0 0 0 3px rgba(92, 158, 206, 0.3);  /* focus ring */
```

### Dark Mode with Glass (Map Creator)

Depth uses transparency + glass effects:

```css
/* Level 1: Page background */
background: #141517;

/* Level 2: Glass card */
background: rgba(255, 255, 255, 0.03);
border: 1px solid rgba(160, 170, 160, 0.12);
backdrop-filter: blur(20px);

/* Level 3: Solid surface */
background: #1a1c1e;
border: 1px solid rgba(160, 170, 160, 0.12);

/* Level 4: Selected/active element */
border-color: #7dad7d;
box-shadow: 0 0 20px rgba(125, 173, 125, 0.3);
```

## Glass / Frosted Effects

Map Creator is the only site that uses glass morphism:

```css
.form-section {
  background: rgba(255, 255, 255, 0.03);   /* nearly transparent */
  border-radius: 18px;
  padding: 24px;
  border: 1px solid rgba(160, 170, 160, 0.12);
  backdrop-filter: blur(20px);              /* frosted glass */
}
```

The `--glass` variable is defined as `rgba(140, 180, 140, 0.05)` — a very subtle green-tinted transparency used for secondary surfaces.

**When to use glass effects:**
- Creative tools where visual sophistication matters
- Overlays that need to show content underneath
- When the background has visual texture (images, gradients, maps)

**When to avoid:**
- Data-dense dashboards (readability > style)
- Forms with lots of text inputs (contrast issues)
- Mobile-first apps (performance cost of `backdrop-filter`)

## Glow Effects

### Accent Glow (Shared Pattern)

Three sites use accent-colored glows for emphasis:

```css
/* DailyBrief.AI - KPI card hover */
.kpi-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom right, rgba(59,130,246,0.05), transparent);
  opacity: 0;
  transition: opacity 0.3s;
}
.kpi-card:hover::before { opacity: 1; }

/* DailyBrief.AI - Pulse glow animation */
@keyframes pulse-glow {
  0%, 100% { box-shadow: 0 0 20px rgba(59, 130, 246, 0.3); }
  50% { box-shadow: 0 0 40px rgba(59, 130, 246, 0.6); }
}

/* Map Creator - Button glow */
.btn-primary {
  box-shadow: 0 4px 20px rgba(125, 173, 125, 0.3);
}
.btn-primary:hover {
  box-shadow: 0 8px 30px rgba(125, 173, 125, 0.4);
}

/* Map Creator - Selected theme glow */
.theme-option input:checked + .theme-card {
  border-color: #7dad7d;
  box-shadow: 0 0 20px rgba(125, 173, 125, 0.3);
}

/* Not A Doc AI - Shadow tokens */
--shadow-glow: 0 0 20px rgba(59, 130, 246, 0.2);
```

### Pulse Ring Animation (Wedding CRM)

The chat toggle uses a pulsing ring animation for attention:

```css
.chat-toggle {
  box-shadow: 0 4px 20px rgba(74, 90, 58, 0.4),
              0 0 0 0 rgba(102, 119, 86, 0.4);
  animation: pulse-ring 2.5s ease-out infinite;
}

@keyframes pulse-ring {
  0% {
    box-shadow: 0 4px 20px rgba(74, 90, 58, 0.4),
                0 0 0 0 rgba(102, 119, 86, 0.4);
  }
  50% {
    box-shadow: 0 4px 20px rgba(74, 90, 58, 0.4),
                0 0 0 12px rgba(102, 119, 86, 0);
  }
  100% {
    box-shadow: 0 4px 20px rgba(74, 90, 58, 0.4),
                0 0 0 0 rgba(102, 119, 86, 0);
  }
}

.chat-toggle:hover {
  animation: none;  /* Stop pulse on hover */
  box-shadow: 0 8px 30px rgba(74, 90, 58, 0.5);
}
```

## Overlay Backgrounds

| Overlay | Wedding CRM | Map Creator | Not A Doc AI | Vector RAG |
|---------|-------------|-------------|--------------|------------|
| Modal backdrop | `rgba(0,0,0,0.5)` | `rgba(0,0,0,0.95)` | — | `rgba(0,0,0,0.6)` + `blur(4px)` |
| Status overlay | — | `rgba(20,21,23,0.95)` | — | — |
| Banner fade | — | `linear-gradient(to bottom, transparent 50%, rgba(20,21,23,0.9) 100%)` | — | — |

Vector RAG is the only site pairing a moderate `60%` black backdrop with a `backdrop-filter: blur(4px)` frost — and it reuses that same glass recipe (`color-mix(panel 88%, transparent)` + `blur(4px)`) on dashboard map/network zoom controls and tooltips.

**Pattern:** Light-mode overlays use moderate opacity (50%) to dim content. Dark-mode overlays use very high opacity (95%) for a near-opaque backdrop that matches the dark aesthetic.

## Shadow Token System (Not A Doc AI)

Not A Doc AI defines shadows as reusable design tokens:

```css
@theme {
  --shadow-soft: 0 2px 8px rgba(0, 0, 0, 0.15);
  --shadow-soft-lg: 0 4px 16px rgba(0, 0, 0, 0.2);
  --shadow-glow: 0 0 20px rgba(59, 130, 246, 0.2);
}
```

This token approach makes it easy to maintain consistent shadows across components and swap shadow systems for different themes.

Vector RAG mirrors the same three-token idea (darker, for its pure-black base) plus a scoped dashboard shadow:

```js
// theme/tokens.ts
shadows = {
  soft:   '0 2px 8px rgba(0, 0, 0, 0.3)',
  softLg: '0 4px 16px rgba(0, 0, 0, 0.4)',
  glow:   '0 0 20px rgba(92, 158, 206, 0.2)',
}
// dashboard.css: --shadow: 0 1px 2px rgba(0,0,0,.5), 0 1px 0 rgba(0,0,0,.3);
```

## How to Build Your Depth System

### For light-mode apps:
1. Use box-shadows with increasing intensity (0.05 → 0.1 → 0.15)
2. Reserve strong shadows (0.15+) for floating elements only
3. Add subtle `0 0 0 1px rgba(0,0,0,0.05)` borders for extra definition

### For dark-mode apps:
1. Skip box-shadows on cards — use background tier + border opacity
2. Use accent-colored glows (`0 0 20px accent/20%`) for interactive elements
3. Increase border opacity on hover (5% → 10%)
4. Reserve animated glows for attention-grabbing elements (CTAs, notifications)

### For creative/premium apps:
1. Combine glass effects (`backdrop-filter: blur(20px)`) with transparent backgrounds
2. Use accent-colored button shadows that intensify on hover
3. Apply `translateY(-Npx)` on hover for physical lift effect
4. Use high-opacity (95%) overlays for modal/gallery views
