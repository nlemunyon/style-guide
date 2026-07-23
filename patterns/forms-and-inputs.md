# Forms & Inputs

Text inputs, selects, range sliders, radio cards, and inline editing patterns.

## Text Inputs

### Wedding CRM - Standard Input

```css
input[type="text"], input[type="email"], input[type="password"],
input[type="date"], input[type="tel"], select, textarea {
  padding: 0.6rem 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 0.9rem;
  width: 100%;
  font-family: inherit;
}

input:focus, select:focus, textarea:focus {
  outline: none;
  border-color: #7d8b6a;
  box-shadow: 0 0 0 3px rgba(125, 139, 106, 0.15);
}

textarea {
  resize: vertical;
  min-height: 100px;
}
```

**Focus ring:** Sage green border + 3px green-tinted outer ring. The `rgba(125, 139, 106, 0.15)` creates a soft halo effect.

### Map Creator - Dark Input

```css
input[type="text"] {
  width: 100%;
  padding: 12px 16px;
  border: 1px solid rgba(160, 170, 160, 0.12);
  border-radius: 10px;
  background: #1a1c1e;
  color: #f5f5f5;
  font-size: 0.9rem;
  font-family: inherit;
  transition: all 0.2s;
}

input[type="text"]:focus {
  outline: none;
  border-color: #7dad7d;
  box-shadow: 0 0 0 3px rgba(125, 173, 125, 0.1);
}

input[type="text"]::placeholder {
  color: #636966;
}
```

**Focus ring:** Same concept but with forest green accent and slightly subtler ring (0.1 opacity vs 0.15).

### Vector RAG - Dark Input + Chat Wrapper

The standalone `Input`/`TextArea` components sit on the elevated tier and switch their border to the accent on focus (the global `:focus-visible` adds the ring):

```jsx
<input className="h-9 rounded-lg bg-bg-elevated border border-border-default px-3
                  text-sm text-text-primary placeholder:text-text-tertiary
                  focus:border-accent outline-none transition-colors" />
/* error state: border-error; optional label: text-xs font-medium text-text-secondary */
```

```css
/* Global focus ring (applies to every focusable element) */
*:focus-visible { outline: none; box-shadow: 0 0 0 3px rgba(92,158,206,0.3); border-radius: 4px; }
```

The **chat input** uses the wrapper pattern — dark-on-black, lighting its border to `#5c9ece` with a soft 2px ring on focus:

```jsx
<div className="flex items-end gap-2 rounded-xl px-4 py-2.5"
     style={{ background: '#0d0d0d', border: '1px solid #1f1f1f' }}
     /* focus-within: borderColor #5c9ece; boxShadow 0 0 0 2px rgba(92,158,206,0.12) */>
  <textarea className="flex-1 resize-none bg-transparent text-sm text-text-primary" /* auto-grow → 200px */ />
</div>
```

### Wedding CRM - Chat Textarea

```css
.chat-input-wrapper {
  display: flex;
  align-items: center;
  gap: 8px;
  background: #fafafa;
  border-radius: 10px;
  padding: 6px 6px 6px 14px;
  border: 1px solid #e0e0e0;
  transition: border-color 0.15s, box-shadow 0.15s, background 0.15s;
}

.chat-input-wrapper:focus-within {
  border-color: #5a6b4a;
  background: #fff;
}

.chat-input-wrapper textarea {
  flex: 1;
  border: none;
  background: transparent;
  resize: none;
  font-size: 14px;
  line-height: 1.4;
  color: #1a1a1a;
  padding: 6px 0;
  max-height: 120px;
  min-height: 20px;
  font-family: inherit;
}
```

**Pattern:** The wrapper element receives the border and focus styles (`:focus-within`), while the inner textarea is borderless and transparent. This allows placing a send button inside the input area.

## Form Groups

### Wedding CRM

```css
.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  margin-bottom: 0.5rem;
  font-weight: 500;
  color: #333;
}

.form-group .help-text {
  font-size: 0.8rem;
  color: #666;
  margin-top: 0.25rem;
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}
```

### Map Creator

```css
.form-group {
  margin-bottom: 18px;
}

label {
  display: block;
  font-size: 0.7rem;
  font-weight: 600;
  margin-bottom: 8px;
  color: #9ca3a0;
  text-transform: uppercase;
  letter-spacing: 1px;
}
```

**Pattern:** Map Creator uses all-caps labels with wide letter-spacing, creating a more structured, technical feel. Wedding CRM uses sentence-case labels for a friendlier feel.

## Range Slider (Map Creator)

Custom-styled range input for distance selection:

