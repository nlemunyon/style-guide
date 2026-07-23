# Animation & Motion

CSS keyframes, Framer Motion presets, easing functions, and duration standards across all five sites.

## Animation Libraries

| Site | Library | Approach |
|------|---------|----------|
| Wedding CRM | CSS only | Keyframes + transitions |
| DailyBrief.AI | CSS + Tailwind keyframes | Config-defined animations |
| Map Creator | CSS only | Transitions + keyframes |
| Not A Doc AI | Framer Motion + CSS | Declarative variants + keyframes |
| Vector RAG | Framer Motion + SVG + CSS | Variants + SVG path/pulse animation + keyframes |

## CSS Keyframes

### Spin (Shared)

Used by Wedding CRM and Map Creator for loading spinners:

```css
@keyframes spin {
  to { transform: rotate(360deg); }
}

/* Wedding CRM: 0.7s linear infinite */
/* Map Creator: 1s linear infinite */
```

### Fade In

```css
/* DailyBrief.AI (Tailwind config) */
@keyframes fade-in {
  0% { opacity: 0; transform: translateY(10px); }
  100% { opacity: 1; transform: translateY(0); }
}
/* Duration: 0.3s ease-out */

/* Not A Doc AI */
@keyframes fadeIn {
  0% { opacity: 0; }
  100% { opacity: 1; }
}
/* Duration: 0.2s ease-out */

/* Wedding CRM */
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
/* Duration: 0.2s ease */
```

### Fade In Up

```css
/* Not A Doc AI */
@keyframes fadeInUp {
  0% { opacity: 0; transform: translateY(8px); }
  100% { opacity: 1; transform: translateY(0); }
}
/* Duration: 0.3s ease-out */
```

### Slide Up (Wedding CRM)

```css
@keyframes slideUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
/* Duration: 0.25s ease — used for guide modal entrance */
```

### Pulse Glow (DailyBrief.AI)

```css
@keyframes pulse-glow {
  0%, 100% { box-shadow: 0 0 20px rgba(59, 130, 246, 0.3); }
  50% { box-shadow: 0 0 40px rgba(59, 130, 246, 0.6); }
}
/* Duration: 2s ease-in-out infinite */
```

### Pulse Soft (Not A Doc AI)

```css
@keyframes pulseSoft {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.7; }
}
/* Duration: 2s ease-in-out infinite */
```

### Pulse Ring (Wedding CRM)

```css
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
/* Duration: 2.5s ease-out infinite — chat toggle attention ring */
```

### Typing Indicators

```css
/* Wedding CRM */
@keyframes typingPulse {
  0%, 60%, 100% { transform: scale(0.8); opacity: 0.4; }
  30% { transform: scale(1); opacity: 1; }
}
/* Duration: 1.4s, stagger: 0s / 0.15s / 0.3s */

/* Not A Doc AI */
@keyframes typing-pulse {
  0%, 60%, 100% { opacity: 0.4; transform: scale(1); }
  30% { opacity: 1; transform: scale(1.1); }
}
/* Duration: 1.4s, stagger: 0s / 0.2s / 0.4s */
```

### Infinite Scroll (Map Creator)

```css
@keyframes scroll {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}
/* Duration: 30s linear infinite — pauses on hover */
```

### Map Ping + Ghost Shimmer (Vector RAG)

The dashboard signals live/fresh data with an expanding box-shadow ping, and loading cards sweep a shimmer:

```css
/* Fresh event dot / live indicator */
@keyframes ap2ping {
  0%        { box-shadow: 0 0 0 0  color-mix(in srgb, var(--pc) 55%, transparent); }
  70%, 100% { box-shadow: 0 0 0 11px transparent; }
}   /* 2.6s ease-out infinite (live dot: 2s) */

/* Skeleton shimmer on .card::after while loading */
@keyframes ghostSweep {
  from { transform: translateX(-100%); }
  to   { transform: translateX(100%); }
}   /* 1.25s ease-in-out infinite; gradient = accent 9% → transparent */
```

