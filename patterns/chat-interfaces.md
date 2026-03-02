# Chat Interfaces

Widget-based chat (Wedding CRM) vs full-page chat (Not A Doc AI), with component patterns for both approaches.

## Architecture Comparison

| Feature | Wedding CRM | Not A Doc AI |
|---------|-------------|--------------|
| Layout | Floating widget (overlay) | Full-page panel |
| Expand | Widget → fullscreen | Always full-page |
| Sidebar | Past conversations (expanded only) | Stats panel |
| Tech | Vanilla JS + SSE streaming | React + Framer Motion |
| Input | Textarea in wrapper | Textarea with suggestions |
| Messages | Role labels above text | Directional entrance animations |
| AI features | 3-agent routing, context badge | Order results table, validation badges |

## Message Bubbles

### Wedding CRM - Role-based Messages

Messages use full-width rows with role labels:

```css
.chat-message { padding: 16px 20px; }
.chat-message.user { background: #f8f8f8; }
.chat-message.assistant { background: #fff; }

.msg-role {
  font-size: 12px;
  font-weight: 600;
  margin-bottom: 6px;
  letter-spacing: 0.01em;
}

.chat-message.user .msg-role { color: #555; }
.chat-message.assistant .msg-role { color: #5a6b4a; }

.msg-bubble {
  font-size: 14px;
  line-height: 1.65;
  color: #333;
}

/* Expanded mode: larger text */
.chat-widget.expanded .msg-bubble {
  font-size: 15px;
  line-height: 1.7;
}

/* Error state */
.chat-message.error .msg-bubble {
  color: #b91c1c;
  background: #fef2f2;
  padding: 12px 14px;
  border-radius: 8px;
  border-left: 3px solid #ef4444;
}
```

### Not A Doc AI - Directional Bubbles

Messages enter from different directions based on role:

```css
/* User messages - accent colored, right-aligned corner */
.message-user {
  background-color: #3b82f6;
  color: white;
  border-radius: 24px 24px 8px 24px;
  padding: 1rem 1.25rem;
}

/* Assistant messages - dark surface, left-aligned corner */
.message-assistant {
  background-color: #1a1a1a;
  color: #ffffff;
  border-radius: 24px 24px 24px 8px;
  padding: 1rem 1.25rem;
  border: 1px solid rgba(255, 255, 255, 0.05);
}
```

**Framer Motion entrance animations:**

```js
// User messages slide in from right
export const userMessage = {
  hidden: { opacity: 0, x: 16, scale: 0.98 },
  visible: {
    opacity: 1, x: 0, scale: 1,
    transition: { duration: 0.25, ease: [0, 0, 0.2, 1] },
  },
}

// Assistant messages slide up from below
export const assistantMessage = {
  hidden: { opacity: 0, y: 8 },
  visible: {
    opacity: 1, y: 0,
    transition: { duration: 0.25, ease: [0, 0, 0.2, 1] },
  },
}
```

## Typing Indicators

### Wedding CRM

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

### Not A Doc AI

```css
.typing-indicator {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  padding: 8px 0;
}

.typing-indicator span {
  width: 8px;
  height: 8px;
  background-color: #3b82f6;
  border-radius: 50%;
  opacity: 0.4;
  animation: typing-pulse 1.4s ease-in-out infinite;
}

.typing-indicator span:nth-child(1) { animation-delay: 0s; }
.typing-indicator span:nth-child(2) { animation-delay: 0.2s; }
.typing-indicator span:nth-child(3) { animation-delay: 0.4s; }

@keyframes typing-pulse {
  0%, 60%, 100% { opacity: 0.4; transform: scale(1); }
  30% { opacity: 1; transform: scale(1.1); }
}
```

**Comparison:** CRM uses gray dots (6px) with scale + opacity. Not A Doc AI uses accent-colored dots (8px) with scale (1.1x) + opacity. Both use 1.4s cycles with staggered delays.

## Chat Input

### Wedding CRM - Wrapper Pattern

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
  max-height: 120px;
  min-height: 20px;
}

