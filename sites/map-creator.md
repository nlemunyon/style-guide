# Map Creator Design System

> Nature-inspired creative tool for generating minimalist city map posters. Dark mode with a forest green accent mirrors the cartographic and geographic theme. CSS custom properties drive a cohesive, maintainable design system. Glass morphism effects and gradient accents create a premium creative-tool feel.

---

## Color Palette

All colors are defined as CSS custom properties on `:root` for global consistency and easy theming.

### Core Tokens

| Token | Value | Swatch | Usage |
|---|---|---|---|
| `--bg-primary` | `#141517` | ![](https://via.placeholder.com/12/141517/141517.png) | Page background, base layer |
| `--bg-secondary` | `#1a1c1e` | ![](https://via.placeholder.com/12/1a1c1e/1a1c1e.png) | Cards, cheat sheet, secondary surfaces |
| `--bg-card` | `rgba(255, 255, 255, 0.03)` | | Glass card fill, preview container |
| `--bg-card-hover` | `rgba(255, 255, 255, 0.06)` | | Card hover state fill |
| `--border-color` | `rgba(160, 170, 160, 0.12)` | | Card borders, dividers, slider track |
| `--text-primary` | `#f5f5f5` | ![](https://via.placeholder.com/12/f5f5f5/f5f5f5.png) | Headings, body copy, primary content |
| `--text-secondary` | `#9ca3a0` | ![](https://via.placeholder.com/12/9ca3a0/9ca3a0.png) | Labels, descriptions, supporting text |
| `--text-muted` | `#636966` | ![](https://via.placeholder.com/12/636966/636966.png) | Footer, disabled states, hints |
| `--accent-primary` | `#7dad7d` | ![](https://via.placeholder.com/12/7dad7d/7dad7d.png) | Links, active states, timer, slider thumb |
| `--accent-secondary` | `#9dc49d` | ![](https://via.placeholder.com/12/9dc49d/9dc49d.png) | Gradient endpoint, hover highlights |
| `--accent-gradient` | `linear-gradient(135deg, #5c8a5c 0%, #7dad7d 50%, #9dc49d 100%)` | ![](https://via.placeholder.com/12/5c8a5c/5c8a5c.png) ![](https://via.placeholder.com/12/7dad7d/7dad7d.png) ![](https://via.placeholder.com/12/9dc49d/9dc49d.png) | Buttons, progress fill, h1 gradient text |
| `--success` | `#6abf6a` | ![](https://via.placeholder.com/12/6abf6a/6abf6a.png) | Success states, optimal size indicator |
| `--glass` | `rgba(140, 180, 140, 0.05)` | | Glass morphism tint overlay |

### Full Custom Properties Block

```css
:root {
  --bg-primary: #141517;
  --bg-secondary: #1a1c1e;
  --bg-card: rgba(255, 255, 255, 0.03);
  --bg-card-hover: rgba(255, 255, 255, 0.06);
  --border-color: rgba(160, 170, 160, 0.12);
  --text-primary: #f5f5f5;
  --text-secondary: #9ca3a0;
  --text-muted: #636966;
  --accent-primary: #7dad7d;
  --accent-secondary: #9dc49d;
  --accent-gradient: linear-gradient(135deg, #5c8a5c 0%, #7dad7d 50%, #9dc49d 100%);
  --success: #6abf6a;
  --glass: rgba(140, 180, 140, 0.05);
}
```

---

## Typography

Map Creator uses **Inter** via Google Fonts, loaded with weights 300 through 700. The typographic scale emphasizes clean readability with tight heading kerning and generous body line-height.

| Element | Size | Weight | Tracking | Notes |
|---|---|---|---|---|
| Logo / brand | `0.65rem` | 600 | `3px` | Uppercase, `--accent-primary` color |
| h1 | `2.5rem` | 700 | `-1px` | Gradient text via `background-clip: text` using `--accent-gradient` |
| h2 | `2rem` | 700 | Default | `--text-primary` |
| Labels | `0.7rem` | 600 | `1px` | Uppercase, `--text-secondary` color |
| Body | Inherited | 400 | Default | `line-height: 1.6`, `--text-primary` |

### Font Loading

```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

### Gradient Heading

```css
h1 {
  font-size: 2.5rem;
  font-weight: 700;
  letter-spacing: -1px;
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

---

## Spacing & Layout

| Property | Value |
|---|---|
| Container max-width | `1400px` |
| Container padding | `0 24px` |
| Main content layout | 2-column CSS grid |
| Main content gap | `24px` |
| Form section border-radius | `18px` |
| Form section padding | `24px` |
| Form section backdrop-filter | `blur(20px)` |
| Gallery grid | `auto-fill, minmax(200px, 1fr)` |
| Gallery gap | `24px` |

### Main Grid Structure

```css
.main-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 24px;
}
```

---

## Components

### 1. Infinite Banner

A continuously scrolling strip of thumbnail images at the top of the page. The banner pauses on hover so users can inspect individual posters.

- Height: `160px`
- Animation: CSS keyframe, `30s linear infinite`
- Overlay: gradient fade at the bottom edge
- Hover behavior: `animation-play-state: paused`

```css
@keyframes banner-scroll {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-50%);
  }
}

.banner-track {
  display: flex;
  animation: banner-scroll 30s linear infinite;
}

.banner-track:hover {
  animation-play-state: paused;
}

.banner-overlay {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 40px;
  background: linear-gradient(transparent, var(--bg-primary));
  pointer-events: none;
}
```

### 2. Form Section (Glass Card)

The primary input area uses glass morphism: a semi-transparent background with a backdrop blur, bordered with a faint green-tinted line.

```css
.form-section {
  background: var(--bg-card);
  border: 1px solid var(--border-color);
  border-radius: 18px;
  padding: 24px;
  backdrop-filter: blur(20px);
}
```

Labels inside the form follow the uppercase micro-label pattern:

```css
.form-label {
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: var(--text-secondary);
}
```

### 3. Theme Grid

A grid of selectable radio cards. Each card represents a map rendering theme. The checked state highlights the card with an accent border and a subtle green glow.

```css
.theme-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(105px, 1fr));
  gap: 8px;
}

.theme-card {
  border: 2px solid var(--border-color);
  border-radius: 10px;
  padding: 10px;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s;
  background: var(--bg-card);
}

.theme-card:hover {
  background: var(--bg-card-hover);
  border-color: var(--accent-primary);
}

.theme-card.checked {
  border-color: var(--accent-primary);
  box-shadow: 0 0 12px rgba(125, 173, 125, 0.2);
  background: rgba(125, 173, 125, 0.08);
}
```

### 4. Distance Slider

A custom range input with a styled thumb and track. The thumb is a small circle in the accent color with a faint glow. The track is a thin line using the border color.

```css
input[type="range"] {
  -webkit-appearance: none;
  width: 100%;
  height: 4px;
  background: var(--border-color);
  border-radius: 2px;
  outline: none;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: var(--accent-primary);
  cursor: pointer;
  box-shadow: 0 0 8px rgba(125, 173, 125, 0.4);
}
```

### 5. Quality Radio Cards

A set of three radio buttons displayed as cards in a fixed 3-column grid. The checked card receives an accent border and a tinted background.

```css
.quality-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 8px;
}

.quality-card {
  border: 2px solid var(--border-color);
  border-radius: 10px;
  padding: 12px;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s;
}

.quality-card.checked {
  border-color: var(--accent-primary);
  background: rgba(125, 173, 125, 0.1);
}
```

### 6. Cheat Sheet

A reference card showing recommended distance values for different city sizes. Uses the secondary background and a 3-column grid. Values are color-coded by suitability.

| Size Category | Color Token | Hex |
|---|---|---|
| Optimal | `--success` | ![](https://via.placeholder.com/12/6abf6a/6abf6a.png) `#6abf6a` |
| Good | `--accent-primary` | ![](https://via.placeholder.com/12/7dad7d/7dad7d.png) `#7dad7d` |
| Maximum | `--text-secondary` | ![](https://via.placeholder.com/12/9ca3a0/9ca3a0.png) `#9ca3a0` |

```css
.cheat-sheet {
  background: var(--bg-secondary);
  border-radius: 12px;
  padding: 16px;
}

.cheat-sheet-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
}
```

### 7. Buttons

Buttons use a generous border-radius and the accent gradient for the primary variant. Hover lifts the button slightly and intensifies the glow.

```css
.btn {
  border-radius: 10px;
  padding: 12px 24px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
  border: none;
}

.btn-primary {
  background: var(--accent-gradient);
  color: #fff;
  box-shadow: 0 4px 12px rgba(125, 173, 125, 0.3);
}

.btn-primary:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(125, 173, 125, 0.5);
}

.btn-success {
  background: var(--success);
  color: #fff;
}
```

### 8. Preview Container

The preview area maintains a portrait poster aspect ratio and uses the card background as a placeholder surface.

```css
.preview-container {
  aspect-ratio: 3 / 4;
  background: var(--bg-card);
  border-radius: 16px;
  overflow: hidden;
  position: relative;
}
```

### 9. Status Overlay

During generation, a dark overlay covers the preview with a spinner, progress bar, and timer. The overlay is nearly opaque to keep focus on the progress indicators.

```css
.status-overlay {
  position: absolute;
  inset: 0;
  background: rgba(20, 21, 23, 0.95);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-radius: 16px;
}
```

### 10. Progress Bar

A thin horizontal bar showing generation progress. The track uses the border color; the fill uses the accent gradient with a smooth width transition.

```css
.progress-track {
  width: 100%;
  height: 6px;
  background: var(--border-color);
  border-radius: 3px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: var(--accent-gradient);
  border-radius: 3px;
  transition: width 0.3s ease-out;
}
```

### 11. Timer

A large monospaced counter displayed during poster generation.

```css
.timer {
  font-size: 2rem;
  font-weight: 600;
  color: var(--accent-primary);
  font-variant-numeric: tabular-nums;
}
```

### 12. Gallery Stacked Cards

When a city has multiple posters, they appear as a stacked card group. The top card is positioned normally; subsequent cards are offset behind it with `position: absolute`. A badge indicates the total count. Hover lifts the stack.

```css
.gallery-card {
  position: relative;
  cursor: pointer;
  transition: transform 0.2s;
}

.gallery-card:hover {
  transform: translateY(-8px);
}

.gallery-card .stack-layer {
  position: absolute;
  top: 4px;
  left: 4px;
  right: -4px;
  bottom: -4px;
  border-radius: 12px;
  background: var(--bg-secondary);
  z-index: -1;
}

.stack-badge {
  position: absolute;
  top: 8px;
  right: 8px;
  background: var(--accent-primary);
  color: #fff;
  font-size: 0.75rem;
  font-weight: 600;
  padding: 2px 8px;
  border-radius: 12px;
}
```

### 13. Expanded Gallery Modal

Clicking a stacked card opens a full-screen overlay showing all posters for that city. Items have subtle hover lift and border brightening.

```css
.expanded-modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
  z-index: 100;
  overflow-y: auto;
  padding: 48px 24px;
}

.expanded-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 24px;
  max-width: 1200px;
  margin: 0 auto;
}

.expanded-item {
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid var(--border-color);
  transition: all 0.2s;
  cursor: pointer;
}

.expanded-item:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.4);
  border-color: rgba(160, 170, 160, 0.25);
}
```

### 14. Image Modal

A full-screen lightbox for viewing a single poster at full resolution. Includes download and close action buttons.

```css
.image-modal {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
  z-index: 200;
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-modal img {
  max-height: 85vh;
  max-width: 90vw;
  border-radius: 16px;
  object-fit: contain;
}

.image-modal .actions {
  position: absolute;
  top: 24px;
  right: 24px;
  display: flex;
  gap: 12px;
}
```

### 15. Footer

A minimal centered footer with muted text and a top border separator.

```css
.footer {
  text-align: center;
  padding: 24px 0;
  color: var(--text-muted);
  border-top: 1px solid var(--border-color);
  margin-top: 48px;
}
```

---

## Animations

### Banner Scroll

```css
@keyframes banner-scroll {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

.banner-track {
  animation: banner-scroll 30s linear infinite;
}
.banner-track:hover {
  animation-play-state: paused;
}
```

### Spinner

```css
@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.spinner {
  width: 40px;
  height: 40px;
  border: 3px solid var(--border-color);
  border-top-color: var(--accent-primary);
  border-radius: 50%;
  animation: spin 1s linear infinite;
}
```

### Interaction Transitions

All interactive elements use `0.2s` to `0.3s` transitions by default.

| Element | Property | Duration | Easing |
|---|---|---|---|
| Button hover | `transform`, `box-shadow` | `0.2s` | Default (ease) |
| Gallery card hover | `transform` | `0.2s` | Default |
| Expanded item hover | `transform`, `box-shadow`, `border-color` | `0.2s` | Default |
| Progress fill | `width` | `0.3s` | `ease-out` |
| Theme card state | `all` | `0.2s` | Default |
| Quality card state | `all` | `0.2s` | Default |

### Hover Lift Values

| Component | translateY | Shadow Change |
|---|---|---|
| Buttons | `-2px` | Glow intensifies (`0.3` to `0.5` alpha) |
| Gallery stacked cards | `-8px` | -- |
| Expanded gallery items | `-4px` | `0 8px 24px rgba(0,0,0,0.4)` + brighter border |

---

## Responsive Behavior

Map Creator is a desktop-focused creative tool. A single breakpoint handles tablet-width layouts.

| Breakpoint | Change |
|---|---|
| `<= 900px` | Main content grid collapses from 2 columns to 1 column |

```css
@media (max-width: 900px) {
  .main-content {
    grid-template-columns: 1fr;
  }
}
```

No additional mobile-specific overrides are documented. The tool expects a desktop viewport for the poster generation workflow.

---

## Design Principles

1. **Nature-forward accent palette.** The forest green gradient (`#5c8a5c` to `#9dc49d`) ties every interactive element back to the geographic and cartographic identity of the tool.

2. **Glass morphism for depth.** Semi-transparent backgrounds with `backdrop-filter: blur(20px)` and fine borders create layered depth without heavy drop shadows.

3. **Gradient as brand.** The `--accent-gradient` is the single strongest visual signature -- it appears on the primary heading, buttons, progress bar fill, and theme card glow.

4. **Restrained animation.** Motion is limited to functional feedback (hover lifts, progress transitions) and the decorative banner scroll. Nothing auto-plays beyond the banner.

5. **CSS custom properties as the single source of truth.** Every color, including translucent values, is tokenized. Swapping the accent from green to another hue requires changing only three values (`--accent-primary`, `--accent-secondary`, and the gradient stops).

---

## How to Adapt This System

The Map Creator design system transfers well to other creative-tool or asset-generator interfaces:

### 1. Design Asset Generator (Icon Maker, Palette Creator)
Replace the theme grid with tool/style selectors. The preview container aspect ratio changes from 3:4 to 1:1 for icons or flexible for palettes. The progress overlay and status pattern carry over directly.

### 2. Photography Portfolio with Gallery + Upload Tool
The gallery stacked cards, expanded modal, and image modal compose a complete portfolio browsing experience. Swap the form section for an upload dropzone. The banner becomes a featured-work carousel.

### 3. Music Visualizer or Audio Tool Interface
The glass card pattern works for control panels. Replace the progress bar with a waveform or playback timeline using the same gradient fill. The accent green shifts to a cyan or violet to match an audio aesthetic.

### 4. 3D Model Viewer / Configurator
The 2-column layout (controls left, preview right) maps directly to a 3D viewport with a configuration panel. Theme cards become material or texture selectors. The distance slider becomes a camera distance or detail-level control.