The landing map's pulses/arcs are **not** CSS keyframes — they're Framer Motion on SVG elements (see below).

## Framer Motion Presets (Not A Doc AI)

Not A Doc AI centralizes all animation variants in a `motion.js` utility file:

```js
const EASINGS = {
  smoothOut: [0, 0, 0.2, 1],  // Aggressive deceleration
}

// Fade in (simplest)
export const fadeIn = {
  hidden: { opacity: 0 },
  visible: { opacity: 1, transition: { duration: 0.2 } },
  exit: { opacity: 0, transition: { duration: 0.15 } },
}

// Fade in + slide up
export const fadeInUp = {
  hidden: { opacity: 0, y: 8 },
  visible: {
    opacity: 1, y: 0,
    transition: { duration: 0.25, ease: EASINGS.smoothOut },
  },
  exit: { opacity: 0, y: -4, transition: { duration: 0.15 } },
}

// Stagger container (wraps children)
export const staggerContainer = (staggerDelay = 0.04, delayChildren = 0) => ({
  hidden: { opacity: 1 },
  visible: {
    opacity: 1,
    transition: { staggerChildren: staggerDelay, delayChildren },
  },
})

// Individual list item
export const listItem = {
  hidden: { opacity: 0, y: 6 },
  visible: {
    opacity: 1, y: 0,
    transition: { duration: 0.2, ease: EASINGS.smoothOut },
  },
}

// Chat messages
export const userMessage = {
  hidden: { opacity: 0, x: 16, scale: 0.98 },
  visible: {
    opacity: 1, x: 0, scale: 1,
    transition: { duration: 0.25, ease: EASINGS.smoothOut },
  },
}

export const assistantMessage = {
  hidden: { opacity: 0, y: 8 },
  visible: {
    opacity: 1, y: 0,
    transition: { duration: 0.25, ease: EASINGS.smoothOut },
  },
}

// Micro-interactions
export const buttonHover = { y: -1, transition: { duration: 0.15 } }
export const buttonTap = { scale: 0.98, transition: { duration: 0.1 } }
```

**Vector RAG uses this exact variant library** (same `smoothOut` easing, same `userMessage`/`assistantMessage`/`fadeInUp`/`staggerContainer`/`buttonHover`/`buttonTap`), plus `slideInLeft/Right`, `scaleIn`, `modalOverlay`/`modalContent`, and a `sidebarVariants` that animates `width: 280 ↔ 0`.

## Framer Motion on SVG (Vector RAG)

Vector RAG's signature is a landing-map animation built by animating **SVG attributes** with Framer Motion — arcs draw via `strokeDashoffset`, dots breathe via `opacity`, rings expand via `scale`. One 45s loop across 15 hotspots (`stepDuration = 3s`):

```jsx
// Arc: draws in over 1s, holds, fades — 2s active window, repeats after 43s
<motion.path stroke="#3a6d8c" strokeWidth={0.8} pathLength={1} strokeDasharray="1"
  animate={{ strokeDashoffset: [1, 0, 0], opacity: [0, 0.35, 0] }}
  transition={{ duration: 2, times: [0, 0.5, 1], ease: 'easeInOut', delay: i*3, repeat: Infinity, repeatDelay: 43 }} />

// Ring: expands + fades, synced to its incoming arc via pulseDelay = (i-1)*3 + 1
<motion.circle r={8} fill="none" stroke="#3a6d8c"
  initial={{ scale: 0.3, opacity: 0.45 }} animate={{ scale: 1.8, opacity: 0 }}
  transition={{ duration: 2, ease: 'easeOut', delay: pulseDelay, repeat: Infinity, repeatDelay: 43 }} />
```

