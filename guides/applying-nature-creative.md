# Applying Nature Creative

How to apply the nature-inspired creative tool aesthetic (used by Map Creator) to any project. This guide covers CSS custom properties, glass effects, gradient branding, and creative tool UI patterns.

## The Core Principle

This aesthetic combines a dark, muted background with nature-inspired green accents and glass morphism effects. It feels premium and creative — suitable for tools where users generate, configure, or explore visual content. CSS custom properties make the entire theme swappable.

## Step 1: Define Your Design Tokens

The entire theme lives in CSS custom properties:

```css
:root {
  /* Backgrounds */
  --bg-primary: #141517;
  --bg-secondary: #1a1c1e;
  --bg-card: rgba(255, 255, 255, 0.03);
  --bg-card-hover: rgba(255, 255, 255, 0.06);

  /* Borders */
  --border-color: rgba(160, 170, 160, 0.12);

  /* Text */
  --text-primary: #f5f5f5;
  --text-secondary: #9ca3a0;
  --text-muted: #636966;

  /* Accent */
  --accent-primary: #7dad7d;
  --accent-secondary: #9dc49d;
  --accent-gradient: linear-gradient(135deg, #5c8a5c 0%, #7dad7d 50%, #9dc49d 100%);

  /* Semantic */
  --success: #6abf6a;
  --glass: rgba(140, 180, 140, 0.05);
}
```

**To change the entire theme**, swap these variables. For a warm/amber creative tool:

```css
:root {
  --accent-primary: #d4a574;
  --accent-secondary: #e8c49a;
  --accent-gradient: linear-gradient(135deg, #b88a5c 0%, #d4a574 50%, #e8c49a 100%);
  --success: #d4a574;
  --glass: rgba(180, 160, 140, 0.05);
  --border-color: rgba(170, 160, 150, 0.12);
}
```

## Step 2: Glass Card Base

The signature look — translucent cards with backdrop blur:

```css
.glass-card {
  background: var(--bg-card);
  border-radius: 18px;
  padding: 24px;
  border: 1px solid var(--border-color);
  backdrop-filter: blur(20px);
}
```

**When glass works:**
- Over solid-color backgrounds (the blur is subtle but present)
- For forms and configuration panels
- At larger sizes (small glass cards look muddy)

**When to skip glass:**
- Content-heavy areas (use solid `--bg-secondary` instead)
- Gallery items (images provide their own visual interest)
- Mobile (performance cost of backdrop-filter)

## Step 3: Gradient Branding

Use your accent gradient for headings and primary CTAs:

```css
/* Gradient text heading */
h1 {
  font-size: 2.5rem;
  font-weight: 700;
  letter-spacing: -1px;
  background: var(--accent-gradient);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

/* Gradient button */
.btn-primary {
  background: var(--accent-gradient);
  color: white;
  border: none;
  border-radius: 10px;
  padding: 14px 28px;
  font-weight: 600;
  box-shadow: 0 4px 20px rgba(125, 173, 125, 0.3);
}

.btn-primary:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(125, 173, 125, 0.4);
}
```

## Step 4: Uppercase Labels

Create structure with small uppercase labels:

```css
label, .label {
  display: block;
  font-size: 0.7rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  color: var(--text-secondary);
  margin-bottom: 8px;
}
```

## Step 5: Radio Card Selectors

For visual option selection (themes, modes, presets):

```css
.option-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(105px, 1fr));
  gap: 8px;
}

.option input { display: none; }

.option-card {
  padding: 14px 10px;
  border-radius: 8px;
  text-align: center;
  font-size: 0.7rem;
  font-weight: 500;
  border: 2px solid transparent;
  transition: all 0.2s;
  cursor: pointer;
}

.option input:checked + .option-card {
  border-color: var(--accent-primary);
  box-shadow: 0 0 20px rgba(125, 173, 125, 0.3);
}

.option-card:hover {
  transform: translateY(-2px);
}
```

## Step 6: Custom Range Slider

```css
input[type="range"] {
  width: 100%;
  height: 4px;
  border-radius: 2px;
  background: var(--border-color);
  -webkit-appearance: none;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: var(--accent-primary);
  box-shadow: 0 2px 8px rgba(125, 173, 125, 0.4);
}
```

## Step 7: Gallery with Stacked Cards

```css
.gallery-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 24px;
}

.gallery-item {
  position: relative;
  cursor: pointer;
  transition: transform 0.3s;
}

.gallery-item:hover {
  transform: translateY(-8px);
}

.gallery-card {
  width: 100%;
  aspect-ratio: 3/4;      /* Or your content's natural ratio */
  background: var(--bg-card);
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid var(--border-color);
}
```

## Step 8: Status Overlay for Processing

```css
.status-overlay {
  position: absolute;
  inset: 0;
  background: rgba(20, 21, 23, 0.95);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s;
  border-radius: inherit;     /* Match parent's border-radius */
}

.status-overlay.active {
  opacity: 1;
  pointer-events: auto;
}
```

## Step 9: Infinite Banner

```css
.banner {
  height: 160px;
  overflow: hidden;
  background: var(--bg-secondary);
  position: relative;
}

.banner-track {
  display: flex;
  animation: scroll 30s linear infinite;
}

.banner-track:hover { animation-play-state: paused; }

@keyframes scroll {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

/* Fade overlay at bottom */
.banner-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom, transparent 50%, rgba(20, 21, 23, 0.9) 100%);
  pointer-events: none;
}
```

## Example Project: Icon Generator Tool

1. **Background:** `#141517` base, glass form panel, solid preview area
2. **Accent:** Purple gradient (`#7d5ca5` → `#a57dd4`)
3. **Controls:** Color picker, style radio cards, size slider
4. **Preview:** Centered icon display with status overlay during generation
5. **Gallery:** Generated icons in stacked card grid
6. **Banner:** Scrolling showcase of popular generated icons

## Example Project: Photography Portfolio + Editor

1. **Background:** `#141517` base, glass upload panel
2. **Accent:** Amber gradient (`#b88a5c` → `#e8c49a`)
3. **Controls:** Filter radio cards, exposure slider, crop options
4. **Gallery:** Photo grid with 3:2 aspect ratio cards
5. **Modal:** Full-screen lightbox with download/share actions
6. **Banner:** Scrolling featured photos at top

## Example Project: Font Preview Tool

1. **Background:** `#141517` base, glass settings panel
2. **Accent:** Teal gradient (`#5ca5a5` → `#7dd4d4`)
3. **Controls:** Font family radio cards, weight slider, size slider
4. **Preview:** Large text display area with glass card
5. **Gallery:** Saved font combinations as stacked cards
6. **Labels:** Uppercase with wide letter-spacing for tool structure
