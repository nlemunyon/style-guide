# Modals & Overlays

Status overlays, guide modals, image modals, expanded views, and overlay backdrops.

## Overlay Backdrops

| Context | Opacity | Color | Site |
|---------|---------|-------|------|
| Guide modal | 50% | Black | Wedding CRM |
| Image modal | 95% | Black | Map Creator |
| Expanded gallery | 95% | Black | Map Creator |
| Status overlay | 95% | `#141517` | Map Creator |
| Chat fullscreen | 100% | White | Wedding CRM |
| Modal | 60% + `blur(4px)` | Black | Vector RAG |

**Pattern:** Dark-mode sites use very high opacity (95%) backdrops that match the dark aesthetic. Light-mode uses moderate opacity (50%) to dim content while keeping it visible. Vector RAG is the outlier — a moderate 60% backdrop paired with a `backdrop-filter: blur(4px)` frost, so context stays legible behind the dialog.

## Guide Modal (Wedding CRM)

Full documentation modal with slide-up entrance:

```css
.guide-overlay {
  display: none;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0,0,0,0.5);
  z-index: 2000;
  animation: fadeIn 0.2s ease;
}

.guide-overlay.open {
  display: flex;
  align-items: center;
  justify-content: center;
}

.guide-modal {
  background: #fff;
  width: 90%;
  max-width: 800px;
  max-height: 85vh;
  border-radius: 12px;
  box-shadow: 0 20px 60px rgba(0,0,0,0.25);
  display: flex;
  flex-direction: column;
  animation: slideUp 0.25s ease;
  overflow: hidden;
}

@keyframes slideUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.guide-header {
  padding: 16px 24px;
  background: linear-gradient(135deg, #7d8b6a 0%, #6b7f5c 100%);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.guide-header h2 {
  font-size: 16px;
  font-weight: 500;
  color: #fff;
  letter-spacing: 0.5px;
}

.guide-close {
  width: 28px;
  height: 28px;
  border: none;
  background: rgba(255,255,255,0.15);
  border-radius: 6px;
  cursor: pointer;
  color: rgba(255,255,255,0.9);
}

.guide-close:hover {
  background: rgba(255,255,255,0.25);
}

.guide-content {
  flex: 1;
  overflow-y: auto;
  padding: 24px;
  font-size: 14px;
  line-height: 1.6;
  color: #333;
  background: #f5f7f3;
}
```

**Characteristics:** Gradient header matching the navbar. Scrollable content area with tinted background. Close button uses semi-transparent white. 85vh max-height leaves room for the overlay to show.

## Image Modal (Map Creator)

Full-screen image viewer with action buttons:

```css
.modal {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
  z-index: 1000;
  align-items: center;
  justify-content: center;
  padding: 24px;
}

.modal.active { display: flex; }

.modal-content {
  max-width: 90%;
  max-height: 90%;
  position: relative;
}

.modal-content img {
  max-width: 100%;
  max-height: 80vh;
  border-radius: 16px;
  box-shadow: 0 25px 50px rgba(0, 0, 0, 0.5);
}

.modal-close {
  position: absolute;
  top: -48px;
  right: 0;
  background: none;
  border: none;
  color: white;
  font-size: 2rem;
  cursor: pointer;
  opacity: 0.7;
}

.modal-close:hover { opacity: 1; }

.modal-actions {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-top: 20px;
}
```

**Characteristics:** Near-opaque black backdrop. Large rounded image with dramatic shadow. Close button positioned above the image. Paired download/close action buttons below.

## Expanded Gallery View (Map Creator)

Grid of items replacing the normal gallery:

```css
.stack-expanded {
  display: none;
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
  z-index: 1000;
  padding: 24px;
  overflow-y: auto;
}

.stack-expanded.active { display: block; }

.stack-expanded-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 24px;
  max-width: 1200px;
  margin-left: auto;
  margin-right: auto;
}

.stack-expanded-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

.expanded-item {
  background: rgba(255, 255, 255, 0.03);
  border-radius: 16px;
  overflow: hidden;
  border: 1px solid rgba(160, 170, 160, 0.12);
  cursor: pointer;
  transition: all 0.3s;
}

.expanded-item:hover {
  transform: translateY(-4px);
  border-color: rgba(255, 255, 255, 0.15);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}
```