.send-btn {
  width: 32px;
  height: 32px;
  background: #5a6b4a;
  color: white;
  border: none;
  border-radius: 8px;
}
```

### Not A Doc AI - Suggestion Buttons

On initial load, the chat panel shows clickable suggestion prompts:

```jsx
const suggestions = [
  "Show me all orders from Ohio over $500",
  "Which customers are most likely to reorder?",
  "Summarize orders by state",
]

{suggestions.map(text => (
  <motion.button
    key={text}
    variants={listItem}
    whileHover={buttonHover}
    whileTap={buttonTap}
    onClick={() => handleSend(text)}
    className="text-left px-4 py-3 rounded-2xl border border-border
               hover:border-border-hover text-sm text-text-secondary
               hover:text-text-primary transition-colors"
  >
    {text}
  </motion.button>
))}
```

## Welcome State

### Wedding CRM

```css
.chat-welcome {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  flex: 1;
  padding: 40px 24px;
  text-align: center;
}

.welcome-icon {
  width: 48px;
  height: 48px;
  background: #5a6b4a;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  margin-bottom: 20px;
}

.welcome-title { font-size: 20px; font-weight: 500; color: #1a1a1a; }
.welcome-subtitle { font-size: 14px; color: #666; max-width: 360px; }

.welcome-prompts-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  max-width: 480px;
}

.welcome-prompt {
  background: #fff;
  border: 1px solid #e0e0e0;
  padding: 12px 14px;
  border-radius: 8px;
  font-size: 13px;
  color: #333;
  cursor: pointer;
  text-align: left;
  transition: all 0.15s;
}

.welcome-prompt:hover { border-color: #bbb; background: #fafafa; }
```

## Widget Expand/Collapse

```css
/* Normal mode */
.chat-widget {
  position: fixed;
  bottom: 24px;
  right: 24px;
  width: 520px;
  height: 640px;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 20px 60px rgba(0,0,0,0.15);
  display: none;
  flex-direction: column;
  z-index: 1001;
}
.chat-widget.open { display: flex; }

/* Expanded mode */
.chat-widget.expanded {
  position: fixed !important;
  top: 0 !important;
  left: 0 !important;
  right: 0 !important;
  bottom: 0 !important;
  width: 100vw !important;
  height: 100vh !important;
  border-radius: 0 !important;
  flex-direction: row !important;  /* sidebar + main */
}
```

## Status Messages (Wedding CRM)

Inline status with spinner during agent routing:

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

.status-spinner {
  width: 12px;
  height: 12px;
  border: 2px solid #e0e0e0;
  border-top-color: #5a6b4a;
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}
```

## Markdown in Chat (Wedding CRM)

The chat renders markdown with styled elements:

```css
.msg-bubble code {
  background: #f3f4f6;
  padding: 2px 6px;
  border-radius: 4px;
  font-size: 0.9em;
  font-family: ui-monospace, 'SF Mono', Monaco, monospace;
}

.msg-bubble pre {
  background: #1e1e1e;
  color: #d4d4d4;
  padding: 14px 16px;
  border-radius: 8px;
  overflow-x: auto;
  font-size: 13px;
}

.msg-bubble blockquote {
  border-left: 3px solid #d1d5db;
  padding-left: 14px;
  color: #6b7280;
  font-style: italic;
}

.msg-bubble a { color: #5a6b4a; text-decoration: underline; }
```

## How to Apply Chat Patterns

### For a floating widget chat:
- Fixed position bottom-right with toggle button
- 520×640 default, expand to fullscreen
- Role labels above messages (not bubbles)
- Welcome state with suggestion grid
- Sidebar for conversation history (expanded only)
- Keyboard shortcut (Cmd+K) for toggle

### For a full-page AI chat:
- Directional message animations (user from right, AI from below)
- Colored bubbles with asymmetric border-radius
- Suggestion buttons on initial state
- Stagger animations for new content
- Typing indicator with accent-colored dots
