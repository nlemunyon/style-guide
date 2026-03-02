# Not A Doc AI -- Design System Deep-Dive

> AI-powered natural language data query chat application built with React, Tailwind CSS, and Framer Motion.

---

## Identity & Philosophy

Not A Doc AI is a modern AI chat interface for querying order data with natural language. It shares the ultra-dark foundation with DailyBrief.AI but adds a more refined design token system, Framer Motion animations, and a chat-first layout. The interface feels like a premium AI assistant -- minimal, responsive, and precise.

The design language prioritizes **information density without clutter**. Every surface, shadow, and animation serves a functional purpose: guiding the user's eye toward AI-generated results while keeping the conversational flow effortless. The palette is deliberately restrained -- near-black backgrounds with surgical blue accents -- so that data tables, badges, and result cards command attention without competing with the chat itself.

**Tech Stack:** React 18 + Tailwind CSS + Framer Motion + CSS @theme tokens

---

## Color Palette

### @theme Token Block

```css
@theme {
  --color-primary: #0a0a0a;
  --color-secondary: #141414;
  --color-tertiary: #1a1a1a;

  --color-surface: #141414;
  --color-surface-hover: #1a1a1a;
  --color-surface-active: #242424;

  --color-text-primary: #ffffff;
  --color-text-secondary: #a3a3a3;
  --color-text-tertiary: #666666;

  --color-accent: #3b82f6;
  --color-accent-hover: #2563eb;
  --color-accent-muted: rgba(59, 130, 246, 0.15);

  --color-success: #4ade80;
  --color-success-muted: rgba(74, 222, 128, 0.15);
  --color-warning: #fbbf24;
  --color-warning-muted: rgba(251, 191, 36, 0.15);
  --color-error: #f87171;
  --color-error-muted: rgba(248, 113, 113, 0.15);

  --color-border: rgba(255, 255, 255, 0.05);
  --color-border-hover: rgba(255, 255, 255, 0.1);
  --color-border-accent: rgba(59, 130, 246, 0.3);
}
```

### Background & Surface Tiers