**Characteristics:** Same dark backdrop as image modal. Scrollable grid of cards. Each card lifts on hover with shadow + border brightening. Title bar with city name and close button.

## Status Overlay (Map Creator)

Overlay on the preview container during poster generation:

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
  border-radius: 24px;
}

.status-overlay.active {
  opacity: 1;
  pointer-events: auto;
}
```

Contains: spinner → status text → progress bar → timer → download button (appears on completion).

## Example Box (Wedding CRM Guide)

Highlighted example blocks within the guide modal:

```css
.guide-content .example-box {
  background: #fff;
  border: 1px solid #d4dbc8;
  border-left: 3px solid #7d8b6a;
  border-radius: 0 8px 8px 0;
  padding: 14px 16px;
  margin: 12px 0;
}

.guide-content .limitation {
  background: #fff;
  border: 1px solid #d4dbc8;
  border-left: 3px solid #a0a89a;
  border-radius: 0 8px 8px 0;
  padding: 12px 16px;
  margin: 12px 0;
  color: #555;
}
```

**Pattern:** Left border accent for callout blocks. Example boxes use the primary accent, limitation boxes use a muted variant.

## Frosted Modal (Vector RAG)

A Framer Motion dialog: a blurred 60% backdrop with a scale-and-lift content entrance. The `Modal` component clicks-outside to close and scales content in over 0.2s:

```jsx
{/* Overlay */}
<motion.div initial={{ opacity: 0 }} animate={{ opacity: 1 }} exit={{ opacity: 0 }}
  transition={{ duration: 0.15 }} className="fixed inset-0 z-50 flex items-center justify-center"
  style={{ backgroundColor: 'rgba(0,0,0,0.6)', backdropFilter: 'blur(4px)' }}>

  {/* Content */}
  <motion.div initial={{ opacity: 0, scale: 0.97, y: 8 }} animate={{ opacity: 1, scale: 1, y: 0 }}
    exit={{ opacity: 0, scale: 0.97, y: 8 }} transition={{ duration: 0.2, ease: [0.16, 1, 0.3, 1] }}
    className="rounded-[20px] bg-bg-surface border border-border-default p-6"  /* max-w 480px default */>
    {/* Close: h-8 w-8 rounded-lg, #606060 → #e8e8e8 on #1a1a1a hover */}
  </motion.div>
</motion.div>
```

A large **content modal** variant (the Data Guide) fills the viewport instead — `95vw × 92vh`, `#000000` bg, `1px solid #1f1f1f`, `12px` radius, with an internally scrolling body.

## Toggle States

### Modal Toggle Pattern

All sites use the same show/hide pattern:

```css
/* Default: hidden */
.modal { display: none; }

/* Active: visible */
.modal.active { display: flex; }
/* or */
.modal.open { display: flex; }
```

JavaScript toggles the `active`/`open` class. No complex state management needed for simple modals.

### Chat Widget Toggle

```css
.chat-widget { display: none; flex-direction: column; }
.chat-widget.open { display: flex; }
.chat-widget.expanded { /* fullscreen overrides */ }
```

Three states: hidden (default), open (widget), expanded (fullscreen).

## How to Apply Modals

### For a light-mode tool:
- 50% opacity black backdrop
- White modal with accent-gradient header
- Slide-up entrance animation (0.25s)
- Max 85vh height with scrollable content
- Close button as semi-transparent white icon

### For a dark creative tool:
- 95% opacity black backdrop
- Near-transparent glass cards for content
- Large rounded corners (16px) on images
- Paired action buttons (primary gradient + glass secondary)
- Hover lift on interactive items

### For documentation/guide modals:
- Left-border callout blocks for examples and warnings
- Scrollable content with generous padding
- Accent-colored section headers
- Field reference tables with accent-colored header rows

### For a dark AI/analyst app (Vector RAG):
- Moderate 60% backdrop + `backdrop-filter: blur(4px)` so context stays readable
- Scale-and-lift content entrance (Framer Motion, `scale 0.97→1` + `y 8→0`, 0.2s)
- `20px`-radius surface card on the elevated tier; click-outside + Escape to close
- For dense reference content, a near-fullscreen (`95vw × 92vh`) variant with its own scroll region
