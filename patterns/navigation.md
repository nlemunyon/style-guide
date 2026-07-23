# Navigation

Sidebars, navbars, tabs, filter pills, and pagination patterns.

## Navbar Patterns

### Gradient Navbar (Wedding CRM)

Horizontal navbar with gradient background and pill-shaped nav links:

```css
.navbar {
  background: linear-gradient(135deg, #7d8b6a 0%, #6b7f5c 100%);
  color: white;
  padding: 0.75rem 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.navbar h1 {
  font-size: 1.5rem;
  font-weight: 300;
  letter-spacing: 2px;
}

.navbar nav {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.navbar nav a {
  color: white;
  text-decoration: none;
  padding: 0.4rem 0.8rem;
  font-size: 0.85rem;
  opacity: 0.9;
  transition: all 0.2s;
  border-radius: 4px;
}

.navbar nav a:hover { opacity: 1; background: rgba(255,255,255,0.1); }
.navbar nav a.active { background: rgba(255,255,255,0.2); opacity: 1; }
```

**User menu separator:**

```css
.navbar .user-menu {
  margin-left: 1rem;
  padding-left: 1rem;
  border-left: 1px solid rgba(255,255,255,0.3);
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
```

### Collapsible Sidebar (DailyBrief.AI)

Fixed left sidebar with collapse/expand toggle:

- **Collapsed:** 64px wide, icon-only navigation
- **Expanded:** 256px wide, full labels visible
- **Transition:** Smooth width animation

Key elements:
- Logo area: "Daily**Brief**.AI" branding with bold emphasis
- Nav items: icon + label, with labels hidden when collapsed
- Active state: blue background + left border + animated indicator dot
- Footer: "Powered by GDELT Project" + data freshness timestamp
- Edge strip: 1.5px clickable area on right edge for toggle

```css
/* Active navigation item (conceptual - implemented in Tailwind) */
.nav-item-active {
  background: rgba(59, 130, 246, 0.1);
  border-left: 2px solid #3b82f6;
  color: #3b82f6;
}
```

### Horizontal Navbar (DailyBrief.AI)

The top navbar includes mode toggle and filter controls:

- **Left:** Simple/Detailed view toggle buttons
- **Right:** Country filter dropdown + Date presets (24h, 7d, 30d, 3m, 6m) + Custom date range
- **Height:** h-16 (64px)
- Filters hide in "simple" mode for a cleaner view

### Header Tab Bar (Vector RAG)

A single `56px` (`h-14`) top header on pure black with a `1px solid #1f1f1f` bottom rule — no left rail. Wordmark + inline tab nav on the left, language + user menu on the right.

```jsx
{/* Wordmark: text-lg font-semibold */}
<h1 style={{ color: '#85d5f7' }}>Vector <span style={{ color: '#5ba8d4' }}>RAG</span></h1>

{/* Tabs: active = subtle raised chip */}
<button className="rounded-md px-3 py-1.5 text-sm text-text-primary"
        style={{ backgroundColor: 'rgba(255,255,255,0.06)', border: '1px solid rgba(255,255,255,0.08)' }}>
  Dashboard
</button>
<button className="rounded-md px-3 py-1.5 text-sm text-text-tertiary hover:text-text-secondary transition-colors">
  Chat
</button>
```

The **user menu** button is transparent with a `1px solid #1f1f1f` border that turns `#5c9ece` with a `rgba(92,158,206,0.08)` fill on hover; its dropdown is `#0d0d0d` / `1px solid #1f1f1f`, `min-w-[140px]`, items `text-xs` hovering to `rgba(255,255,255,0.05)`.

### Collapsible Chat Sidebars (Vector RAG)

Two independent, **user-toggled** panels flank the chat (not breakpoint-driven), each animating width + opacity over `0.25s` ease `[0,0,0.2,1]`:

- **History (left, 280px):** conversation rows `px-2 py-2 rounded-lg`; active `bg-bg-elevated text-text-primary`; idle `text-text-secondary` → hover `bg-bg-elevated/50`; a delete button (`text-error bg-error-muted` on hover) reveals per-row.
- **Documents (right, 400px):** retrieved source blocks `bg-bg-elevated border rounded-xl px-3 py-2.5` with an accent index badge.

