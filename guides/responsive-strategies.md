# Responsive Strategies

Per-site breakpoint strategies, mobile adaptations, and responsive patterns.

## Breakpoint Summary

| Site | Primary Breakpoint | Strategy |
|------|-------------------|----------|
| Wedding CRM | `768px` | Stack everything vertically |
| DailyBrief.AI | Sidebar collapse | Sidebar 256px → 64px, filters toggle |
| Map Creator | `900px` | Two-column → single-column |
| Not A Doc AI | — | Fixed panel layout |

## Wedding CRM (768px)

The CRM uses a single breakpoint that converts all multi-column layouts to single-column:

```css
@media (max-width: 768px) {
  /* Navbar: horizontal → vertical */
  .navbar {
    flex-direction: column;
    gap: 1rem;
  }
  .navbar nav {
    flex-wrap: wrap;
    justify-content: center;
  }

  /* Forms: 2-col → 1-col */
  .form-row {
    grid-template-columns: 1fr;
  }

  /* Grids: multi-col → 1-col */
  .grid-2, .grid-3, .grid-4 {
    grid-template-columns: 1fr;
  }
}
```

### Chat Widget Mobile

The chat widget has its own responsive behavior:

```css
@media (max-width: 768px) {
  /* Toggle button: smaller, no keyboard hint */
  .chat-toggle {
    bottom: 16px;
    right: 16px;
    width: 54px;
    height: 54px;
    border-radius: 14px;
  }
  .chat-toggle .kbd-hint { display: none; }

  /* Widget: nearly full-screen */
  .chat-widget {
    width: calc(100vw - 16px);
    height: calc(100vh - 80px);
    bottom: 8px;
    right: 8px;
    border-radius: 12px;
  }

  /* Expanded: hide sidebar on mobile */
  .chat-widget.expanded .chat-sidebar { display: none; }

  /* Content adjustments */
  .chat-message { padding: 14px 16px; }
  .chat-input-area { padding: 8px 12px 10px; }
  .welcome-prompts-grid { grid-template-columns: 1fr; }
}
```

## DailyBrief.AI (Sidebar Collapse)

Instead of a traditional breakpoint, the dashboard uses a collapsible sidebar:

**Expanded (256px):**
- Full logo text
- Icon + label navigation
- Footer with data freshness

**Collapsed (64px):**
- Logo icon only
- Icons only (labels hidden)
- Footer hidden

**Navbar filter toggle:**
- "Simple" mode hides filters entirely
- "Detailed" mode shows country filter + date presets
- User controls the mode — not the viewport

This approach works well for dashboards because:
1. Users on small screens still have all functionality
2. Data-dense content benefits from maximum width
3. The toggle is user-controlled, not viewport-dependent

## Map Creator (900px)

Simple two-column to single-column conversion:

```css
@media (max-width: 900px) {
  .main-content {
    grid-template-columns: 1fr;
  }
}
```

The `auto-fill` grids (theme selector, gallery) are inherently responsive:

```css
/* These auto-adapt without media queries */
.theme-grid {
  grid-template-columns: repeat(auto-fill, minmax(105px, 1fr));
}

.gallery-grid {
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
}
```

## Responsive Grid Patterns

### Auto-fit (Wedding CRM)

```css
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1.5rem;
}
```

Items stretch to fill available space. Good for cards that look fine at any width.

### Auto-fill (Map Creator)

```css
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 24px;
}
```

Items maintain their minimum size, leaving empty columns if space allows. Good for fixed-aspect-ratio content (images, cards).

### Fixed with Breakpoint Override (Wedding CRM)

```css
.grid-3 { grid-template-columns: repeat(3, 1fr); }

@media (max-width: 768px) {
  .grid-3 { grid-template-columns: 1fr; }
}
```

Exact column control with explicit mobile override. Good when you need precise layout at specific sizes.

## Responsive Typography

None of the sites use responsive font sizes (no `clamp()` or media query size changes). Text sizes remain consistent across breakpoints. This works because:

1. The base sizes are already readable on mobile
2. Container widths handle the layout, not font sizes
3. Chat widgets cap content width at 680-720px regardless of viewport

## Responsive Navigation Patterns

| Pattern | Best For | Example |
|---------|----------|---------|
| Stack vertically | Simple navbars | Wedding CRM (768px) |
| Collapse sidebar | Data dashboards | DailyBrief.AI |
| Hide filters | Complex filter bars | DailyBrief.AI "simple" mode |
| No change | Desktop-focused tools | Map Creator |

## How to Choose Your Strategy

### For content management tools (CRM, admin):
- Single 768px breakpoint
- Stack navbar, single-column grids and forms
- Nearly-fullscreen chat on mobile
- Hide non-essential features (keyboard hints, sidebar)

### For data dashboards:
- Collapsible sidebar (user-controlled)
- Toggle for filter visibility
- Keep data tables full-width
- Charts may need dedicated mobile variants

### For creative tools:
- 900px breakpoint for main layout
- Use `auto-fill`/`auto-fit` grids for galleries
- Desktop-first — creative tools are often used on larger screens
- Modal views (gallery, image viewer) work well at any size

### For chat interfaces:
- Widget: `calc(100vw - 16px)` × `calc(100vh - 80px)` on mobile
- Hide sidebar in expanded mode on mobile
- Single-column suggestion prompts
- Reduce padding for more message space
