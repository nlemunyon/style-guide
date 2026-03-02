# GBH Aesthetics CRM -- Design System

> Warm organic CRM for a wedding aesthetics business. Light mode. Sage green palette creates a premium, approachable, nature-inspired feel. Clean and professional without being clinical.

---

## Color Palette

### Core Colors

| Role | Hex | Swatch | Usage |
|------|------|--------|-------|
| Background | `#f5f7f3` | ![](https://via.placeholder.com/12/f5f7f3/f5f7f3.png) | Page background, tinted warm white |
| Card / Surface | `#ffffff` | ![](https://via.placeholder.com/12/ffffff/ffffff.png) | Cards, modals, chat assistant bubbles |
| Primary Accent | `#7d8b6a` | ![](https://via.placeholder.com/12/7d8b6a/7d8b6a.png) | Buttons, active tabs, focus rings, stat values |
| Secondary Accent | `#6b7f5c` | ![](https://via.placeholder.com/12/6b7f5c/6b7f5c.png) | Hover states, stat big-numbers, darker sage |
| Dark Accent | `#5a6b4a` | ![](https://via.placeholder.com/12/5a6b4a/5a6b4a.png) | Deep sage for context badges, pressed states |

### Navbar Gradient

```css
background: linear-gradient(135deg, #7d8b6a 0%, #6b7f5c 100%);
```

| Stop | Hex | Swatch |
|------|------|--------|
| 0% | `#7d8b6a` | ![](https://via.placeholder.com/12/7d8b6a/7d8b6a.png) |
| 100% | `#6b7f5c` | ![](https://via.placeholder.com/12/6b7f5c/6b7f5c.png) |

### Chat Toggle Gradient

```css
background: linear-gradient(135deg, #667756 0%, #4a5a3a 50%, #3d4d2f 100%);
```

| Stop | Hex | Swatch |
|------|------|--------|
| 0% | `#667756` | ![](https://via.placeholder.com/12/667756/667756.png) |
| 50% | `#4a5a3a` | ![](https://via.placeholder.com/12/4a5a3a/4a5a3a.png) |
| 100% | `#3d4d2f` | ![](https://via.placeholder.com/12/3d4d2f/3d4d2f.png) |

### Text

| Role | Hex | Swatch | Usage |
|------|------|--------|-------|
| Primary | `#333333` | ![](https://via.placeholder.com/12/333333/333333.png) | Body copy, headings, table cells |
| Secondary | `#666666` | ![](https://via.placeholder.com/12/666666/666666.png) | Descriptions, meta text |
| Muted | `#999999` | ![](https://via.placeholder.com/12/999999/999999.png) | Timestamps, placeholders, timeline dates |

### Semantic Colors

| State | Background | Swatch | Text | Swatch |
|-------|-----------|--------|------|--------|
| Success | `#d4edda` | ![](https://via.placeholder.com/12/d4edda/d4edda.png) | `#155724` | ![](https://via.placeholder.com/12/155724/155724.png) |
| Warning | `#fff3cd` | ![](https://via.placeholder.com/12/fff3cd/fff3cd.png) | `#856404` | ![](https://via.placeholder.com/12/856404/856404.png) |
| Danger | `#f8d7da` | ![](https://via.placeholder.com/12/f8d7da/f8d7da.png) | `#721c24` | ![](https://via.placeholder.com/12/721c24/721c24.png) |
| Info | `#cce5ff` | ![](https://via.placeholder.com/12/cce5ff/cce5ff.png) | `#004085` | ![](https://via.placeholder.com/12/004085/004085.png) |

### Chat Panel Colors

| Role | Hex | Swatch | Usage |
|------|------|--------|-------|
| Sidebar Background | `#f7f8f6` | ![](https://via.placeholder.com/12/f7f8f6/f7f8f6.png) | Chat sidebar panel |
| Sidebar Border | `#e5e7e3` | ![](https://via.placeholder.com/12/e5e7e3/e5e7e3.png) | Sidebar right edge |
| Context Badge BG | `#eef0eb` | ![](https://via.placeholder.com/12/eef0eb/eef0eb.png) | Context indicator pill |
| Context Badge Text | `#5a6b4a` | ![](https://via.placeholder.com/12/5a6b4a/5a6b4a.png) | Badge label |

---

## Typography

### Font Stacks

```css
/* Body / UI */
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;

/* Code in chat */
font-family: ui-monospace, monospace;
```

### Type Scale

| Element | Size | Weight | Extras |
|---------|------|--------|--------|
| Navbar title (h1) | `1.5rem` | 300 | `letter-spacing: 2px` |
| Page header (h2) | `1.8rem` | 400 | -- |
| Body | inherited | 400 | `line-height: 1.6` |
| Table header (th) | `0.85rem` | 500 | `text-transform: uppercase; letter-spacing: 0.5px` |
| Filter buttons | `0.85rem` | -- | -- |
| Chat role labels | `12px` | 600 | -- |
| Chat bubble (normal) | `14px` | 400 | `line-height: 1.65` |
| Chat bubble (expanded) | `15px` | 400 | `line-height: 1.7` |

The type hierarchy relies on weight contrast rather than dramatic size jumps. The navbar title uses an ultra-light 300 weight with generous letter-spacing to feel elegant rather than bold. Table headers use uppercase at a small size with letter-spacing, establishing a quiet authority without shouting.

---

## Spacing & Layout

### Container

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}
```

### Card

```css
.card {
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  border-radius: 12px;
}
```

### Grid System

```css
/* Auto-fit responsive grid */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1.5rem;
}

/* Fixed column variants */
.grid-2 { grid-template-columns: repeat(2, 1fr); gap: 1.5rem; }
.grid-3 { grid-template-columns: repeat(3, 1fr); gap: 1.5rem; }
.grid-4 { grid-template-columns: repeat(4, 1fr); gap: 1.5rem; }
```

### Form Row

```css
.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}
```

### Chat Widget Dimensions

| Mode | Width | Height |
|------|-------|--------|
| Normal | `520px` | `640px` |
| Expanded | `100vw` (fullscreen) | `100vh` (fullscreen) |
| Mobile | `calc(100vw - 16px)` | `calc(100vh - 80px)` |

### Chat Messages Inner

| Mode | Max Width |
|------|-----------|
| Normal | `680px` |
| Expanded | `720px` |

---

## Components

### 1. Navbar

The navbar uses a sage green gradient background with flex layout. Navigation links display as pills on hover, and the user menu is separated by a left border.

```css
.navbar {
  background: linear-gradient(135deg, #7d8b6a 0%, #6b7f5c 100%);
  display: flex;
  align-items: center;
  padding: 0 2rem;
}

.navbar h1 {
  font-size: 1.5rem;
  font-weight: 300;
  letter-spacing: 2px;
  color: #fff;
}

.nav-link {
  color: rgba(255, 255, 255, 0.85);
  padding: 0.4rem 0.8rem;
  border-radius: 20px;
  transition: background 0.2s;
}

.nav-link:hover {
  background: rgba(255, 255, 255, 0.15);
  color: #fff;
}

.user-menu {
  border-left: 1px solid rgba(255, 255, 255, 0.3);
  padding-left: 1rem;
}
```

### 2. Cards

Cards use a clean white surface with a subtle shadow. The large border-radius (12px) softens the overall feel.

```css
.card {
  background: #ffffff;
  border-radius: 12px;
  padding: 1.5rem;
  margin-bottom: 1.5rem;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}
```

Big-number displays inside cards show key metrics (e.g., total contacts, revenue) with the value rendered in sage green and a small uppercase label beneath.

### 3. Stat Boxes

```css
.stat-box {
  background: #ffffff;
  border-radius: 8px;
  text-align: center;
  padding: 1.25rem;
}

.stat-box .value {
  font-size: 1.8rem;
  font-weight: 600;
  color: #6b7f5c;
}

.stat-box .label {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  color: #666;
}
```

### 4. Buttons

All buttons are pill-shaped with a 25px border-radius. The primary variant uses sage green.

```css
.btn {
  border-radius: 25px;
  padding: 0.5rem 1.25rem;
  font-size: 0.85rem;
  transition: all 0.2s;
  cursor: pointer;
}

.btn-primary {
  background: #7d8b6a;
  color: #fff;
  border: none;
}

.btn-primary:hover {
  background: #6b7f5c;
}

.btn-outline {
  background: transparent;
  border: 1px solid #7d8b6a;
  color: #7d8b6a;
}

.btn-secondary {
  background: #e9ecef;
  color: #333;
  border: none;
}

.btn-danger {
  background: #dc3545;
  color: #fff;
  border: none;
}
```

### 5. Filter Tabs

Filter tabs are pill-shaped toggles. The default state is transparent; the active state fills with sage green and switches text to white.

```css
.filter-tab {
  background: transparent;
  border: 1px solid #ddd;
  border-radius: 25px;
  padding: 0.4rem 1rem;
  font-size: 0.85rem;
  color: #666;
  cursor: pointer;
  transition: all 0.2s;
}

.filter-tab.active {
  background: #7d8b6a;
  border-color: #7d8b6a;
  color: #fff;
}
```

### 6. Badges

Badges are small pill-shaped indicators with a 20px border-radius.

**Semantic Badges:**

| Variant | Background | Text |
|---------|-----------|------|
| Green | `#d4edda` ![](https://via.placeholder.com/12/d4edda/d4edda.png) | `#155724` ![](https://via.placeholder.com/12/155724/155724.png) |
| Yellow | `#fff3cd` ![](https://via.placeholder.com/12/fff3cd/fff3cd.png) | `#856404` ![](https://via.placeholder.com/12/856404/856404.png) |
| Red | `#f8d7da` ![](https://via.placeholder.com/12/f8d7da/f8d7da.png) | `#721c24` ![](https://via.placeholder.com/12/721c24/721c24.png) |
| Blue | `#cce5ff` ![](https://via.placeholder.com/12/cce5ff/cce5ff.png) | `#004085` ![](https://via.placeholder.com/12/004085/004085.png) |
| Gray | `#e9ecef` ![](https://via.placeholder.com/12/e9ecef/e9ecef.png) | `#666` ![](https://via.placeholder.com/12/666666/666666.png) |
| Purple | `#e8daef` ![](https://via.placeholder.com/12/e8daef/e8daef.png) | `#6c3483` ![](https://via.placeholder.com/12/6c3483/6c3483.png) |

**Status Pipeline Badges:**

| Status | Color | Meaning |
|--------|-------|---------|
| Lead | Gray | New inquiry, not yet contacted |
| Contacted | Blue | Initial outreach made |
| Quoted | Yellow | Proposal / quote sent |
| Booked | Green | Contract signed, deposit received |
| Completed | Deeper green | Service delivered |
| Lost | Red | Did not convert |

```css
.badge {
  display: inline-block;
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 500;
}
```

### 7. Table

```css
table {
  width: 100%;
  border-collapse: collapse;
}

th {
  font-size: 0.85rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.5px;
  color: #666;
  padding: 0.75rem;
  text-align: left;
  border-bottom: 2px solid #e9ecef;
}

td {
  padding: 0.75rem;
  border-bottom: 1px solid #f0f0f0;
  color: #333;
}

tr:hover {
  background: #fafafa;
}
```

### 8. Timeline

The timeline uses a left border as the vertical spine, with colored dots marking different activity types.

```css
.timeline {
  border-left: 2px solid #e9ecef;
  padding-left: 1.5rem;
  margin-left: 0.5rem;
}

.timeline-item {
  position: relative;
  margin-bottom: 1.25rem;
}

.timeline-item::before {
  content: '';
  position: absolute;
  left: -1.75rem;
  top: 0.35rem;
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: #7d8b6a; /* sage default */
}

/* Activity type dot colors */
.timeline-item.email::before  { background: #28a745; } /* green */
.timeline-item.note::before   { background: #007bff; } /* blue */
.timeline-item.status::before { background: #fd7e14; } /* orange */

.timeline-date {
  font-size: 0.8rem;
  color: #999;
}

.timeline-content {
  background: #f8f9fa;
  border-radius: 8px;
  padding: 0.75rem 1rem;
  margin-top: 0.25rem;
}
```

### 9. Flash Messages

```css
.flash {
  border-radius: 8px;
  padding: 0.75rem 1.25rem;
  margin-bottom: 1rem;
}

.flash-success { background: #d4edda; color: #155724; }
.flash-warning { background: #fff3cd; color: #856404; }
.flash-danger  { background: #f8d7da; color: #721c24; }
.flash-info    { background: #cce5ff; color: #004085; }
```

### 10. Forms

Inputs use an 8px border-radius and a sage green focus ring.

```css
input, select, textarea {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 0.5rem 0.75rem;
  font-size: 0.9rem;
  transition: border-color 0.2s, box-shadow 0.2s;
}

input:focus, select:focus, textarea:focus {
  outline: none;
  border-color: #7d8b6a;
  box-shadow: 0 0 0 3px rgba(125, 139, 106, 0.15);
}
```

### 11. Chat Toggle Button

The chat toggle is a fixed-position button in the bottom-right corner with a sage gradient and a pulse-ring animation to draw attention.

```css
.chat-toggle {
  position: fixed;
  bottom: 24px;
  right: 24px;
  width: 60px;
  height: 60px;
  border-radius: 16px;
  background: linear-gradient(135deg, #667756 0%, #4a5a3a 50%, #3d4d2f 100%);
  color: #fff;
  border: none;
  cursor: pointer;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.2);
  transition: transform 0.2s, box-shadow 0.2s;
}

.chat-toggle:hover {
  transform: translateY(-3px) scale(1.05);
  box-shadow: 0 6px 28px rgba(0, 0, 0, 0.3);
}

/* Keyboard shortcut hint shown on hover */
.chat-toggle .kbd-hint {
  position: absolute;
  top: -28px;
  opacity: 0;
  transition: opacity 0.2s;
}

.chat-toggle:hover .kbd-hint {
  opacity: 1;
}
```

### 12. Chat Widget

```css
.chat-widget {
  position: fixed;
  bottom: 24px;
  right: 24px;
  width: 520px;
  height: 640px;
  border-radius: 16px;
  background: #fff;
  box-shadow: 0 8px 40px rgba(0, 0, 0, 0.15);
  display: flex;
  flex-direction: column;
  overflow: hidden;
}

/* Expanded / fullscreen mode */
.chat-widget.expanded {
  width: 100vw;
  height: 100vh;
  bottom: 0;
  right: 0;
  border-radius: 0;
}
```

### 13. Chat Sidebar (Expanded Mode)

```css
.chat-sidebar {
  width: 260px;
  background: #f7f8f6;
  border-right: 1px solid #e5e7e3;
  display: flex;
  flex-direction: column;
}

.chat-sidebar .new-chat-btn {
  margin: 1rem;
  background: #7d8b6a;
  color: #fff;
  border-radius: 25px;
}

.chat-sidebar .session-item {
  padding: 0.75rem 1rem;
  border-bottom: 1px solid #e5e7e3;
  cursor: pointer;
  transition: background 0.15s;
}

.chat-sidebar .session-item:hover {
  background: #eef0eb;
}
```

### 14. Chat Messages

```css
.chat-messages {
  flex: 1;
  overflow-y: auto;
  padding: 1rem;
}

.chat-messages-inner {
  max-width: 680px;
  margin: 0 auto;
}

.chat-widget.expanded .chat-messages-inner {
  max-width: 720px;
}

.message.user {
  background: #f8f8f8;
  border-radius: 12px;
  padding: 0.75rem 1rem;
}

.message.assistant {
  background: #ffffff;
  border-radius: 12px;
  padding: 0.75rem 1rem;
}

.message .role-label {
  font-size: 12px;
  font-weight: 600;
  margin-bottom: 0.25rem;
}

.message .bubble-text {
  font-size: 14px;
  line-height: 1.65;
}

.chat-widget.expanded .message .bubble-text {
  font-size: 15px;
  line-height: 1.7;
}
```

### 15. Chat Input Area

```css
.chat-input-area textarea {
  background: #fafafa;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 0.5rem 0.75rem;
  resize: none;
  transition: border-color 0.2s;
}

.chat-input-area textarea:focus {
  border-color: #7d8b6a;
}

.chat-send-btn {
  background: #7d8b6a;
  color: #fff;
  border: none;
  border-radius: 8px;
  padding: 0.5rem 1rem;
  cursor: pointer;
  transition: background 0.2s;
}

.chat-send-btn:hover {
  background: #6b7f5c;
}
```

### 16. Guide Modal

The guide modal slides up from below with a sage gradient header and a tinted content area.

```css
.guide-modal {
  animation: slideUp 0.25s ease;
}

.guide-modal .header {
  background: linear-gradient(135deg, #7d8b6a 0%, #6b7f5c 100%);
  color: #fff;
  padding: 1.5rem;
}

.guide-modal .content {
  background: #f5f7f3;
  padding: 1.5rem;
}
```

### 17. Typing Indicator

Three dots that pulse in sequence using a staggered scale/opacity animation.

```css
.typing-indicator {
  display: flex;
  gap: 4px;
  padding: 0.5rem;
}

.typing-indicator .dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #7d8b6a;
  animation: typingPulse 1.4s ease-in-out infinite;
}

.typing-indicator .dot:nth-child(2) { animation-delay: 0.15s; }
.typing-indicator .dot:nth-child(3) { animation-delay: 0.30s; }
```

### 18. Status Spinner

```css
.spinner {
  width: 12px;
  height: 12px;
  border: 2px solid #e9ecef;
  border-top-color: #7d8b6a;
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}
```

---

## Animations

### Keyframes

```css
@keyframes pulse-ring {
  0%   { box-shadow: 0 0 0 0 rgba(125, 139, 106, 0.5); }
  70%  { box-shadow: 0 0 0 12px rgba(125, 139, 106, 0); }
  100% { box-shadow: 0 0 0 0 rgba(125, 139, 106, 0); }
}

@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes slideUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

@keyframes typingPulse {
  0%, 100% { transform: scale(0.8); opacity: 0.4; }
  50%      { transform: scale(1);   opacity: 1; }
}

@keyframes spin {
  to { transform: rotate(360deg); }
}
```

### Animation Assignments

| Element | Animation | Duration | Timing |
|---------|-----------|----------|--------|
| Chat toggle pulse ring | `pulse-ring` | 2.5s | ease-out, infinite |
| Chat toggle hover | `translateY(-3px) scale(1.05)` | 0.2s | transition |
| Chat widget open | `fadeIn` | 0.2s | ease |
| Guide modal | `slideUp` | 0.25s | ease |
| Typing dots | `typingPulse` | 1.4s | ease-in-out, infinite, staggered 0.15s |
| Status spinner | `spin` | 0.7s | linear, infinite |

### Transition Defaults

- Standard interactions (buttons, links, cards): `0.2s`
- Subtle micro-interactions (sidebar hover, input focus): `0.15s`

---

## Responsive Behavior

### Breakpoint: 768px

The single breakpoint at 768px handles the transition from desktop to mobile.

**Navbar:**
```css
@media (max-width: 768px) {
  .navbar {
    flex-direction: column;
    padding: 1rem;
  }
}
```

**Form Rows:**
```css
@media (max-width: 768px) {
  .form-row {
    grid-template-columns: 1fr;
  }
}
```

**Grids:**
```css
@media (max-width: 768px) {
  .grid-2, .grid-3, .grid-4 {
    grid-template-columns: 1fr;
  }
}
```

**Chat Widget:**
```css
@media (max-width: 768px) {
  .chat-widget {
    width: calc(100vw - 16px);
    height: calc(100vh - 80px);
    bottom: 8px;
    right: 8px;
  }

  /* Sidebar hidden on mobile even in expanded mode */
  .chat-widget.expanded .chat-sidebar {
    display: none;
  }

  /* Welcome prompts stack vertically */
  .welcome-prompts-grid {
    grid-template-columns: 1fr;
  }
}
```

---

## Design Tokens Summary

A quick-reference for the values most commonly needed when building new components.

```css
:root {
  /* Colors */
  --color-bg:             #f5f7f3;
  --color-surface:        #ffffff;
  --color-primary:        #7d8b6a;
  --color-primary-hover:  #6b7f5c;
  --color-primary-dark:   #5a6b4a;
  --color-text:           #333333;
  --color-text-secondary: #666666;
  --color-text-muted:     #999999;
  --color-border:         #e9ecef;
  --color-border-light:   #f0f0f0;

  /* Typography */
  --font-sans:  -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
  --font-mono:  ui-monospace, monospace;
  --line-height: 1.6;

  /* Spacing */
  --radius-sm:   8px;
  --radius-md:   12px;
  --radius-lg:   16px;
  --radius-pill:  25px;
  --space-sm:    1rem;
  --space-md:    1.5rem;
  --space-lg:    2rem;

  /* Shadows */
  --shadow-card:   0 2px 10px rgba(0, 0, 0, 0.05);
  --shadow-chat:   0 8px 40px rgba(0, 0, 0, 0.15);
  --shadow-toggle: 0 4px 20px rgba(0, 0, 0, 0.2);

  /* Focus */
  --focus-ring: 0 0 0 3px rgba(125, 139, 106, 0.15);

  /* Transitions */
  --transition-default: 0.2s;
  --transition-subtle:  0.15s;
}
```

---

## How to Adapt This System

The sage green organic aesthetic and light-mode CRM layout transfer well to adjacent domains:

### 1. Day Spa or Salon Booking System

Swap the status pipeline badges (Lead/Contacted/Quoted/Booked/Completed/Lost) for appointment states (Requested/Confirmed/In-Progress/Completed/Cancelled). The timeline component maps directly to service history per client. Keep the sage palette -- it already evokes wellness and calm.

### 2. Boutique E-Commerce (Candles, Florals, Artisan Goods)

Replace the contact table with a product catalog grid using the existing card component. Stat boxes become inventory metrics and revenue KPIs. The chat widget repurposes as a customer support assistant. The warm white background and organic greens align naturally with artisan brand identity.

### 3. Event Planning Dashboard

The filter tabs become event categories (Weddings, Corporate, Social). The timeline tracks vendor milestones and deliverables instead of contact activity. The grid layout accommodates task boards and vendor cards. The existing responsive breakpoints handle tablet use during on-site event coordination.

### 4. Small Business CRM for Service Professionals

This is the most direct adaptation. Rename status pipeline stages to match the industry (e.g., for photographers: Inquiry/Consultation/Proposal/Contracted/Delivered). The AI chat widget becomes a business assistant for any service vertical. The analytics dashboard, badge system, and form components work without modification.