Both share a `h-10` header in `text-xs font-medium uppercase tracking-wider`.

## Tab Patterns

### Filter Tabs (Wedding CRM)

Pill-shaped tab buttons for content filtering:

```css
.filters {
  margin-bottom: 1.5rem;
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.filters a, .filters button {
  display: inline-block;
  padding: 0.5rem 1rem;
  text-decoration: none;
  color: #666;
  border-radius: 20px;
  font-size: 0.85rem;
  border: none;
  background: transparent;
  cursor: pointer;
}

.filters a:hover, .filters button:hover {
  background: #e8eee3;
}

.filters a.active, .filters button.active {
  background: #7d8b6a;
  color: white;
}
```

### Date Presets (DailyBrief.AI)

Date range pills in the navbar (implemented with Tailwind):

```jsx
{['24h', '7d', '30d', '3m', '6m'].map(preset => (
  <button
    key={preset}
    className={`px-3 py-1 rounded-lg text-xs font-medium transition-colors
      ${active === preset
        ? 'bg-accent text-white'
        : 'text-text-secondary hover:text-white hover:bg-tertiary'
      }`}
  >
    {preset}
  </button>
))}
```

### News Section Tabs (DailyBrief.AI)

Tab buttons for switching between National/International content with sort mode toggles:

- Active tab: accent color text + bottom border
- Inactive tab: secondary text color
- Sort modes: Most Covered, Most Recent, Most Polar

## Sidebar Chat Sessions (Wedding CRM)

Session list in expanded chat sidebar:

```css
.chat-sidebar {
  width: 260px;
  background: #f7f8f6;
  border-right: 1px solid #e5e7e3;
  display: flex;
  flex-direction: column;
}

.chat-session-item {
  padding: 10px 12px;
  border-radius: 6px;
  cursor: pointer;
  margin-bottom: 2px;
}

.chat-session-item:hover { background: #eef0eb; }
.chat-session-item.active { background: #e0e5d8; }

.chat-session-item .session-title {
  font-size: 13px;
  color: #333;
  font-weight: 500;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.chat-session-item .session-date {
  font-size: 11px;
  color: #888;
}
```

## Navigation Badge (Wedding CRM)

Count badge on navigation items:

```css
.nav-badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-width: 18px;
  height: 18px;
  padding: 0 5px;
  background: #dc3545;
  color: white;
  border-radius: 9px;
  font-size: 0.7rem;
  font-weight: 600;
  margin-left: 4px;
}
```

## Navigation Comparison Table

| Property | Wedding CRM | DailyBrief.AI | Vector RAG |
|----------|-------------|---------------|-----------|
| Type | Top navbar | Left sidebar + top navbar | Top header (tabs) + dual chat sidebars |
| Background | Gradient sage green | Dark (#0a0a0a) | Pure black (#000000) |
| Active indicator | White bg overlay | Blue border + bg tint | Raised chip (6% white bg + border) |
| Collapse | Mobile: stacks vertically | Desktop: 256px → 64px | Chat sidebars user-toggled (280/400px → 0) |
| Filters | Pill tabs below content | Embedded in top navbar | Dashboard filter chips (14px pill) |

## How to Apply Navigation

### For a content management tool:
- Horizontal gradient navbar with white text
- Pill-shaped navigation links
- User menu separated with a border-left divider
- Filter tabs below the navbar for content views

### For a data dashboard:
- Collapsible left sidebar with icon + label
- Active item: accent color border + background tint
- Top navbar for filters and view mode toggles
- Date preset pills for time-range selection
- Hide filters in simplified view mode

### For a chat application:
- Session sidebar (260px) with list of past conversations
- Truncated titles with ellipsis
- Active session highlighted
- New chat button in sidebar header
- Or (Vector RAG): a slim top header with tab nav + two independently toggleable sidebars — history (left) and retrieved sources (right) — each animating width/opacity rather than snapping
