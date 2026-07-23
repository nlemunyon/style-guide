# Loading & Feedback

Spinners, progress bars, typing indicators, timers, status messages, and flash notifications.

## Spinners

### Border Spinner (Shared Pattern)

Both Wedding CRM and Map Creator use CSS border-based spinners:

```css
/* Map Creator - Large spinner (48px) */
.spinner {
  width: 48px;
  height: 48px;
  border: 3px solid rgba(160, 170, 160, 0.12);
  border-top-color: #7dad7d;
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin-bottom: 20px;
}

/* Wedding CRM - Small spinner (12px, in chat) */
.status-spinner {
  width: 12px;
  height: 12px;
  border: 2px solid #e0e0e0;
  border-top-color: #5a6b4a;
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

**Pattern:** Gray border with accent-colored top segment. The accent color matches each site's palette. Larger spinners (48px) for page-level loading, smaller (12px) for inline status.

### SVG Spinner (Vector RAG)

Vector RAG uses an SVG arc spinner tinted with the accent, in three sizes:

```jsx
<svg className="animate-spin text-accent" /* h-4 w-4 | h-6 w-6 | h-8 w-8 */ viewBox="0 0 24 24" fill="none">
  <circle className="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" strokeWidth="4" />
  <path className="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4z" />
</svg>
```

### Skeleton Shimmer (Vector RAG)

Dashboard cards ghost-load with a sweeping accent gradient rather than a spinner:

```css
.card::after { content: ''; /* overlays the card while .is-loading */
  background: linear-gradient(90deg, transparent, color-mix(in srgb, var(--accent) 9%, transparent), transparent);
  animation: ghostSweep 1.25s ease-in-out infinite;
}
@keyframes ghostSweep { from { transform: translateX(-100%); } to { transform: translateX(100%); } }
```

## Progress Bars

### Map Creator - Poster Generation

Multi-part feedback: spinner + status text + progress bar + timer:

```css
.progress-container {
  width: 80%;
  max-width: 300px;
}