| Token | Value | Swatch | Usage |
|---|---|---|---|
| `--color-primary` | `#0a0a0a` | ![](https://via.placeholder.com/12/0a0a0a/0a0a0a.png) | Deepest background -- page body, chat viewport |
| `--color-secondary` | `#141414` | ![](https://via.placeholder.com/12/141414/141414.png) | Card backgrounds, sidebar, panels |
| `--color-tertiary` | `#1a1a1a` | ![](https://via.placeholder.com/12/1a1a1a/1a1a1a.png) | Elevated surfaces -- assistant bubbles, hover states |
| `--color-surface` | `#141414` | ![](https://via.placeholder.com/12/141414/141414.png) | Generic surface (aliases secondary) |
| `--color-surface-hover` | `#1a1a1a` | ![](https://via.placeholder.com/12/1a1a1a/1a1a1a.png) | Interactive surface on hover |
| `--color-surface-active` | `#242424` | ![](https://via.placeholder.com/12/242424/242424.png) | Pressed/active surface state |

### Text Hierarchy

| Token | Value | Swatch | Usage |
|---|---|---|---|
| `--color-text-primary` | `#ffffff` | ![](https://via.placeholder.com/12/ffffff/ffffff.png) | Headings, message body, primary labels |
| `--color-text-secondary` | `#a3a3a3` | ![](https://via.placeholder.com/12/a3a3a3/a3a3a3.png) | Descriptions, timestamps, metadata |
| `--color-text-tertiary` | `#666666` | ![](https://via.placeholder.com/12/666666/666666.png) | Placeholders, disabled text, hints |

### Accent & Semantic Colors

| Token | Value | Swatch | Usage |
|---|---|---|---|
| `--color-accent` | `#3b82f6` | ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) | Primary action, user bubbles, links, focus rings |
| `--color-accent-hover` | `#2563eb` | ![](https://via.placeholder.com/12/2563eb/2563eb.png) | Hovered buttons, pressed accent elements |
| `--color-accent-muted` | `rgba(59, 130, 246, 0.15)` | ![](https://via.placeholder.com/12/0e1a2f/0e1a2f.png) | Badge backgrounds, subtle accent fills |
| `--color-success` | `#4ade80` | ![](https://via.placeholder.com/12/4ade80/4ade80.png) | Positive metrics, confirmation states |
| `--color-success-muted` | `rgba(74, 222, 128, 0.15)` | ![](https://via.placeholder.com/12/0f1f14/0f1f14.png) | Success badge backgrounds |
| `--color-warning` | `#fbbf24` | ![](https://via.placeholder.com/12/fbbf24/fbbf24.png) | Caution states, validation warnings |
| `--color-warning-muted` | `rgba(251, 191, 36, 0.15)` | ![](https://via.placeholder.com/12/1f1a0a/1f1a0a.png) | Warning badge backgrounds |
| `--color-error` | `#f87171` | ![](https://via.placeholder.com/12/f87171/f87171.png) | Errors, destructive actions |
| `--color-error-muted` | `rgba(248, 113, 113, 0.15)` | ![](https://via.placeholder.com/12/1f0f0f/1f0f0f.png) | Error badge backgrounds |

### Border Tokens

| Token | Value | Usage |
|---|---|---|
| `--color-border` | `rgba(255, 255, 255, 0.05)` | Default card and divider borders |
| `--color-border-hover` | `rgba(255, 255, 255, 0.1)` | Hovered card borders, interactive edges |
| `--color-border-accent` | `rgba(59, 130, 246, 0.3)` | Focus rings, accent-bordered elements |

---

## Shadow Tokens

| Token | Value | Usage |
|---|---|---|
| `--shadow-soft` | `0 2px 8px rgba(0, 0, 0, 0.15)` | Cards, dropdowns, floating elements |
| `--shadow-soft-lg` | `0 4px 16px rgba(0, 0, 0, 0.2)` | Modals, elevated panels, popovers |
| `--shadow-glow` | `0 0 20px rgba(59, 130, 246, 0.2)` | Focused inputs, active accent elements |

```css
@theme {
  --shadow-soft: 0 2px 8px rgba(0, 0, 0, 0.15);
  --shadow-soft-lg: 0 4px 16px rgba(0, 0, 0, 0.2);
  --shadow-glow: 0 0 20px rgba(59, 130, 246, 0.2);
}
```

---

## Typography

### Font Stacks

| Token | Value | Usage |
|---|---|---|
| `--font-sans` | `'Inter', -apple-system, BlinkMacSystemFont, system-ui, sans-serif` | All body text, headings, UI labels |
| `--font-mono` | `'JetBrains Mono', 'SF Mono', Monaco, monospace` | Code blocks, raw JSON, technical data |

### OpenType Features

Inter ships with several alternate character forms. The application activates the following OpenType features for improved readability in data-heavy contexts:

```css
body {
  font-family: var(--font-sans);
  font-feature-settings: 'cv02', 'cv03', 'cv04', 'cv11';
  -webkit-font-smoothing: antialiased;
}
```

| Feature | Effect |
|---|---|
| `cv02` | Alternate `a` (single-story) |
| `cv03` | Alternate `r` (more distinct) |
| `cv04` | Alternate `i` (curved tail) |
| `cv11` | Single-story `g` |

These alternates improve legibility at smaller sizes and reduce ambiguity in numeric/data contexts.

### Type Scale

The application uses Tailwind's default scale. Common usages across components:

| Element | Size | Weight | Font |
|---|---|---|---|
| Page headings | `text-xl` / `text-2xl` | `font-semibold` (600) | Sans |
| Card titles | `text-sm` / `text-base` | `font-medium` (500) | Sans |
| Body / messages | `text-sm` | `font-normal` (400) | Sans |
| Badges | `text-xs` (0.75rem) | `font-medium` (500) | Sans |
| Code / JSON | `text-xs` / `text-sm` | `font-normal` (400) | Mono |
| Timestamps | `text-xs` | `font-normal` (400) | Sans, `--color-text-tertiary` |

---

## Custom Scrollbar

All scrollable regions use a custom thin scrollbar that blends with the dark palette:

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

The track is fully transparent so the scrollbar thumb floats over content. The `100px` border-radius produces a perfectly pill-shaped thumb at any height.

---

## Selection Highlight

Text selection uses the accent color at 30% opacity for a cohesive branded feel:

```css
::selection {
  background: rgba(59, 130, 246, 0.3);
}
```

---

## Key Components

### 1. Message Bubbles

Message bubbles are the primary visual element. User and assistant messages use distinct shapes and colors for instant role recognition.

**User Messages:**

```css
.message-user {
  background: #3b82f6;           /* --color-accent */
  color: #ffffff;                 /* --color-text-primary */
  border-radius: 24px 24px 8px 24px;
  padding: 1rem 1.25rem;
}
```

- Right-aligned in the chat viewport
- Accent blue background with white text
- The bottom-right corner is sharply clipped (8px) to create the "speech tail" pointing toward the user's side
- No border -- the solid accent fill provides enough contrast against `--color-primary`

**Assistant Messages:**

```css
.message-assistant {
  background: #1a1a1a;           /* --color-tertiary */
  color: #ffffff;                 /* --color-text-primary */
  border-radius: 24px 24px 24px 8px;
  border: 1px solid rgba(255, 255, 255, 0.05);  /* --color-border */
  padding: 1rem 1.25rem;
}
```

- Left-aligned in the chat viewport
- Elevated tertiary background with a subtle 5% white border
- The bottom-left corner is sharply clipped (8px) to create the "speech tail" pointing toward the assistant's side
- May contain inline order results tables, badge groups, and validation warnings

### 2. Typing Indicator

A three-dot pulsing animation signals that the assistant is generating a response:

```css
.typing-dot {
  width: 8px;
  height: 8px;
  background: #3b82f6;           /* --color-accent */
  border-radius: 50%;
  animation: typing-pulse 1.4s ease-in-out infinite;
}

.typing-dot:nth-child(1) { animation-delay: 0s; }
.typing-dot:nth-child(2) { animation-delay: 0.2s; }
.typing-dot:nth-child(3) { animation-delay: 0.4s; }

@keyframes typing-pulse {
  0%, 100% {
    opacity: 0.4;
    transform: scale(1);
  }
  50% {
    opacity: 1;
    transform: scale(1.1);
  }
}
```

- Three dots, each 8px diameter, rendered in accent blue
- Staggered animation delays (0s, 0.2s, 0.4s) create a cascading wave
- The 1.4s cycle with ease-in-out produces a soft, organic breathing motion
- `scale(1.1)` adds a subtle size pulse alongside the opacity change

### 3. Badges

Badges are used for filter tags, status indicators, validation warnings, and result summaries.

```css
.badge {
  display: inline-flex;
  align-items: center;
  border-radius: 100px;          /* Pill shape */
  font-size: 0.75rem;
  font-weight: 500;
  padding: 0.25rem 0.75rem;
}
```

| Variant | Background | Text Color | Usage |
|---|---|---|---|
| Accent | `rgba(59, 130, 246, 0.15)` ![](https://via.placeholder.com/12/3b82f6/3b82f6.png) | `#3b82f6` | Filter tags, active states, count badges |
| Success | `rgba(74, 222, 128, 0.15)` ![](https://via.placeholder.com/12/4ade80/4ade80.png) | `#4ade80` | Positive results, completed status |
| Warning | `rgba(251, 191, 36, 0.15)` ![](https://via.placeholder.com/12/fbbf24/fbbf24.png) | `#fbbf24` | Validation warnings, caution flags |
| Error | `rgba(248, 113, 113, 0.15)` ![](https://via.placeholder.com/12/f87171/f87171.png) | `#f87171` | Error states, failed queries |

### 4. Cards

Cards wrap panels, result groups, and stat blocks. They use the three-tier surface system.

```css
.card {
  background: #141414;           /* --color-secondary */
  border: 1px solid rgba(255, 255, 255, 0.05);  /* --color-border */
  border-radius: 20px;
  padding: 1.25rem;
}

.card:hover {
  border-color: rgba(255, 255, 255, 0.1);  /* --color-border-hover */
}
```

- 20px border-radius produces generously rounded corners
- The 1px border at 5% opacity is barely visible at rest, rising to 10% on hover
- Cards do not use box-shadow by default; `--shadow-soft` is applied selectively on floating cards

### 5. ChatPanel

The ChatPanel is the primary interaction surface. It contains:

- **Suggestion buttons** on initial load -- pre-written natural language queries the user can click to get started
- **Textarea** with dynamic height that grows as the user types (min 1 row, max ~6 rows)
- **Smooth scroll to bottom** when new messages arrive, using `scrollIntoView({ behavior: 'smooth' })`

The textarea sits in a fixed footer area with a subtle top border separating it from the message stream.

### 6. Message Component

Each message renders as a discrete block:

- **User messages:** Right-aligned, accent blue bubble, slides in from the right (see Framer Motion `userMessage` preset)
- **Assistant messages:** Left-aligned, tertiary bubble, fades in from below (see Framer Motion `assistantMessage` preset)
- **Order results table:** Rendered inline within assistant messages when query results are returned
- **Validation warnings:** Displayed as warning badges within the message body

### 7. ResultsPanel

A side panel (or tabbed section) for exploring query results in detail:

- **Tabs:** Results / Raw JSON toggle
- **Summary badge:** Shows total result count (accent badge)
- **Filter badges:** Active filters displayed as dismissible pills
- **Order cards:** Scrollable list of individual order cards, each showing key fields and a reorder probability score

### 8. StatsPanel

A dedicated panel for model and data analytics:

- **Model overview card:** Displays the active model name, version, and performance summary
- **State reorder rate:** Color-coded progress bars per state, using the semantic color scale (success for high, warning for medium, error for low)
- **Feature importance bars:** Horizontal bar chart showing which features the model weighs most heavily, rendered with accent fills

---

## Framer Motion System

All animations are defined in a central `motion.js` module and imported as variant objects. This keeps animation behavior consistent and easy to tune globally.

### Easing

```js
const EASINGS = {
  smoothOut: [0, 0, 0.2, 1]
};
```

The `smoothOut` cubic-bezier starts with zero acceleration and ends with a quick deceleration, producing a natural "slide into place" feel.

### Animation Presets

```js
// Simple fade in
const fadeIn = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: { duration: 0.2 }
  },
  exit: {
    opacity: 0,
    transition: { duration: 0.15 }
  }
};

// Fade in with upward slide
const fadeInUp = {
  hidden: { opacity: 0, y: 8 },
  visible: {
    opacity: 1,
    y: 0,
    transition: { duration: 0.25, ease: EASINGS.smoothOut }
  },
  exit: {
    opacity: 0,
    y: -4,
    transition: { duration: 0.15 }
  }
};

// Stagger container for lists
const staggerContainer = (staggerDelay = 0.04, delayChildren = 0) => ({
  hidden: {},
  visible: {
    transition: {
      staggerChildren: staggerDelay,
      delayChildren: delayChildren
    }
  }
});

// Individual list item
const listItem = {
  hidden: { opacity: 0, y: 6 },
  visible: {
    opacity: 1,
    y: 0,
    transition: { duration: 0.2, ease: EASINGS.smoothOut }
  }
};

// User chat message -- slides in from right
const userMessage = {
  hidden: { opacity: 0, x: 16, scale: 0.98 },
  visible: {
    opacity: 1,
    x: 0,
    scale: 1,
    transition: { duration: 0.25 }
  }
};

// Assistant chat message -- fades up
const assistantMessage = {
  hidden: { opacity: 0, y: 8 },
  visible: {
    opacity: 1,
    y: 0,
    transition: { duration: 0.25 }
  }
};

// Button micro-interactions
const buttonHover = {
  y: -1,
  transition: { duration: 0.15 }
};

const buttonTap = {
  scale: 0.98,
  transition: { duration: 0.1 }
};
```

### Usage Pattern

```jsx
import { motion, AnimatePresence } from 'framer-motion';
import { fadeInUp, staggerContainer, listItem, userMessage, assistantMessage } from './motion';

// Staggered list
<motion.div variants={staggerContainer()} initial="hidden" animate="visible">
  {items.map(item => (
    <motion.div key={item.id} variants={listItem}>
      {item.content}
    </motion.div>
  ))}
</motion.div>

// Chat messages with AnimatePresence
<AnimatePresence>
  {messages.map(msg => (
    <motion.div
      key={msg.id}
      variants={msg.role === 'user' ? userMessage : assistantMessage}
      initial="hidden"
      animate="visible"
    >
      <MessageBubble message={msg} />
    </motion.div>
  ))}
</AnimatePresence>

// Button with hover/tap
<motion.button whileHover={buttonHover} whileTap={buttonTap}>
  Send
</motion.button>
```

### Animation Timing Summary

| Preset | Duration | Easing | Movement |
|---|---|---|---|
| `fadeIn` | 0.2s in / 0.15s out | default | Opacity only |
| `fadeInUp` | 0.25s in / 0.15s out | smoothOut | +8px Y translate |
| `staggerContainer` | 0.04s stagger | -- | Orchestrates children |
| `listItem` | 0.2s | smoothOut | +6px Y translate |
| `userMessage` | 0.25s | default | +16px X, scale 0.98 |
| `assistantMessage` | 0.25s | default | +8px Y translate |
| `buttonHover` | 0.15s | default | -1px Y lift |
| `buttonTap` | 0.1s | default | scale 0.98 |

---

## CSS Animations

For elements outside the React tree or for lightweight animation where Framer Motion is unnecessary, the application uses CSS keyframes:

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}
/* Usage: animation: fadeIn 0.2s ease-out; */

@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
/* Usage: animation: fadeInUp 0.3s ease-out; */

@keyframes pulseSoft {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.7; }
}
/* Usage: animation: pulseSoft 2s ease-in-out infinite; */

@keyframes typing-pulse {
  0%, 100% {
    opacity: 0.4;
    transform: scale(1);
  }
  50% {
    opacity: 1;
    transform: scale(1.1);
  }
}
/* Usage: animation: typing-pulse 1.4s ease-in-out infinite; (staggered per dot) */
```

| Animation | Duration | Easing | Behavior |
|---|---|---|---|
| `fadeIn` | 0.2s | ease-out | One-shot opacity reveal |
| `fadeInUp` | 0.3s | ease-out | One-shot opacity + Y slide |
| `pulseSoft` | 2s | ease-in-out | Infinite subtle breathing |
| `typing-pulse` | 1.4s | ease-in-out | Infinite, staggered across dots |

---

## Accessibility

### Reduced Motion

The application respects the user's operating system motion preferences. When `prefers-reduced-motion: reduce` is active, all animations and transitions are effectively disabled:

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

This blanket rule sets all animation durations to a near-zero value (0.01ms) and forces animations to run exactly once, ensuring:

- No looping animations (typing indicator, pulseSoft)
- No slide/fade transitions on messages
- No hover micro-interactions
- Layout and functionality remain fully intact

### Additional Accessibility Notes

- All interactive elements are keyboard-navigable
- Focus rings use `--color-border-accent` (rgba(59, 130, 246, 0.3)) for visibility against dark backgrounds
- Contrast ratios: `--color-text-primary` (#ffffff) on `--color-primary` (#0a0a0a) exceeds WCAG AAA (21:1). `--color-text-secondary` (#a3a3a3) on `--color-primary` meets WCAG AA (9.6:1)
- The chat textarea includes appropriate ARIA labels for screen readers
- Badge color variants never rely on color alone -- each variant also uses contextual text

---

## Layout Architecture

The application uses a three-panel layout:

```
+------------------------------------------------------------------+
|  Header / Navbar                                                  |
+------------------------------------------------------------------+
|                |                    |                              |
|   StatsPanel   |    ChatPanel       |    ResultsPanel             |
|   (left)       |    (center)        |    (right)                  |
|                |                    |                              |
|   - Model      |  - Message stream  |  - Tabs: Results / JSON    |
|     overview   |  - Suggestion btns |  - Summary badge            |
|   - State      |  - Typing indicator|  - Filter badges            |
|     reorder    |  - Input textarea  |  - Order cards              |
|   - Feature    |                    |  - Reorder probability      |
|     importance |                    |                              |
|                |                    |                              |
+------------------------------------------------------------------+
```

- The **ChatPanel** is the focal point and takes the majority of horizontal space
- **StatsPanel** and **ResultsPanel** flank the chat and can collapse on smaller viewports
- All panels scroll independently with the custom scrollbar styling
- The input textarea is pinned to the bottom of the ChatPanel

---

## Design Tokens at a Glance

### Complete Token Reference

```css
@theme {
  /* Backgrounds */
  --color-primary: #0a0a0a;
  --color-secondary: #141414;
  --color-tertiary: #1a1a1a;

  /* Surfaces */
  --color-surface: #141414;
  --color-surface-hover: #1a1a1a;
  --color-surface-active: #242424;

  /* Text */
  --color-text-primary: #ffffff;
  --color-text-secondary: #a3a3a3;
  --color-text-tertiary: #666666;

  /* Accent */
  --color-accent: #3b82f6;
  --color-accent-hover: #2563eb;
  --color-accent-muted: rgba(59, 130, 246, 0.15);

  /* Semantic */
  --color-success: #4ade80;
  --color-success-muted: rgba(74, 222, 128, 0.15);
  --color-warning: #fbbf24;
  --color-warning-muted: rgba(251, 191, 36, 0.15);
  --color-error: #f87171;
  --color-error-muted: rgba(248, 113, 113, 0.15);

  /* Borders */
  --color-border: rgba(255, 255, 255, 0.05);
  --color-border-hover: rgba(255, 255, 255, 0.1);
  --color-border-accent: rgba(59, 130, 246, 0.3);

  /* Shadows */
  --shadow-soft: 0 2px 8px rgba(0, 0, 0, 0.15);
  --shadow-soft-lg: 0 4px 16px rgba(0, 0, 0, 0.2);
  --shadow-glow: 0 0 20px rgba(59, 130, 246, 0.2);

  /* Typography */
  --font-sans: 'Inter', -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', 'SF Mono', Monaco, monospace;
}
```

---

## How to Adapt

The Not A Doc AI design system is intentionally generic enough to power any AI chat-first application. Below are four adaptation paths:

### 1. Customer Support AI Chatbot

- Swap `--color-accent` to brand color
- Replace suggestion buttons with common support queries ("Track my order", "Return policy")
- Replace ResultsPanel with a ticket/order detail panel
- Add a satisfaction rating component in the assistant message footer

### 2. Code Assistant / Pair Programming Tool

- Expand `--font-mono` usage -- make it the default for all message content
- Add syntax-highlighted code blocks inside assistant messages (use a library like Prism or Shiki)
- Replace ResultsPanel with a file tree or diff viewer
- Add a "Copy code" button to assistant messages using `buttonHover`/`buttonTap` presets

### 3. Data Exploration / SQL Assistant Interface

- Keep the existing color system as-is (it is already optimized for data density)
- Replace order cards in ResultsPanel with a full data table component (sortable columns, pagination)
- Add a SQL preview toggle inside assistant messages
- Extend StatsPanel with query execution time, row counts, and schema browser

### 4. Internal Knowledge Base Search Tool

- Replace the chat-first layout with a search-first layout (large search bar at top, results below)
- Use cards for document results instead of order cards
- Add relevance score badges (accent variant) to each result
- Keep the assistant message pattern for follow-up questions and refinement
