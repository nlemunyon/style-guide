# Scrolling & Carousels

Infinite banners, auto-rotation, custom scrollbars, and scroll behavior patterns.

## Infinite Banner (Map Creator)

A continuously scrolling strip of gallery thumbnails:

```css
.banner {
  position: relative;
  height: 160px;
  overflow: hidden;
  background: #1a1c1e;
  border-bottom: 1px solid rgba(160, 170, 160, 0.12);
}

.banner-track {
  display: flex;
  animation: scroll 30s linear infinite;
  height: 100%;
}

.banner-track:hover {
  animation-play-state: paused;
}

@keyframes scroll {
  0% { transform: translateX(0); }
  100% { transform: translateX(-50%); }
}

.banner-item {
  flex-shrink: 0;
  width: 120px;
  height: 160px;
  margin-right: 2px;
  position: relative;
  overflow: hidden;
}

.banner-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0.7;
  transition: opacity 0.3s;
}

.banner-item:hover img {
  opacity: 1;
}
```

### Fade Overlay

A gradient overlay creates a fade-to-background effect at the bottom:

```css
.banner-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(to bottom, transparent 50%, rgba(20, 21, 23, 0.9) 100%);
  pointer-events: none;
}
```

### Implementation Notes

- The track contains all items duplicated (`[...items, ...items]`), so `translateX(-50%)` seamlessly loops
- 30s duration feels natural — fast enough to notice movement, slow enough to scan
- `animation-play-state: paused` on hover lets users focus on a specific item
- Individual items brighten from 70% to 100% opacity on hover
- Empty state shows centered "Loading gallery..." text

## Custom Scrollbars

### DailyBrief.AI

```css
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: #0a0a0a;
}

::-webkit-scrollbar-thumb {
  background: #1a1a1a;
  border-radius: 9999px;
}

::-webkit-scrollbar-thumb:hover {
  background: #a3a3a3;
}
```

**Strategy:** Scrollbar matches the background at rest (nearly invisible). Brightens dramatically on hover for usability.

### Not A Doc AI

```css
::-webkit-scrollbar {
  width: 8px;
  height: 8px;
}

::-webkit-scrollbar-track {
  background: transparent;
}

::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.15);
  border-radius: 100px;
}

::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 255, 255, 0.25);
}
```

**Strategy:** Transparent track (fully invisible). Semi-transparent thumb. Subtler hover brightening.

### Comparison

| Property | DailyBrief.AI | Not A Doc AI |
|----------|---------------|--------------|
| Track | `#0a0a0a` (solid) | `transparent` |
| Thumb default | `#1a1a1a` | `rgba(255,255,255,0.15)` |
| Thumb hover | `#a3a3a3` | `rgba(255,255,255,0.25)` |
| Radius | `9999px` | `100px` |
| Visibility at rest | Very low | Low |

## Chat Auto-Scroll

Both chat implementations auto-scroll to the latest message:

```javascript
// Scroll to bottom after new message
function scrollToBottom() {
  chatMessages.scrollTop = chatMessages.scrollHeight;
}

// Called after message append and typing indicator show
```

For Not A Doc AI (React), the pattern uses a ref:

```jsx
const messagesEndRef = useRef(null)

useEffect(() => {
  messagesEndRef.current?.scrollIntoView({ behavior: 'smooth' })
}, [messages])

// In JSX:
<div ref={messagesEndRef} />
```

## Chat Sessions List Scroll (Wedding CRM)

The sidebar sessions list scrolls independently:

```css
.chat-sessions-list {
  flex: 1;
  overflow-y: auto;
  padding: 8px;
}
```

Using `flex: 1` + `overflow-y: auto` makes it fill available space and scroll when needed.

## Gallery Expanded Scroll (Map Creator)

The expanded gallery modal is a scrollable overlay:

```css
.stack-expanded {
  position: fixed;
  inset: 0;
  overflow-y: auto;  /* Scrollable modal */
  padding: 24px;
}
```

The entire overlay scrolls, not just a content area within it. This works well for gallery views where you want the header to scroll away.

## How to Apply Scrolling Patterns

### For an infinite banner/carousel:
- Duplicate items in the track so `translateX(-50%)` creates a seamless loop
- 30s duration is a good starting point for moderate-speed scrolling
- Pause on hover with `animation-play-state: paused`
- Add a gradient overlay to fade items into the background
- Individual items should brighten on hover (0.7 → 1.0 opacity)

### For custom scrollbars in dark mode:
- Match the track to the background (or use transparent)
- Thumb at 15-20% white opacity when resting
- Brighten to 25% on hover
- Full border-radius for pill shape
- Keep 8px width — narrow enough to be subtle, wide enough to grab

### For auto-scrolling chat:
- Use `scrollIntoView({ behavior: 'smooth' })` in React
- Use `scrollTop = scrollHeight` in vanilla JS
- Trigger after each new message and typing indicator
- Don't auto-scroll if user has scrolled up (reading history)

### For scrollable modals:
- `overflow-y: auto` on the fixed overlay itself (not an inner container)
- Works best for gallery/grid layouts where all content should scroll
- For document modals, put scroll on the content area to keep the header fixed