.progress-bar {
  width: 100%;
  height: 6px;
  background: rgba(160, 170, 160, 0.12);
  border-radius: 3px;
  overflow: hidden;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(135deg, #5c8a5c 0%, #7dad7d 50%, #9dc49d 100%);
  border-radius: 3px;
  transition: width 0.3s ease-out;
  width: 0%;
}

.progress-text {
  display: flex;
  justify-content: space-between;
  margin-top: 8px;
  font-size: 0.75rem;
  color: #636966;
}
```

The progress bar sits inside a status overlay that covers the preview container. It shows step name on the left and percentage on the right.

### Timer Display

```css
.timer {
  font-size: 2rem;
  font-weight: 600;
  color: #7dad7d;
  margin-bottom: 8px;
  font-variant-numeric: tabular-nums;
}
```

`tabular-nums` ensures digits are fixed-width so the display doesn't shift as numbers change.

## Typing Indicators

### Three-Dot Pulse (Wedding CRM)

```css
.typing-indicator {
  display: flex;
  align-items: center;
  gap: 5px;
  padding: 8px 0;
}

.typing-dot {
  width: 6px;
  height: 6px;
  background: #9ca3af;
  border-radius: 50%;
  animation: typingPulse 1.4s ease-in-out infinite;
}

.typing-dot:nth-child(1) { animation-delay: 0s; }
.typing-dot:nth-child(2) { animation-delay: 0.15s; }
.typing-dot:nth-child(3) { animation-delay: 0.3s; }

@keyframes typingPulse {
  0%, 60%, 100% { transform: scale(0.8); opacity: 0.4; }
  30% { transform: scale(1); opacity: 1; }
}
```

### Accent-Colored Pulse (Not A Doc AI)

```css
.typing-indicator span {
  width: 8px;
  height: 8px;
  background-color: #3b82f6;
  border-radius: 50%;
  opacity: 0.4;
  animation: typing-pulse 1.4s ease-in-out infinite;
}

@keyframes typing-pulse {
  0%, 60%, 100% { opacity: 0.4; transform: scale(1); }
  30% { opacity: 1; transform: scale(1.1); }
}
```

**Comparison:**
| Property | Wedding CRM | Not A Doc AI |
|----------|-------------|--------------|
| Dot size | 6px | 8px |
| Color | Gray (`#9ca3af`) | Accent blue (`#3b82f6`) |
| Scale range | 0.8 → 1.0 | 1.0 → 1.1 |
| Stagger delay | 0.15s | 0.2s |

### Word Bounce + Streaming Caret (Vector RAG)

Vector RAG skips dots entirely. Its "thinking" state is a single word that fades in and bounces on the y-axis (`role="status"`, `aria-live="polite"`, `text-base` `#e0e0e0`); once tokens actually stream, it renders a pulsing caret at the tail of the text instead:

```jsx
<span className="inline-block w-1.5 h-4 bg-accent animate-pulse" />
```

## Status Messages

### Inline Status (Wedding CRM Chat)

Shows during AI agent routing:

```css
.status-message {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 8px 12px;
  background: #f5f5f5;
  border-radius: 6px;
  color: #666;
  font-size: 13px;
}
```

Contains a small spinner + text like "Routing to Data Agent..."

## Flash Notifications (Wedding CRM)

Full-width alert banners:

```css
.flash {
  padding: 1rem 1.5rem;
  border-radius: 8px;
  margin-bottom: 1.5rem;
}

.flash-success { background: #d4edda; color: #155724; }
.flash-error   { background: #f8d7da; color: #721c24; }
.flash-warning  { background: #fff3cd; color: #856404; }
.flash-info    { background: #cce5ff; color: #004085; }
```

### Error Message in Chat (Wedding CRM)

```css
.chat-message.error .msg-bubble {
  color: #b91c1c;
  background: #fef2f2;
  padding: 12px 14px;
  border-radius: 8px;
  border-left: 3px solid #ef4444;
}
```

**Pattern:** Red left border for error emphasis. Light red background. Used for API failures or model errors.

## Pulse Animations for Live Data

### DailyBrief.AI - KPI Glow

```css
@keyframes pulse-glow {
  0%, 100% { box-shadow: 0 0 20px rgba(59, 130, 246, 0.3); }
  50% { box-shadow: 0 0 40px rgba(59, 130, 246, 0.6); }
}
/* 2s ease-in-out infinite — indicates live/updating data */
```

### Not A Doc AI - Soft Pulse

```css
@keyframes pulseSoft {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.7; }
}
/* 2s ease-in-out infinite — subtle loading/processing indicator */
```

### Vector RAG - Expanding Ping

```css
@keyframes ap2ping {
  0%        { box-shadow: 0 0 0 0  color-mix(in srgb, var(--pc) 55%, transparent); }
  70%, 100% { box-shadow: 0 0 0 11px transparent; }
}
/* fresh events: 2.6s ease-out infinite · live/streaming dot (--neg #f87171): 2s */
```

### Wedding CRM - Chat Toggle Ring

```css
@keyframes pulse-ring {
  0% { box-shadow: ..., 0 0 0 0 rgba(102, 119, 86, 0.4); }
  50% { box-shadow: ..., 0 0 0 12px rgba(102, 119, 86, 0); }
  100% { box-shadow: ..., 0 0 0 0 rgba(102, 119, 86, 0); }
}
/* 2.5s ease-out infinite — draws attention to the chat button */
```

## How to Apply Loading Patterns

### For quick operations (< 2 seconds):
- Small inline spinner (12px) next to status text
- Use the typing indicator for AI/chat responses
- Disable interactive elements during loading

### For medium operations (2-30 seconds):
- Large centered spinner (48px) in an overlay
- Status text describing the current step
- Optional progress bar if steps are quantifiable

### For long operations (30+ seconds):
- Full progress bar with percentage
- Step-by-step status text updates
- Elapsed timer with `tabular-nums`
- Allow the user to continue other tasks

### For live data:
- Pulse glow animation on data indicators
- Small green status dot for connection health
- Stale data warnings when cache is outdated
- Expanding-ring "ping" (Vector RAG `ap2ping`) on fresh map events and the live streaming dot; ghost-sweep skeletons for whole cards while their data loads