A `useReducedMotion()` guard strips every arc/ring and renders flat static dots — the accessible fallback for the whole effect. See [Maps & Data Viz](maps-and-data-viz.md#animated-svg-world-map-vector-rag) for the full projection.

### Usage Pattern

```jsx
<motion.div
  variants={staggerContainer()}
  initial="hidden"
  animate="visible"
>
  {items.map(item => (
    <motion.div key={item.id} variants={listItem}>
      {item.content}
    </motion.div>
  ))}
</motion.div>
```

## Hover Transitions

| Element | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI | Vector RAG |
|---------|-------------|---------------|-------------|--------------|------------|
| Card | — | Border brightens | `translateY(-8px)` | Border brightens | Border brightens (8%→14%) |
| Button | bg-color change | — | `translateY(-2px)` + shadow boost | `y: -1` (FM) | `y: -1` (FM) |
| Gallery item | — | — | `translateY(-4px)` + shadow | — | — |
| Chat toggle | `translateY(-3px) scale(1.05)` | — | — | — | — |
| Nav link | bg highlight | — | — | — | text-color shift |
| Chart bar | — | — | — | — | opacity 0.42 → 1.0 |

## Duration Standards

| Duration | Usage | Sites |
|----------|-------|-------|
| 0.1s | Button tap/press | Not A Doc AI |
| 0.15s | Subtle UI transitions, hover states | Wedding CRM, Not A Doc AI |
| 0.2s | Default transitions, fade-in | All sites |
| 0.25s | Slide-up, message entrance | Wedding CRM, Not A Doc AI |
| 0.3s | Fade-in-up, opacity transitions | DailyBrief, Map Creator, Not A Doc AI |
| 0.7s | Spinner rotation | Wedding CRM |
| 1s | Spinner rotation | Map Creator |
| 1.4s | Typing indicator cycle | Wedding CRM, Not A Doc AI |
| 2s | Pulse animations | DailyBrief, Not A Doc AI, Vector RAG (map dot/ring, live dot) |
| 2.5s | Attention ring pulse | Wedding CRM |
| 2.6s | Fresh-event ping | Vector RAG |
| 7s | Welcome suggestion carousel | Vector RAG |
| 30s | Banner infinite scroll | Map Creator |
| 45s | Landing map hotspot loop | Vector RAG |

## Easing Functions

| Easing | CSS Value | Usage |
|--------|-----------|-------|
| `ease` | `ease` | General transitions (Wedding CRM) |
| `ease-out` | `ease-out` | Enter animations (all sites) |
| `ease-in-out` | `ease-in-out` | Pulse/glow loops |
| `linear` | `linear` | Spinners, infinite scroll |
| `smoothOut` | `cubic-bezier(0, 0, 0.2, 1)` | Framer Motion (Not A Doc AI, Vector RAG) |
| Custom | `cubic-bezier(0.4, 0, 0.2, 1)` | Chat toggle (Wedding CRM) |

> **Reduced motion:** Vector RAG ships a global `@media (prefers-reduced-motion: reduce)` rule that clamps all animation/transition durations to `0.01ms`, and its landing map has a dedicated `useReducedMotion()` fallback that removes arcs/rings entirely. When adding signature motion, always design the static fallback alongside it.

## How to Apply Motion

### For a professional tool:
- Keep durations at 0.15-0.2s for responsive feel
- Use `ease-out` for entrances, `ease` for state changes
- Avoid dramatic transforms — subtle opacity changes are sufficient
- Reserve animations for attention (notifications, new data)

### For a data dashboard:
- Prefer `fade-in` (0.3s) for new data loading
- Use `pulse-glow` for live data indicators
- Avoid stagger animations on frequently-updating data
- Keep transitions at 200ms (Tailwind default)

### For a creative tool:
- Use `translateY` on hover for tactile feedback
- Apply longer durations (0.3s) for smooth gallery interactions
- Infinite scroll for showcase/banner elements
- Progress animations for long-running processes

### For a chat interface:
- Use directional entrance: user messages from right (`x: 16`), assistant from below (`y: 8`)
- Stagger child elements at 40ms intervals
- Typing indicator with 3 dots, 1.4s cycle, staggered 150-200ms
- Smooth scroll-to-bottom after new messages
