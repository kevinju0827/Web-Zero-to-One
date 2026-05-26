# M13 Transitions & Animation

![Module 13 of 16](https://img.shields.io/badge/Module-13_of_16-6366f1?style=flat-square)
![Beginner](https://img.shields.io/badge/Difficulty-Beginner-4ade80?style=flat-square)
![1.5-2 hours](https://img.shields.io/badge/Time-1.5--2_hours-60a5fa?style=flat-square)
![Prerequisites: M01–M12](https://img.shields.io/badge/Prerequisites-M01–M12-94a3b8?style=flat-square)

**Topics covered:** `transition` · timing functions · `transform` · `@keyframes` · `animation` · `animation-fill-mode` · `animation-iteration-count` · `prefers-reduced-motion`

---

## The Why?

A button that instantly snaps to a darker shade when hovered feels abrupt. The same button with a 150ms colour transition feels responsive and intentional. Motion is not decoration — it communicates state changes, guides attention, and makes interfaces feel polished.

CSS provides two tools for motion: **transitions** (animate between two states triggered by user interaction) and **animations** (run independently with a defined sequence of keyframes). Together they cover almost every UI motion pattern — hover effects, loading spinners, entrance animations, and micro-interactions.

The key constraint: motion should be purposeful and fast. Most UI transitions are 150–300ms. Animations that run for longer than 1 second without user intent start to feel slow.

By the end of this module you will be able to:
- Add smooth transitions to hover and focus states
- Use `transform` to move, scale, and rotate elements
- Write `@keyframes` animations for repeating effects and entrance sequences
- Respect the `prefers-reduced-motion` media query for accessibility

---

## Core Concepts

### `transition`

Animates a CSS property change between two states (e.g., default and `:hover`).

```css
/* transition: property duration timing-function delay */
.button {
  background-color: #2563eb;
  transition: background-color 0.2s ease;
}

.button:hover {
  background-color: #1d4ed8;
}
```

Transition multiple properties:

```css
.card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.12);
}
```

Use `all` to transition every changed property (convenient but less precise):

```css
.element { transition: all 0.2s ease; }
```

---

### Timing Functions

| Value | Behaviour |
|-------|----------|
| `ease` | Slow start, fast middle, slow end — default, feels natural |
| `linear` | Constant speed — good for looping animations |
| `ease-in` | Starts slow, ends fast |
| `ease-out` | Starts fast, ends slow — best for elements entering the screen |
| `ease-in-out` | Slow start and end — good for back-and-forth motion |
| `cubic-bezier(x1,y1,x2,y2)` | Custom curve |

---

### `transform`

Moves, scales, rotates, or skews elements without affecting document flow.

```css
/* Translate — move without affecting surrounding elements */
transform: translateX(20px);
transform: translateY(-8px);
transform: translate(-50%, -50%);   /* centering trick */

/* Scale — resize from the transform-origin point */
transform: scale(1.05);     /* 5% larger */
transform: scaleX(0);       /* collapsed horizontally */

/* Rotate */
transform: rotate(45deg);
transform: rotate(-180deg);

/* Combine multiple transforms in one declaration */
transform: translateY(-4px) scale(1.02);
```

`transform` is GPU-accelerated — prefer it over changing `top`/`left`/`width` for smooth animations.

---

### `@keyframes`

Defines a named sequence of CSS states. Each percentage (or `from`/`to`) is a keyframe.

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}
```

---

### `animation`

Applies a `@keyframes` sequence to an element.

```css
/* animation: name duration timing-function delay iteration-count direction fill-mode */
.card {
  animation: slideUp 0.4s ease-out both;
}

.spinner {
  animation: spin 1s linear infinite;
}

/* Long form */
.element {
  animation-name: fadeIn;
  animation-duration: 0.5s;
  animation-timing-function: ease-out;
  animation-delay: 0.1s;
  animation-iteration-count: 1;    /* or infinite */
  animation-fill-mode: both;       /* keep end-state styles after animation */
}
```

---

### `animation-fill-mode`

| Value | Behaviour |
|-------|----------|
| `none` | Default — element snaps back to original state when animation ends |
| `forwards` | Holds the final keyframe state after the animation ends |
| `backwards` | Applies the first keyframe state during the delay period |
| `both` | Combines forwards + backwards — usually what you want |

---

### `prefers-reduced-motion`

Some users have vestibular disorders or motion sensitivity — auto-playing animations can cause discomfort. Always wrap non-essential animations in this media query:

```css
@keyframes slideUp { ... }

.card {
  animation: slideUp 0.4s ease-out both;
}

/* Disable animation for users who prefer reduced motion */
@media (prefers-reduced-motion: reduce) {
  .card {
    animation: none;
  }
}
```

---

## Going Further

<details>
<summary>🎯 `transform-origin` — changing the pivot point</summary>

By default, transforms happen from the element's centre (`50% 50%`). `transform-origin` changes that:

```css
.card { transform-origin: top left; }
.card:hover { transform: scale(1.05); }
/* Card expands from its top-left corner, not its centre */

.badge { transform-origin: center bottom; }
.badge:hover { transform: rotate(10deg); }
/* Badge rotates around its bottom-centre like a door hinge */
```

Common values: `center` (default), `top left`, `bottom right`, `50% 100%`, `0 0`.

</details>

<details>
<summary>⏱️ Staggered animations with `animation-delay`</summary>

Apply the same animation to multiple elements with increasing delays to create a stagger effect:

```css
.card { animation: slideUp 0.4s ease-out both; }

.card:nth-child(1) { animation-delay: 0ms; }
.card:nth-child(2) { animation-delay: 80ms; }
.card:nth-child(3) { animation-delay: 160ms; }
.card:nth-child(4) { animation-delay: 240ms; }
```

This makes the cards appear to cascade in one by one. In JavaScript frameworks this is often handled dynamically — in plain CSS, `:nth-child` works for a known number of items.

</details>

<details>
<summary>🔄 CSS Custom Properties in animations</summary>

CSS variables can be used inside `@keyframes` and animated indirectly:

```css
:root { --card-offset: 0px; }

@keyframes pulse {
  0%, 100% { box-shadow: 0 0 0 0 rgba(37, 99, 235, 0.4); }
  50%       { box-shadow: 0 0 0 8px rgba(37, 99, 235, 0); }
}

.ping-button {
  animation: pulse 2s ease-in-out infinite;
}
```

For complex interactive motion, CSS variables let you control animations from JavaScript by updating the variable value.

</details>

<details>
<summary>🤖 AI and CSS animation</summary>

Animation is one of the weaker areas for AI-generated CSS:

- **`animation-fill-mode` forgotten** — elements snap back to their original state at the end of an entrance animation. Ask for `fill-mode: both` explicitly.
- **No `prefers-reduced-motion`** — almost never included unless requested.
- **`transition: all`** — AI uses this liberally; it can cause unintended animations on properties like `height` or `clip-path` that have poor performance.
- **Overly long durations** — AI tends to generate animations that run 0.5–1s when 0.15–0.3s would feel snappier.

Useful AI prompts:
- *"Add entrance animations to these cards with a stagger delay of 80ms per card. Use animation-fill-mode: both and include a prefers-reduced-motion override."*
- *"Convert this CSS transition to a @keyframes animation so I can control the timing curve more precisely."*

</details>

---

## Guided Practice

**Scenario:** You are building a UI component showcase for **Vivid** — a design system library. The page demonstrates hover transitions, loading spinners, entrance animations, and a pulsing notification badge.

See `vivid_example.html` in this folder for the finished result.

---

### Step 1: Create the file

In `M13Transitions`, create `vivid.html`. Title: `Vivid — UI Component Showcase`. Add an empty `<style>` block.

---

### Step 2: Add the global reset and base

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: system-ui, sans-serif;
  background-color: #f4f4f8;
  color: #1a1a2e;
  padding: 3rem 2rem;
}

.showcase {
  max-width: 900px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  gap: 4rem;
}

.demo-block {
  background-color: white;
  border: 1px solid #e5e5ef;
  border-radius: 16px;
  padding: 2rem;
}

.demo-title {
  font-size: 0.72rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.15em;
  color: #8888aa;
  margin-bottom: 1.5rem;
}
```

---

### Step 3: Button hover transitions

```html
<div class="demo-block">
  <p class="demo-title">Button transitions</p>
  <div class="btn-row">
    <button class="btn btn-primary">Save changes</button>
    <button class="btn btn-outline">Cancel</button>
    <button class="btn btn-danger">Delete</button>
  </div>
</div>
```

```css
.btn-row {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.btn {
  padding: 0.6rem 1.5rem;
  border-radius: 8px;
  font-size: 0.9rem;
  font-weight: 600;
  cursor: pointer;
  border: 2px solid transparent;
  /* transition: animate background, border, transform, and shadow together */
  transition: background-color 0.15s ease, border-color 0.15s ease,
              transform 0.15s ease, box-shadow 0.15s ease;
}

.btn-primary {
  background-color: #4f46e5;
  color: white;
}

.btn-primary:hover {
  background-color: #4338ca;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(79,70,229,0.35);
}

.btn-outline {
  background-color: transparent;
  color: #4f46e5;
  border-color: #4f46e5;
}

.btn-outline:hover {
  background-color: #4f46e5;
  color: white;
}

.btn-danger {
  background-color: #ef4444;
  color: white;
}

.btn-danger:hover {
  background-color: #dc2626;
  transform: translateY(-1px);
}
```

---

### Step 4: Card lift effect

```html
<div class="demo-block">
  <p class="demo-title">Card hover effect</p>
  <div class="card-row">
    <div class="lift-card">
      <div class="card-icon">🎨</div>
      <h3>Design tokens</h3>
      <p>Colours, spacing, and typography as reusable variables.</p>
    </div>
    <div class="lift-card">
      <div class="card-icon">🧩</div>
      <h3>Components</h3>
      <p>Buttons, inputs, cards, and modals ready to use.</p>
    </div>
    <div class="lift-card">
      <div class="card-icon">📐</div>
      <h3>Layout system</h3>
      <p>Flex and grid utilities for consistent spacing.</p>
    </div>
  </div>
</div>
```

```css
.card-row {
  display: flex;
  gap: 1.25rem;
}

.lift-card {
  flex: 1;
  background-color: #fafafd;
  border: 1px solid #e5e5ef;
  border-radius: 12px;
  padding: 1.5rem;
  cursor: pointer;
  /* transition: combine transform and shadow for a lift effect */
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.lift-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 30px rgba(0,0,0,0.1);
}

.card-icon {
  font-size: 1.5rem;
  margin-bottom: 0.75rem;
}

.lift-card h3 {
  font-size: 0.95rem;
  font-weight: 700;
  margin-bottom: 0.4rem;
}

.lift-card p {
  font-size: 0.82rem;
  color: #777;
  line-height: 1.5;
}
```

---

### Step 5: Loading spinner with `@keyframes`

```html
<div class="demo-block">
  <p class="demo-title">Loading states</p>
  <div class="spinner-row">
    <div class="spinner spinner-sm"></div>
    <div class="spinner spinner-md"></div>
    <div class="spinner spinner-lg"></div>
  </div>
</div>
```

```css
@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

.spinner-row {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.spinner {
  border-radius: 50%;
  border: 3px solid #e5e5ef;
  border-top-color: #4f46e5;   /* single coloured arc creates spinner illusion */
  animation: spin 0.8s linear infinite;
}

.spinner-sm { width: 24px;  height: 24px; }
.spinner-md { width: 40px;  height: 40px; }
.spinner-lg { width: 56px;  height: 56px; border-width: 5px; }
```

---

### Step 6: Entrance animation with `@keyframes slideUp`

```html
<div class="demo-block">
  <p class="demo-title">Entrance animation</p>
  <div class="enter-cards">
    <div class="enter-card">First</div>
    <div class="enter-card">Second</div>
    <div class="enter-card">Third</div>
  </div>
</div>
```

```css
@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.enter-cards {
  display: flex;
  gap: 1rem;
}

.enter-card {
  flex: 1;
  background-color: #4f46e5;
  color: white;
  border-radius: 10px;
  padding: 1.5rem;
  text-align: center;
  font-weight: 700;
  /* animation-fill-mode: both — keeps end state; applies first frame during delay */
  animation: slideUp 0.4s ease-out both;
}

/* Stagger with animation-delay */
.enter-card:nth-child(1) { animation-delay: 0ms; }
.enter-card:nth-child(2) { animation-delay: 100ms; }
.enter-card:nth-child(3) { animation-delay: 200ms; }
```

---

### Step 7: Pulsing notification badge

```html
<div class="demo-block">
  <p class="demo-title">Pulsing badge</p>
  <div class="icon-group">
    <div class="icon-wrap">
      <span class="icon-bell">🔔</span>
      <span class="pulse-badge">3</span>
    </div>
  </div>
</div>
```

```css
@keyframes pulse-ring {
  0%   { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0.5); }
  70%  { box-shadow: 0 0 0 8px rgba(239, 68, 68, 0); }
  100% { box-shadow: 0 0 0 0 rgba(239, 68, 68, 0); }
}

.icon-group {
  display: flex;
  gap: 2rem;
}

.icon-wrap {
  position: relative;
  display: inline-block;
}

.icon-bell {
  font-size: 2rem;
}

.pulse-badge {
  position: absolute;
  top: -6px;
  right: -8px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background-color: #ef4444;
  color: white;
  font-size: 0.65rem;
  font-weight: 700;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: pulse-ring 1.5s ease-out infinite;
}
```

---

### Step 8: Add `prefers-reduced-motion`

At the bottom of your `<style>` block, add:

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

This disables all animations for users who have requested reduced motion in their OS settings (Settings → Accessibility → Reduce Motion on macOS/iOS).

---

### Step 9: Ask AI to enhance

Paste your `vivid.html` into Gemini and prompt:

> *"Here is a UI showcase page with CSS transitions and animations. Add CSS to: add a ripple effect to the buttons on click using a @keyframes animation with transform: scale and opacity, add a skeleton loading shimmer animation using a linear-gradient that moves across placeholder boxes, and add a progress bar at the top of the page that animates from 0% to 100% width over 3 seconds on page load. Include a prefers-reduced-motion override. Keep all existing CSS intact."*

Save as `vivid_styled.html`.

---

## Checkpoints

* [ ] **Micro-interaction Set**  
  Build a page demonstrating five distinct micro-interactions. Requirements:
  - Toggle switch: `<input type="checkbox">` styled as a pill with a sliding circle — use CSS `:checked` and `transition` on `transform: translateX()`
  - Accordion: three `<details>` elements — style `summary` and add a `transition` on `max-height` or use the built-in open/close animation
  - Progress bar: animated `width` from `0%` to a set percentage using `@keyframes` and `animation-fill-mode: forwards`
  - Tooltip: appears on hover with a `transition` on `opacity` and `transform: translateY(-4px)`
  - Floating label input: `<label>` that moves above the `<input>` on focus using `transform: translateY()` and `transition`

* [ ] **Card Entrance Sequence**  
  Build a page with 6 project cards that animate in when the page loads. Requirements:
  - Cards use `@keyframes` with `opacity` (0 → 1) and `translateY` (20px → 0)
  - Each card has a progressively longer `animation-delay` (80ms increments)
  - `animation-fill-mode: both` so cards start invisible before the animation begins
  - On hover, each card lifts with `transform: translateY(-6px)` and a `box-shadow` — both animated with `transition`
  - Full `prefers-reduced-motion: reduce` override that disables all animation/transition