```css
.distance-container {
  background: #1a1c1e;
  border-radius: 8px;
  padding: 8px 10px;
  border: 1px solid rgba(160, 170, 160, 0.12);
}

input[type="range"] {
  width: 100%;
  height: 4px;
  border-radius: 2px;
  background: rgba(160, 170, 160, 0.12);
  -webkit-appearance: none;
  cursor: pointer;
}

input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none;
  width: 16px;
  height: 16px;
  border-radius: 50%;
  background: #7dad7d;
  box-shadow: 0 2px 8px rgba(125, 173, 125, 0.4);
  cursor: pointer;
}

.distance-value {
  font-size: 0.9rem;
  font-weight: 600;
  color: #7dad7d;
}

.distance-labels {
  display: flex;
  justify-content: space-between;
  margin-top: 4px;
  font-size: 0.6rem;
  color: #636966;
}
```

The slider sits inside a container card with a header row showing the label and current value, the slider track, and min/max labels below.

## Radio Cards

### Theme Selector (Map Creator)

Hidden radio inputs with visual card labels:

```css
.theme-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(105px, 1fr));
  gap: 8px;
}

.theme-option { cursor: pointer; }
.theme-option input { display: none; }

.theme-card {
  padding: 14px 10px;
  border-radius: 8px;
  text-align: center;
  font-size: 0.7rem;
  font-weight: 500;
  transition: all 0.2s;
  border: 2px solid transparent;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Each theme card gets its own bg/text colors inline */
/* style="background: {{ theme.bg }}; color: {{ theme.text }};" */

.theme-option input:checked + .theme-card {
  border-color: #7dad7d;
  box-shadow: 0 0 20px rgba(125, 173, 125, 0.3);
}

.theme-card:hover {
  transform: translateY(-2px);
}
```

### Quality Selector (Map Creator)

Three-option radio cards:

```css
.quality-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 8px;
}

.quality-option { cursor: pointer; }
.quality-option input { display: none; }

.quality-card {
  padding: 12px 8px;
  border-radius: 10px;
  text-align: center;
  background: #1a1c1e;
  border: 2px solid rgba(160, 170, 160, 0.12);
  transition: all 0.2s;
}

.quality-option input:checked + .quality-card {
  border-color: #7dad7d;
  background: rgba(125, 173, 125, 0.1);
}

.quality-card:hover {
  border-color: rgba(125, 173, 125, 0.5);
}
```

**Pattern:** Both use hidden `<input>` elements with adjacent sibling selectors (`input:checked + .card`). The checked state combines accent border + glow/tint.

## Model Selector (Wedding CRM Chat)

Minimal inline select with custom arrow:

```css
.model-selector select {
  appearance: none;
  background: transparent url("data:image/svg+xml,...chevron-svg...") no-repeat right center;
  border: none;
  font-size: 11px;
  color: #666;
  cursor: pointer;
  padding-right: 14px;
  max-width: 140px;
}

.model-selector select:focus { outline: none; }
```

Paired with a small status dot:

```css
.model-status {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: #10b981;  /* green = online */
}

.model-status.offline { background: #ef4444; }
```

## Input Comparison Table

| Property | Wedding CRM | Map Creator | Vector RAG |
|----------|-------------|-------------|-----------|
| Border | `1px solid #ddd` | `1px solid rgba(160,170,160,0.12)` | `1px solid rgba(255,255,255,0.08)` |
| Radius | `8px` | `10px` | `8px` inputs / `12px` chat wrapper |
| Background | White (default) | `#1a1c1e` | `#111111` inputs / `#0d0d0d` chat |
| Focus border | `#7d8b6a` | `#7dad7d` | `#5c9ece` |
| Focus ring | `3px rgba(125,139,106,0.15)` | `3px rgba(125,173,125,0.1)` | `3px rgba(92,158,206,0.3)` global / `2px rgba(92,158,206,0.12)` chat |
| Label style | Sentence case, 500 weight | Uppercase, 600 weight, letter-spaced | Sentence case, `text-xs` 500 weight |
| Placeholder | Default | `#636966` | `#606060` (text-tertiary) |

## How to Apply Forms

### For a light-mode professional tool:
- Standard inputs with 8px radius and 1px gray border
- Accent-colored focus ring at 15% opacity
- Sentence-case labels with 500 weight
- Two-column form rows for compact layout

### For a dark creative tool:
- Dark background inputs matching the surface tier
- Accent focus ring at 10% opacity
- Uppercase labels with letter-spacing for structure
- Radio cards for visual selection (themes, options)
- Custom range sliders with accent-colored thumb + glow

### For a chat input:
- Wrapper element with focus-within styling
- Borderless inner textarea
- Send button inside the wrapper
- Auto-growing textarea with max-height cap
- On a pure-black base (Vector RAG), pair a per-element accent focus border with a global `:focus-visible` accent ring so keyboard focus is always visible
