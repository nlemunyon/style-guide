# Applying Dark Minimal

How to apply the ultra-dark aesthetic (used by DailyBrief.AI and Not A Doc AI) to any project. This guide covers the three-tier background rule, border strategy, accent usage, and component styling.

## The Core Principle

Dark minimal design creates depth through subtle background tiers and near-invisible borders, not through shadows. Every surface is a shade of near-black, and color is used sparingly for accent and semantic meaning.

## Step 1: Define Your Background Tiers

Pick three background values with 6-10 lightness units between each:

```css
:root {
  --bg-page: #0a0a0a;      /* Deepest — page background */
  --bg-surface: #141414;    /* Middle — cards, panels */
  --bg-elevated: #1a1a1a;   /* Lightest — hover states, nested elements */
}
```

**Rule:** Never skip a tier. The page background is always the darkest. Cards sit on the middle tier. Interactive or nested elements use the lightest tier.

**Alternatives:**
- Slightly warmer: `#0f0f0f` → `#171717` → `#1f1f1f`
- Blue-tinted: `#0a0c10` → `#12151a` → `#1a1d24`

## Step 2: Define Your Border Strategy

Borders replace shadows in dark mode. Use white with very low opacity:

```css
:root {
  --border-default: rgba(255, 255, 255, 0.05);
  --border-hover: rgba(255, 255, 255, 0.1);
  --border-accent: rgba(59, 130, 246, 0.3);  /* Your accent at 30% */
}
```

**Usage rules:**
- All cards get `1px solid var(--border-default)`
- Hover increases to `var(--border-hover)`
- Active/selected items get `var(--border-accent)`
- Dividers use `var(--border-default)`

## Step 3: Pick One Accent Color

Choose a single accent color and derive muted variants from it:

```css
:root {
  --accent: #3b82f6;                        /* Full brightness for CTAs and links */
  --accent-hover: #2563eb;                  /* Darker for hover states */
  --accent-muted: rgba(59, 130, 246, 0.15); /* Background for badges and highlights */
  --accent-glow: rgba(59, 130, 246, 0.2);  /* Box-shadow for glow effects */
}
```

**Rule:** The accent color should appear on less than 10% of the screen. It marks interactive elements (buttons, links, active states) and important data points. Everything else is grayscale.

## Step 4: Set Up Text Colors

```css
:root {
  --text-primary: #ffffff;     /* Headings, values, important text */
  --text-secondary: #a3a3a3;   /* Labels, descriptions, secondary info */
  --text-tertiary: #666666;    /* Timestamps, hints, disabled text */
}
```

**Usage rules:**
- Primary text: headings, data values, navigation labels
- Secondary text: descriptions, table headers, metadata
- Tertiary text: timestamps, placeholder text, footnotes

## Step 5: Style Your Cards

```css
.card {
  background: var(--bg-surface);
  border: 1px solid var(--border-default);
  border-radius: 12px;       /* 12px for data-dense, 20px for chat/friendly */
  padding: 1rem;             /* 1rem for dense, 1.25rem for comfortable */
  transition: border-color 0.2s;
}

.card:hover {
  border-color: var(--border-hover);
}
```

## Step 6: Add Semantic Colors

```css
:root {
  --success: #4ade80;
  --success-muted: rgba(74, 222, 128, 0.15);
  --warning: #fbbf24;
  --warning-muted: rgba(251, 191, 36, 0.15);
  --error: #f87171;
  --error-muted: rgba(248, 113, 113, 0.15);
}
```

**Dark mode semantic pattern:** Use the muted variant (15% opacity) as background, full-brightness color as text.

```css
.badge-success {
  background: var(--success-muted);
  color: var(--success);
}
```

## Step 7: Custom Scrollbar

```css
::-webkit-scrollbar { width: 8px; height: 8px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.15);
  border-radius: 100px;
}
::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 255, 255, 0.25);
}
```

## Step 8: Typography

```css
body {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
  color: var(--text-primary);
  background: var(--bg-page);
  -webkit-font-smoothing: antialiased;
}

/* Optional: Inter character alternates for a more distinctive feel */
body { font-feature-settings: 'cv02', 'cv03', 'cv04', 'cv11'; }

/* Monospace for data, code, timestamps */
.mono { font-family: 'JetBrains Mono', 'SF Mono', Monaco, monospace; }
```

## Step 9: Selection Color

```css
::selection {
  background: rgba(59, 130, 246, 0.3);
  color: #ffffff;
}
```

## Step 10: Add Glow Effects (Optional)

For interactive elements that need extra emphasis:

```css
.glow-on-hover:hover {
  box-shadow: 0 0 20px var(--accent-glow);
}

/* Pulsing glow for live data indicators */
@keyframes pulse-glow {
  0%, 100% { box-shadow: 0 0 20px rgba(59, 130, 246, 0.3); }
  50% { box-shadow: 0 0 40px rgba(59, 130, 246, 0.6); }
}
```

## Example Project: Cybersecurity Dashboard

Applying this aesthetic to a SIEM dashboard:

1. **Background tiers:** `#0a0a0a` page, `#141414` alert cards, `#1a1a1a` expanded detail
2. **Accent:** Red (`#ef4444`) for critical alerts, blue (`#3b82f6`) for navigation
3. **Cards:** Threat alerts with severity-colored left borders
4. **Data viz:** Dark Recharts with 5% white grid lines
5. **Tables:** Minimal borders, uppercase headers, colored severity badges

## Example Project: Developer Portfolio

Applying this aesthetic to a personal portfolio:

1. **Background tiers:** `#0a0a0a` base, `#141414` project cards, `#1a1a1a` hover
2. **Accent:** Green (`#22c55e`) for links and tech tags
3. **Cards:** Project cards with 20px radius, hover border glow
4. **Typography:** Inter body + JetBrains Mono for tech stack lists
5. **Animation:** Framer Motion stagger for project grid entrance
