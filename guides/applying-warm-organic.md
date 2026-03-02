# Applying Warm Organic

How to apply the warm, organic aesthetic (used by the Wedding CRM) to any project. This guide covers tinted whites, natural accent colors, premium density, and component styling for light-mode professional tools.

## The Core Principle

Warm organic design uses tinted whites, natural colors, and generous spacing to create a premium, approachable feel. It avoids stark black-on-white contrast in favor of softer tones. Shadows create depth instead of borders.

## Step 1: Define Your Background Palette

Start with a warm-tinted background instead of pure white:

```css
:root {
  --bg-page: #f5f7f3;        /* Warm sage-tinted white */
  --bg-surface: #ffffff;      /* Pure white for cards */
  --bg-elevated: #f8f9fa;     /* Slightly warm gray for nested elements */
  --bg-hover: #fafafa;        /* Subtle hover state */
  --bg-active: #f0f0f0;       /* Stronger active/click state */
}
```

**Alternatives:**
- Pink-tinted: `#f7f3f5` → `#ffffff` → `#faf8f9`
- Blue-tinted: `#f3f5f7` → `#ffffff` → `#f8f9fa`
- Sand/cream: `#f7f5f3` → `#ffffff` → `#faf9f8`

The tint should be barely perceptible — just enough to feel warmer than sterile white.

## Step 2: Choose a Natural Accent

Pick a desaturated, nature-inspired accent color:

```css
:root {
  --accent: #7d8b6a;          /* Sage green — primary buttons, active states */
  --accent-dark: #6b7f5c;     /* Darker — hover states */
  --accent-deep: #5a6b4a;     /* Deepest — text on accent backgrounds */
  --accent-light: #e8eee3;    /* Very light — hover backgrounds */
  --accent-ring: rgba(125, 139, 106, 0.15);  /* Focus ring */
}
```

**Good natural accent options:**

| Color | Hex | Mood |
|-------|-----|------|
| Sage green | `#7d8b6a` | Nature, wellness, organic |
| Dusty rose | `#b07d7d` | Beauty, warmth, elegance |
| Slate blue | `#6a7d8b` | Calm, professional, trust |
| Warm clay | `#8b7d6a` | Earth, craft, heritage |
| Lavender | `#7d6a8b` | Creative, gentle, premium |

## Step 3: Set Up Text Colors

```css
:root {
  --text-primary: #333333;    /* Headings, body text */
  --text-secondary: #666666;  /* Labels, descriptions */
  --text-muted: #999999;      /* Timestamps, hints */
  --text-on-accent: #ffffff;  /* Text on accent-colored backgrounds */
}
```

## Step 4: Define Your Shadow Scale

Shadows create depth in light mode (unlike dark mode which uses borders):

```css
:root {
  --shadow-card: 0 2px 10px rgba(0, 0, 0, 0.05);
  --shadow-stat: 0 1px 3px rgba(0, 0, 0, 0.1);
  --shadow-float: 0 20px 60px rgba(0, 0, 0, 0.15);
  --shadow-focus: 0 0 0 3px var(--accent-ring);
}
```

## Step 5: Style Your Cards

```css
.card {
  background: var(--bg-surface);
  border-radius: 12px;
  box-shadow: var(--shadow-card);
  padding: 1.5rem;
  margin-bottom: 1.5rem;
}

/* No borders needed — shadow provides depth */
/* Optional accent: */
.card h3 {
  font-size: 1rem;
  font-weight: 500;
  color: var(--text-secondary);
}
```

## Step 6: Navbar with Gradient

```css
.navbar {
  background: linear-gradient(135deg, var(--accent) 0%, var(--accent-dark) 100%);
  color: white;
  padding: 0.75rem 1.5rem;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.navbar h1 {
  font-weight: 300;       /* Light weight for elegance */
  letter-spacing: 2px;    /* Wide spacing for brand feel */
}

.navbar a {
  color: white;
  opacity: 0.9;
  border-radius: 4px;
  padding: 0.4rem 0.8rem;
}

.navbar a:hover { opacity: 1; background: rgba(255, 255, 255, 0.1); }
.navbar a.active { background: rgba(255, 255, 255, 0.2); opacity: 1; }
```

## Step 7: Pill-Shaped Buttons

```css
.btn {
  border-radius: 25px;          /* Full pill shape */
  padding: 0.6rem 1.5rem;
  font-size: 0.9rem;
  transition: all 0.2s;
}

.btn-primary {
  background: var(--accent);
  color: white;
}

.btn-primary:hover {
  background: var(--accent-dark);
}

.btn-outline {
  background: transparent;
  border: 1px solid var(--accent);
  color: var(--accent);
}

.btn-outline:hover {
  background: var(--accent);
  color: white;
}
```

## Step 8: Form Inputs with Accent Focus

```css
input, select, textarea {
  padding: 0.6rem 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 0.9rem;
  width: 100%;
  font-family: inherit;
}

input:focus, select:focus, textarea:focus {
  outline: none;
  border-color: var(--accent);
  box-shadow: var(--shadow-focus);
}
```

## Step 9: Semantic Color System

Use pastel backgrounds with dark same-hue text:

```css
:root {
  --success-bg: #d4edda;  --success-text: #155724;
  --warning-bg: #fff3cd;  --warning-text: #856404;
  --error-bg: #f8d7da;    --error-text: #721c24;
  --info-bg: #cce5ff;     --info-text: #004085;
}
```

## Step 10: Filter Tabs

```css
.filters {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.filter-tab {
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.85rem;
  background: transparent;
  color: var(--text-secondary);
  cursor: pointer;
}

.filter-tab:hover { background: var(--accent-light); }
.filter-tab.active { background: var(--accent); color: white; }
```

## Example Project: Day Spa Booking System

1. **Background:** `#f7f5f3` (warm cream) for page, white cards
2. **Accent:** Dusty rose `#b07d7d` for buttons and active states
3. **Cards:** Service cards with large light-weight pricing numbers
4. **Navbar:** Rose gradient with light-weight brand name
5. **Badges:** Pipeline status (inquiry → consulted → booked → completed)
6. **Tables:** Appointment schedules with colored status badges

## Example Project: Artisan E-commerce

1. **Background:** `#f5f5f3` (warm gray) for page, white product cards
2. **Accent:** Warm clay `#8b7d6a` for buttons and category tabs
3. **Cards:** Product cards with 12px radius, subtle shadow, clean images
4. **Navbar:** Clay gradient with uppercase thin brand name
5. **Filters:** Pill-shaped category filters
6. **Forms:** Checkout form with accent focus rings

## Example Project: Architecture Firm Portfolio

1. **Background:** `#f3f5f7` (cool blue-tinted) for page, white project cards
2. **Accent:** Slate blue `#6a7d8b` for navigation and CTAs
3. **Cards:** Large project images with thin overlay descriptions
4. **Timeline:** Project history with colored milestone dots
5. **Typography:** System font stack, 300 weight for headings, generous line-height
