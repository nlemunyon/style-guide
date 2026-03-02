# Buttons & Actions

Gradient buttons, solid buttons, pill buttons, ghost buttons, icon buttons, and micro-interactions.

## Button Variants

### Pill Button (Wedding CRM)

Rounded pill shape with semantic color variants:

```css
.btn {
  display: inline-block;
  padding: 0.6rem 1.5rem;
  border: none;
  border-radius: 25px;
  font-size: 0.9rem;
  cursor: pointer;
  text-decoration: none;
  transition: all 0.2s;
}

.btn-sm { padding: 0.4rem 1rem; font-size: 0.8rem; }

.btn-primary { background: #7d8b6a; color: white; }
.btn-primary:hover { background: #6b7f5c; }

.btn-secondary { background: #e9ecef; color: #333; }
.btn-secondary:hover { background: #dee2e6; }

.btn-danger { background: #dc3545; color: white; }
.btn-danger:hover { background: #c82333; }

.btn-outline {
  background: transparent;
  border: 1px solid #7d8b6a;
  color: #7d8b6a;
}
.btn-outline:hover { background: #7d8b6a; color: white; }
```

**Characteristics:** High border-radius (25px) for friendly pill shape. Simple hover: darken background. Outline variant inverts on hover.

### Gradient Button (Map Creator)

Gradient fill with shadow glow and lift effect:

```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 14px 28px;
  border: none;
  border-radius: 10px;
  font-size: 0.9rem;
  font-weight: 600;
  font-family: inherit;
  cursor: pointer;
  transition: all 0.2s;
}

.btn-primary {
  width: 100%;
  background: linear-gradient(135deg, #5c8a5c 0%, #7dad7d 50%, #9dc49d 100%);
  color: white;
  box-shadow: 0 4px 20px rgba(125, 173, 125, 0.3);
}

.btn-primary:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px rgba(125, 173, 125, 0.4);
}

.btn-primary:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
}

.btn-success {
  background: linear-gradient(135deg, #6abf6a 0%, #4a9f4a 100%);
  color: white;
}
```

**Characteristics:** Gradient fill with matching color shadow. Physical lift on hover (`translateY(-2px)`) with intensified shadow. Disabled state reduces opacity.

### Icon Button (Wedding CRM Chat)

Small square buttons with icon content:

```css
.chat-header-actions button {
  width: 32px;
  height: 32px;
  background: #f5f7f3;
  border: 1px solid #d4dbc8;
  border-radius: 6px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #6b7f5c;
  transition: all 0.15s;
}

.chat-header-actions button:hover {
  background: #e8eee3;
  border-color: #7d8b6a;
  color: #5a6b4a;
}

.chat-header-actions button svg { width: 16px; height: 16px; }
```

### Send Button (Wedding CRM Chat)

Compact circular send button:

```css
.send-btn {
  width: 32px;
  height: 32px;
  background: #5a6b4a;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-shrink: 0;
  transition: background 0.15s;
}

.send-btn:hover:not(:disabled) { background: #4a5a3a; }
.send-btn:disabled { background: #ccc; cursor: not-allowed; }
.send-btn svg { width: 14px; height: 14px; }
```

### Chat Toggle (Wedding CRM)

Floating action button with attention animation:

```css
.chat-toggle {
  position: fixed;
  bottom: 24px;
  right: 24px;
  width: 60px;
  height: 60px;
  border-radius: 16px;
  background: linear-gradient(135deg, #667756 0%, #4a5a3a 50%, #3d4d2f 100%);
  color: white;
  border: none;
  cursor: pointer;
  box-shadow: 0 4px 20px rgba(74, 90, 58, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
  animation: pulse-ring 2.5s ease-out infinite;
}

.chat-toggle:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 8px 30px rgba(74, 90, 58, 0.5);
  animation: none;
}

.chat-toggle:active {
  transform: translateY(-1px) scale(0.98);
}
```

### Framer Motion Button (Not A Doc AI)

Declarative micro-interactions:

```jsx
<motion.button
  whileHover={{ y: -1, transition: { duration: 0.15 } }}
  whileTap={{ scale: 0.98, transition: { duration: 0.1 } }}
  className="bg-accent text-white px-4 py-2 rounded-full"
>
  Send
</motion.button>
```

### Modal Action Buttons (Map Creator)

Paired download/close buttons:

```css
.modal-btn {
  padding: 12px 28px;
  border: none;
  border-radius: 10px;
  font-size: 0.9rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
  font-family: inherit;
  width: 140px;
  text-align: center;
}

.modal-btn-download {
  background: linear-gradient(135deg, #5c8a5c 0%, #7dad7d 50%, #9dc49d 100%);
  color: white;
}

.modal-btn-close {
  background: rgba(140, 180, 140, 0.05);  /* glass variable */
  color: white;
  border: 1px solid rgba(160, 170, 160, 0.12);
}

.modal-btn:hover { transform: scale(1.05); }
```

### Filter Tab Buttons (Wedding CRM)

Pill-shaped filter toggles:

```css
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

.filters a:hover, .filters button:hover { background: #e8eee3; }
.filters a.active, .filters button.active { background: #7d8b6a; color: white; }
```

## Button Comparison Table

| Property | Wedding CRM | DailyBrief.AI | Map Creator | Not A Doc AI |
|----------|-------------|---------------|-------------|--------------|
| Shape | Pill (25px) | — | Rounded (10px) | Pill (full) |
| Fill | Solid color | Tailwind utility | Gradient | Solid color |
| Hover | Darken bg | — | Lift + shadow boost | `y: -1` lift |
| Active/Tap | — | — | — | `scale: 0.98` |
| Shadow | None | None | Accent glow | None |
| Disabled | — | — | `opacity: 0.6` | — |

## How to Apply Buttons

### For a professional tool:
- Pill-shaped (20-25px radius) for friendly, approachable CTAs
- Solid accent color with simple darken-on-hover
- Outline variant for secondary actions
- Small icon buttons (32px) for toolbars

### For a creative tool:
- Gradient fill with matching color shadow
- `translateY(-2px)` lift on hover with intensified shadow
- Fixed-width buttons for paired actions (download/close)
- Scale effect on hover for modal actions

### For a chat interface:
- Compact send button (32px) matching accent color
- Floating toggle with pulse animation for discoverability
- Icon buttons with subtle border in header toolbars
- Disabled state: gray out with `cursor: not-allowed`

### For a modern AI interface:
- Framer Motion `whileHover` and `whileTap` for physics-based feel
- Small lift (`y: -1`) rather than large transforms
- Scale down on tap (`0.98`) for press feedback
- Full border-radius for pill shape
