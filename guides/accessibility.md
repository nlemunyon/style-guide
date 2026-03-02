# Accessibility

Reduced motion preferences, focus management, contrast considerations, and keyboard navigation patterns.

## Reduced Motion

Not A Doc AI implements the recommended `prefers-reduced-motion` media query:

```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

This effectively disables all animations and transitions for users who have enabled "Reduce motion" in their OS accessibility settings.

### What to Apply

Every site should include this media query. It affects:
- CSS keyframe animations (spinners, pulses, scrolling banners)
- CSS transitions (hover effects, color changes)
- Framer Motion (use `useReducedMotion()` hook additionally)

### Framer Motion Reduced Motion

For Not A Doc AI's Framer Motion animations, also use the hook:

```jsx
import { useReducedMotion } from 'framer-motion'

function AnimatedComponent() {
  const prefersReducedMotion = useReducedMotion()

  return (
    <motion.div
      initial={prefersReducedMotion ? false : "hidden"}
      animate="visible"
      variants={fadeInUp}
    >
      {/* content */}
    </motion.div>
  )
}
```

## Focus Management

### Input Focus Rings

All four sites style focus states explicitly, removing the default outline:

```css
/* Wedding CRM - Sage green focus ring */
input:focus {
  outline: none;
  border-color: #7d8b6a;
  box-shadow: 0 0 0 3px rgba(125, 139, 106, 0.15);
}

/* Map Creator - Forest green focus ring */
input:focus {
  outline: none;
  border-color: #7dad7d;
  box-shadow: 0 0 0 3px rgba(125, 173, 125, 0.1);
}

/* Not A Doc AI - Blue focus (implicit via Tailwind focus: utilities) */
/* focus:border-accent focus:ring-2 focus:ring-accent-muted */
```

### Recommendation

When removing `outline`, always provide a visible alternative:

```css
/* Good: Custom focus ring */
*:focus {
  outline: none;
  box-shadow: 0 0 0 3px var(--accent-ring);
}

/* Better: Only remove for mouse users */
*:focus:not(:focus-visible) {
  outline: none;
  box-shadow: none;
}

*:focus-visible {
  outline: none;
  box-shadow: 0 0 0 3px var(--accent-ring);
}
```

`:focus-visible` shows the focus ring only for keyboard navigation, not mouse clicks.

## Keyboard Navigation

### Chat Keyboard Shortcuts (Wedding CRM)

| Shortcut | Action |
|----------|--------|
| `Cmd/Ctrl+K` | Toggle chat open/closed |
| `Escape` | Minimize expanded view or close chat |
| `Enter` | Send message |
| `Shift+Enter` | New line in message |

These are documented in the user guide and shown as a keyboard hint on the toggle button.

### Chat Input (Not A Doc AI)

```jsx
const handleKeyDown = (e) => {
  if (e.key === 'Enter' && !e.shiftKey) {
    e.preventDefault()
    handleSend()
  }
}
```

### Modal Dismiss

All modals should close on `Escape` key:

```javascript
document.addEventListener('keydown', (e) => {
  if (e.key === 'Escape') {
    closeModal()
  }
})
```

## Color Contrast

### Dark Mode Contrast Ratios

| Combination | Ratio | WCAG | Usage |
|-------------|-------|------|-------|
| White on `#0a0a0a` | 19.3:1 | AAA | Primary text |
| `#a3a3a3` on `#0a0a0a` | 8.6:1 | AAA | Secondary text |
| `#666666` on `#0a0a0a` | 4.0:1 | AA | Tertiary text |
| `#3b82f6` on `#0a0a0a` | 4.6:1 | AA | Accent links |
| White on `#3b82f6` | 4.2:1 | AA | Button text |

### Light Mode Contrast Ratios

| Combination | Ratio | WCAG | Usage |
|-------------|-------|------|-------|
| `#333` on `#ffffff` | 12.6:1 | AAA | Primary text |
| `#666` on `#ffffff` | 5.7:1 | AAA | Secondary text |
| `#999` on `#ffffff` | 2.8:1 | Fails AA | Muted text (decorative only) |
| `#155724` on `#d4edda` | 7.1:1 | AAA | Success badge |
| White on `#7d8b6a` | 3.8:1 | AA Large | Button text |

### Recommendations

- Muted text (`#999` in light mode, `#666` in dark mode) falls below WCAG AA for small text. Use only for decorative elements, timestamps, or text paired with other visual indicators.
- Badge color combinations all pass AA for the larger badge text size.
- Primary and secondary text combinations pass AAA in both modes.

## Interactive Targets

### Minimum Touch Targets

| Element | Size | Site |
|---------|------|------|
| Chat toggle | 60×60px (54px mobile) | Wedding CRM |
| Icon buttons | 32×32px | Wedding CRM |
| Filter tabs | ~44px height (0.5rem + 1rem padding + text) | Wedding CRM |
| Theme cards | 50px height | Map Creator |
| Slider thumb | 16×16px | Map Creator |

**Recommendation:** All interactive targets should be at least 44×44px for touch accessibility (WCAG 2.5.8). The slider thumb (16px) is below this — consider adding a transparent hit area:

```css
input[type="range"]::-webkit-slider-thumb {
  width: 16px;
  height: 16px;
  /* Add invisible padding for touch */
  border: 14px solid transparent;
  background-clip: padding-box;
}
```

## Semantic HTML

### Heading Hierarchy

All sites should maintain proper heading order (h1 → h2 → h3) without skipping levels. The Wedding CRM guide modal does this well:

- `h2` for the modal title
- `h3` for section headers
- `h4` for subsection headers

### ARIA Attributes

For dynamic content (chat messages, loading states), add ARIA attributes:

```jsx
{/* Live region for new messages */}
<div role="log" aria-live="polite" aria-label="Chat messages">
  {messages.map(msg => /* ... */)}
</div>

{/* Loading state */}
<div role="status" aria-live="polite">
  {isLoading && <span>Generating response...</span>}
</div>

{/* Modal */}
<div role="dialog" aria-modal="true" aria-labelledby="modal-title">
  <h2 id="modal-title">User Guide</h2>
</div>
```

## Checklist for New Projects

- [ ] Add `prefers-reduced-motion` media query
- [ ] Add `useReducedMotion()` hook if using Framer Motion
- [ ] Use `:focus-visible` for keyboard-only focus rings
- [ ] Verify primary text contrast ≥ 4.5:1 (AA)
- [ ] Verify secondary text contrast ≥ 4.5:1 (AA) or mark as decorative
- [ ] Ensure all interactive targets ≥ 44×44px
- [ ] Add `Escape` to close modals
- [ ] Add `aria-live="polite"` to dynamic content regions
- [ ] Maintain proper heading hierarchy
- [ ] Test keyboard navigation through all interactive elements
