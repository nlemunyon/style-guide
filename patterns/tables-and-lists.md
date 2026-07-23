# Tables & Lists

Data tables, activity timelines, and staggered animated lists.

## Data Tables

### Wedding CRM Table

Full-width table with uppercase headers and hover rows:

```css
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  padding: 0.75rem 1rem;
  text-align: left;
  border-bottom: 1px solid #eee;
}

th {
  font-weight: 500;
  color: #666;
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

tr:hover { background: #fafafa; }
tr.clickable { cursor: pointer; }
tr.clickable:hover { background: #f0f0f0; }
```

**Characteristics:** Subtle bottom borders only (no vertical lines). Uppercase headers create visual hierarchy. Clickable rows get a slightly stronger hover. Clean, spreadsheet-like feel.

### DailyBrief.AI Table (Tailwind)

Dark-mode table with minimal borders:

```css
/* Conceptual CSS equivalent of Tailwind classes used */
table { width: 100%; border-collapse: collapse; }

th {
  padding: 0.5rem 1rem;
  text-align: left;
  font-size: 0.75rem;
  font-weight: 500;
  color: #a3a3a3;  /* text-secondary */
  text-transform: uppercase;
  letter-spacing: 0.05em;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

td {
  padding: 0.75rem 1rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  color: #ffffff;
}

tr:hover { background: rgba(255, 255, 255, 0.02); }
```

**Characteristics:** Near-invisible borders (5% white opacity). Very subtle hover state. Headers use text-secondary color. Works on `#0a0a0a` background.

### Chat Markdown Table (Wedding CRM)

Tables rendered inside chat message bubbles:

```css
.msg-bubble table {
  width: 100%;
  border-collapse: collapse;
  margin: 12px 0;
  font-size: 13px;
}

.msg-bubble th, .msg-bubble td {
  border: 1px solid #e5e7eb;
  padding: 8px 12px;
  text-align: left;
}

.msg-bubble th {
  background: #f9fafb;
  font-weight: 600;
}

.msg-bubble tr:nth-child(even) { background: #fafafa; }
```

**Characteristics:** Full borders (all sides) for clarity in chat context. Striped rows for readability. Smaller font (13px) to fit within message width.

### Chat Markdown Table (Vector RAG)

Tables rendered inside assistant answers — bottom-border rows with a faint header fill and zebra striping tuned for the dark surface:

```css
.markdown th {
  background: rgba(255,255,255,0.04);
  font-size: 0.875rem; font-weight: 600;
  padding: 8px 12px; border-bottom: 1px solid #2a2a2a;
}
.markdown td { padding: 8px 12px; color: #bbb; border-bottom: 1px solid rgba(255,255,255,0.05); }
.markdown tr:nth-child(even) { background: rgba(255,255,255,0.02); }
.markdown tr:hover { background: rgba(255,255,255,0.04); }
/* outer table border: 1px solid #333 */
```

**Characteristics:** Unlike Wedding CRM's fully-bordered chat tables, Vector RAG uses bottom-borders + zebra striping (like the dashboard tables) for a lighter, more data-dense read.

### Guide Table (Wedding CRM)

Styled tables inside the user guide modal:

```css
.guide-content .field-table {
  width: 100%;
  border-collapse: collapse;
  margin: 12px 0;
  font-size: 13px;
  background: #fff;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 1px 3px rgba(0,0,0,0.05);
}

.guide-content .field-table th {
  background: #7d8b6a;
  color: #fff;
  font-weight: 500;
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 0.3px;
}

.guide-content .field-table tr:hover td { background: #f8f9f7; }
```

**Characteristics:** Rounded container with overflow:hidden. Accent-colored header row. White background with subtle hover.

## Activity Timeline (Wedding CRM)

Vertical timeline with colored activity dots:

```css
.timeline {
  position: relative;
  padding-left: 2rem;
}

.timeline::before {
  content: '';
  position: absolute;
  left: 0.5rem;
  top: 0;
  bottom: 0;
  width: 2px;
  background: #e9ecef;
}

.timeline-item {
  position: relative;
  padding-bottom: 1.5rem;
}

.timeline-item::before {
  content: '';
  position: absolute;
  left: -1.5rem;
  top: 0.25rem;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #7d8b6a;  /* Default: sage green */
}

/* Activity type colors */
.timeline-item.email::before  { background: #4CAF50; }  /* Green */
.timeline-item.note::before   { background: #2196F3; }  /* Blue */
.timeline-item.status::before { background: #FF9800; }  /* Orange */

.timeline-date {
  font-size: 0.75rem;
  color: #999;
  margin-bottom: 0.25rem;
}

.timeline-content {
  background: #f8f9fa;
  padding: 0.75rem 1rem;
  border-radius: 8px;
}
```

**Characteristics:** Thin vertical line with colored dots per activity type. Content cards with soft background. Date above each entry.

## Staggered Animated Lists (Not A Doc AI)

Framer Motion stagger pattern for list rendering:

```jsx
import { motion } from 'framer-motion'
import { staggerContainer, listItem } from '../utils/motion'

function OrderList({ orders }) {
  return (
    <motion.div
      variants={staggerContainer(0.04)}
      initial="hidden"
      animate="visible"
    >
      {orders.map(order => (
        <motion.div key={order.id} variants={listItem}>
          {/* Order card content */}
        </motion.div>
      ))}
    </motion.div>
  )
}
```

The `staggerContainer` delays each child by 40ms, and each `listItem` fades in while sliding up 6px over 200ms.

## Leaderboard Lists (DailyBrief.AI)

Ranked lists for event types, trending actors, and recent events:

- Each item: rank number + label + count/metric
- Color-coded bars or indicators
- Truncated text with ellipsis for long names
- Top 10 items shown by default

## Rank-Bar Lists (Vector RAG)

The dashboard's ranking widgets are a grid-aligned bar list — label, an inline `7px` accent bar on a `--hi` track, and a mono value:

```css
.rank-row  { display: grid; grid-template-columns: minmax(0,1.4fr) 1.6fr auto; align-items: center; }
.rank-bar  { height: 7px; border-radius: 4px; background: var(--hi); }          /* #1a1a1a track */
.rank-bar > i { display: block; height: 100%; border-radius: 4px; background: var(--accent); }
.rank-val  { font-family: var(--font-mono); font-size: 13px; font-weight: 600; text-align: right; }
```

Used three-up in the analysis row (fatalities by country, event-type mix, conflict dyads) and for actor activity — a denser cousin of DailyBrief's leaderboard. Alerts and history rows likewise use bottom-border `1px var(--line-2)` separators rather than full borders.

## Table Comparison

| Property | Wedding CRM | DailyBrief.AI | Chat Tables | Vector RAG |
|----------|-------------|---------------|-------------|-----------|
| Borders | Bottom only (`#eee`) | Bottom only (5% white) | All sides (`#e5e7eb`) | Bottom only + `1px #333` outer |
| Header style | Uppercase, gray | Uppercase, secondary | Bold, light bg | Bold, `4%` white fill |
| Hover | `#fafafa` | 2% white | — | `4%` white |
| Font size | Default | Compact | 13px | `text-sm` |
| Striping | No | No | Even rows | Even rows (`2%` white) |
| Radius | None | None | 8px container | None (rank cards `8px`) |

## How to Apply Tables

### For a CRM or admin tool:
- Bottom-border-only with uppercase headers
- Letter-spacing on headers for structure
- Clickable rows with stronger hover color
- Wrap in rounded containers for guide/modal contexts

### For a dark dashboard:
- Near-invisible borders (5% white)
- Subtle hover (2% white tint)
- Uppercase headers in text-secondary color
- Keep font sizes compact for density

### For a timeline:
- Vertical line with colored dots per activity type
- Date label above content
- Content in soft-background cards (8px radius)
- 1.5rem bottom padding between items

### For animated lists:
- Use stagger containers with 40ms delay per child
- Each item: fade in + slide up 6px
- Keep durations at 200ms with deceleration easing
- Works for any list: orders, results, notifications
- Vector RAG uses the identical `staggerContainer(0.04)` + `listItem` variants

### For dashboard rankings:
- Grid-align label · inline bar · mono value (Vector RAG rank-row)
- 7px accent bar on a dark track, `4px` radius
- Bottom-border separators (not full borders) for alert/history rows
