# Style Guide

Design system documentation for five production web applications. Each app has a distinctive aesthetic — from warm organic CRMs to ultra-dark intelligence dashboards. This repo captures the design decisions, tokens, and component patterns in enough detail for a designer or developer to apply them to entirely different project types.

## Who This Is For

- **Designers** adapting these aesthetics to new products
- **Developers** building new apps that should feel consistent with an existing site
- **Anyone** who wants to understand the "why" behind each design system

## The Five Sites

| Site | Identity | Background | Accent | Mode |
|------|----------|-----------|--------|------|
| [Wedding CRM](sites/wedding-crm.md) | Warm organic, premium service | ![](https://via.placeholder.com/12/f5f7f3/f5f7f3.png) `#f5f7f3` | ![](https://via.placeholder.com/12/7d8b6a/7d8b6a.png) `#7d8b6a` Sage Green | Light |
| [DailyBrief.AI](sites/dailybrief.md) | Ultra-dark intelligence dashboard | ![](https://via.placeholder.com/12/0a0a0a/0a0a0a.png) `#0a0a0a` | ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) `#3b82f6` Blue | Dark |
| [Map Creator](sites/map-creator.md) | Nature-inspired creative tool | ![](https://via.placeholder.com/12/141517/141517.png) `#141517` | ![](https://via.placeholder.com/12/7dad7d/7dad7d.png) `#7dad7d` Forest Green | Dark |
| [Not A Doc AI](sites/not-a-doc-ai.md) | Modern AI chat + data interface | ![](https://via.placeholder.com/12/0a0a0a/0a0a0a.png) `#0a0a0a` | ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) `#3b82f6` Blue | Dark |
| [Vector RAG](sites/vector-rag.md) | Animated-map intel chat + live dashboard | ![](https://via.placeholder.com/12/000000/000000.png) `#000000` | ![](https://via.placeholder.com/12/5c9ece/5c9ece.png) `#5c9ece` Blue | Dark |

## How to Navigate

**By site** — Start with the [sites/](sites/) folder for a complete deep-dive into any single application's design system.

**By pattern** — Use the [patterns/](patterns/) folder to see how cards, buttons, navigation, or other components are handled across all five sites.

**By foundation** — The [foundations/](foundations/) folder covers cross-cutting design tokens (color, typography, spacing, shadows) with side-by-side comparisons.

**By guide** — The [guides/](guides/) folder has step-by-step instructions for applying each aesthetic to a new project.

## Design System Comparison Matrix

| Property | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI | Vector RAG |
|----------|-------------|---------------|-------------|--------------|------------|
| Background | `#f5f7f3` | `#0a0a0a` | `#141517` | `#0a0a0a` | `#000000` |
| Surface | `#ffffff` | `#141414` | `rgba(255,255,255,0.03)` | `#141414` | `#0a0a0a` |
| Accent | `#7d8b6a` | `#3b82f6` | `#7dad7d` | `#3b82f6` | `#5c9ece` |
| Accent Gradient | `135deg #667756→#3d4d2f` | None (flat) | `135deg #5c8a5c→#9dc49d` | None (flat) | None (flat) |
| Font (Body) | System stack | Inter | Inter | Inter | Inter (self-hosted) |
| Font (Mono) | `ui-monospace` | JetBrains Mono | — | JetBrains Mono | JetBrains Mono (self-hosted) |
| Border Radius | `25px` pills, `12px` cards | `12px` cards | `16-18px` cards, `10px` inputs | `20px` cards, `24px` bubbles | `20px` cards, `24px` bubbles, `8px` panels |
| Animation Library | CSS transitions | CSS + Tailwind keyframes | CSS transitions | Framer Motion | Framer Motion + SVG |
| Border Strategy | None (shadow-based) | `1px rgba(255,255,255,0.05)` | `1px rgba(160,170,160,0.12)` | `1px rgba(255,255,255,0.05)` | `1px rgba(255,255,255,0.08)` |
| Mode | Light | Dark | Dark | Dark | Dark |

## Table of Contents

### Sites
- [Wedding CRM](sites/wedding-crm.md) — Warm organic CRM with sage green palette
- [DailyBrief.AI](sites/dailybrief.md) — Ultra-dark intelligence dashboard
- [Map Creator](sites/map-creator.md) — Nature-inspired creative tool
- [Not A Doc AI](sites/not-a-doc-ai.md) — Modern AI chat + data interface
- [Vector RAG](sites/vector-rag.md) — Dark intel chat with animated world-map landing + live dashboard

### Foundations
- [Color](foundations/color.md) — Palettes, semantics, opacity scales
- [Typography](foundations/typography.md) — Font pairings, scales, weights, OpenType features
- [Spacing](foundations/spacing.md) — Container widths, padding, grid systems, density
- [Shadows & Depth](foundations/shadows-and-depth.md) — Shadows, glass effects, layered depth, glows

### Patterns
- [Animation & Motion](patterns/animation-and-motion.md) — CSS keyframes, Framer Motion, easing, durations
- [Cards](patterns/cards.md) — KPI, glass, white, accent-bordered, stacked
- [Buttons & Actions](patterns/buttons-and-actions.md) — Gradient, solid, pill, ghost, circular, icon
- [Forms & Inputs](patterns/forms-and-inputs.md) — Inputs, selects, sliders, radio cards, inline edit
- [Navigation](patterns/navigation.md) — Sidebars, navbars, tabs, filters, pagination
- [Badges & Status](patterns/badges-and-status.md) — Status pipeline, semantic, count, stack badges
- [Tables & Lists](patterns/tables-and-lists.md) — Data tables, timelines, staggered lists
- [Chat Interfaces](patterns/chat-interfaces.md) — Widget vs full-page chat, side-by-side comparison
- [Maps & Data Viz](patterns/maps-and-data-viz.md) — OpenLayers, choropleths, Recharts, progress bars
- [Modals & Overlays](patterns/modals-and-overlays.md) — Status overlays, guide modals, expansions
- [Loading & Feedback](patterns/loading-and-feedback.md) — Skeletons, spinners, progress bars, timers
- [Scrolling & Carousels](patterns/scrolling-and-carousels.md) — Infinite banners, auto-rotation, custom scrollbars

### Guides
- [Applying Dark Minimal](guides/applying-dark-minimal.md) — Three-tier bg rule, border strategy, accent usage
- [Applying Warm Organic](guides/applying-warm-organic.md) — Tinted whites, natural accents, premium density
- [Applying Nature Creative](guides/applying-nature-creative.md) — CSS vars, glass effects, creative tool UI
- [Responsive Strategies](guides/responsive-strategies.md) — Per-site breakpoint strategies
- [Accessibility](guides/accessibility.md) — Reduced motion, focus rings, contrast, keyboard nav

---

*MIT Licensed. See [CONTRIBUTING.md](CONTRIBUTING.md) for contribution guidelines.*
