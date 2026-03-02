# Badges & Status

Status pipeline badges, semantic indicators, count badges, and stack count badges.

## Semantic Badges (Wedding CRM)

Color-coded badges for categorical information:

```css
.badge {
  display: inline-block;
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 500;
}

.badge-green  { background: #d4edda; color: #155724; }
.badge-yellow { background: #fff3cd; color: #856404; }
.badge-red    { background: #f8d7da; color: #721c24; }
.badge-blue   { background: #cce5ff; color: #004085; }
.badge-gray   { background: #e9ecef; color: #495057; }
.badge-purple { background: #e2d4f0; color: #5a3d7a; }
```

**Pattern:** Pastel background with dark text of the same hue. High contrast for readability on white surfaces.

## Status Pipeline (Wedding CRM)

A complete sales pipeline with distinct colors per stage:

```css
.status-lead      { background: #e9ecef; color: #495057; }  /* Gray - new */
.status-contacted { background: #cce5ff; color: #004085; }  /* Blue - reached out */
.status-quoted    { background: #fff3cd; color: #856404; }  /* Yellow - proposal sent */
.status-hold      { background: #e2e3e5; color: #6c757d; }  /* Muted gray - paused */
.status-booked    { background: #d4edda; color: #155724; }  /* Green - confirmed */
.status-completed { background: #c3e6cb; color: #155724; }  /* Deeper green - done */
.status-lost      { background: #f8d7da; color: #721c24; }  /* Red - lost deal */
```

The progression (gray → blue → yellow → green → deeper green) creates a natural visual flow from cold leads to warm completions, with red as the off-ramp.

## Dark Mode Badges (Not A Doc AI)

Muted-opacity backgrounds with bright text:

```css
.badge {
  display: inline-flex;
  align-items: center;
  gap: 0.375rem;
  padding: 0.25rem 0.625rem;
  border-radius: 100px;
  font-size: 0.75rem;
  font-weight: 500;
}

.badge-accent {
  background-color: rgba(59, 130, 246, 0.15);
  color: #3b82f6;
}

.badge-success {
  background-color: rgba(74, 222, 128, 0.15);
  color: #4ade80;
}

.badge-warning {
  background-color: rgba(251, 191, 36, 0.15);
  color: #fbbf24;
}
```

**Pattern:** 15% opacity of the semantic color as background, full-brightness color as text. The `inline-flex` + `gap` allows pairing text with icons or dots.

## Stack Count Badge (Map Creator)

Badge showing number of items in a gallery stack:

```css
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

Displays "+N" (e.g., "+3") to indicate additional items behind the top card.

## Count Badge (Wedding CRM)

Pill-shaped gallery count:

```css
.stack-count {
  font-size: 0.75rem;
  color: #636966;
  background: rgba(255, 255, 255, 0.03);
  padding: 3px 10px;
  border-radius: 100px;
  border: 1px solid rgba(160, 170, 160, 0.12);
}
```

## Navigation Badge (Wedding CRM)

Red notification count on nav items:

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

## Context Badge (Wedding CRM Chat)

Inline badge showing contextual information:

```css
.context-badge {
  background: #eef0eb;
  color: #5a6b4a;
  padding: 3px 8px;
  border-radius: 4px;
  font-size: 10px;
  font-weight: 500;
  margin-left: 8px;
  white-space: nowrap;
}
```

Displays the current page context (e.g., "Viewing: Sarah Johnson") inside the chat header.

## Model Status Dot (Wedding CRM)

Tiny dot indicating connection state:

```css
.model-status {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #10b981;  /* green = online */
}

.model-status.offline {
  background: #ef4444;  /* red = offline */
}
```

## Badge Comparison Table

| Property | Wedding CRM (Light) | Not A Doc AI (Dark) | Map Creator |
|----------|---------------------|---------------------|-------------|
| Background | Pastel tint | 15% opacity accent | Solid accent |
| Text | Dark tint | Bright accent | Dark bg color |
| Radius | `20px` | `100px` (full pill) | `12px` |
| Size | `0.75rem` | `0.75rem` | `0.85rem` |
| Weight | 500 | 500 | 600 |

## How to Apply Badges

### For a light-mode CRM or admin tool:
- Use pastel background + dark same-hue text
- Define a full pipeline progression (gray → blue → yellow → green → red)
- 20px radius for pill shape
- Red notification badges on nav items

### For a dark-mode data app:
- Use 15% opacity accent color as background
- Full-brightness color as text
- `border-radius: 100px` for perfect pills
- `inline-flex` with `gap` for icon+text badges

### For a gallery or content tool:
- Absolute-positioned count badges on card corners
- Solid accent background with dark text for high visibility
- "+N" format for additional item counts
