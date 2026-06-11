# M13 Transitions & Animation

![Module 13 of 16](https://img.shields.io/badge/Module-13_of_16-6366f1?style=flat-square)
![Beginner](https://img.shields.io/badge/Difficulty-Beginner-4ade80?style=flat-square)
![1.5-2 hours](https://img.shields.io/badge/Time-1.5--2_hours-60a5fa?style=flat-square)
![Prerequisites: M05–M06](https://img.shields.io/badge/Prerequisites-M05–M06-94a3b8?style=flat-square)

**Topics covered:** two-state changes · `transition` · timing functions · `transform` · animatable properties · `@keyframes` · `animation` · `animation-fill-mode` · staggered delays · `prefers-reduced-motion`

---

## The Why?

A button that instantly snaps to a darker shade when hovered feels abrupt. The same button with a 150ms colour transition feels responsive and intentional. Motion is not decoration — it communicates state changes, guides attention, and makes interfaces feel polished.

Here is the mental model for this whole module: **by default, every CSS change happens instantly**. When you hover a button and its background changes, the browser jumps from the old colour to the new one in a single frame. Everything you learn here is a way of telling the browser: *"don't jump — walk."*

CSS gives you two tools for that, and they answer two different questions:

- **`transition`** — *"When this property changes from A to B, take some time doing it."* Needs something to trigger the change (hover, focus, a class change). Two states, smooth path between them.
- **`animation`** — *"Play this scripted sequence of states, on your own, as soon as you appear."* No trigger needed. Can loop forever. This is how spinners spin.

One supporting actor appears constantly alongside both: **`transform`**, the property that moves, scales, and rotates elements — the thing you most often want to animate.

The key constraint: motion should be purposeful and fast. Most UI transitions are 150–300ms. Animations that run longer than 1 second without user intent start to feel slow.

By the end of this module you will be able to:
- Explain the difference between a transition and an animation, and pick the right one
- Add smooth transitions to hover and focus states
- Use `transform` to move, scale, and rotate elements without disturbing the layout
- Write `@keyframes` animations for spinners and entrance sequences
- Stop entrance animations from "snapping back" with `animation-fill-mode`
- Respect the `prefers-reduced-motion` media query for accessibility

---

## Core Concepts

### Where Motion Comes From — Element States and `:hover`

An element on a page is not always in the same situation: right now the mouse pointer might be over it, or not; an input might have keyboard focus, or not. CSS calls these situations **states**, and it can style each state differently using **pseudo-classes** — selectors that start with a colon and attach to a normal selector.

The one you will use constantly is `:hover` — it matches an element *only while the mouse pointer is over it*:

```css
.btn {
  background-color: #2563eb;   /* state 1: normal — applies all the time */
}

.btn:hover {
  background-color: #1e3a8a;   /* state 2: applies ONLY while the pointer is over it */
}
```

Read `.btn:hover` as "a `.btn`, while hovered". While the pointer is over the button, *both* rules match — and since the `:hover` rule is more specific about the situation, its `background-color` wins. Move the pointer away and the `:hover` rule stops matching, so the button falls back to state 1.

A sibling worth knowing: `:focus` matches an element while it has keyboard focus (an input being typed in, a button reached with the Tab key). Everything this module does with `:hover` works the same with `:focus`.

Now the important part: when the pointer arrives, the browser swaps state 1 for state 2 — **instantly, in a single frame**. Move the mouse away and it snaps back just as instantly. The two states are fine; the *jump between them* is what feels cheap.

A **transition** keeps both states exactly as they are and changes only the journey: instead of teleporting from blue to darker blue, the browser calculates all the in-between colours and plays them over a duration you choose. That in-between calculation is called **interpolation** — it is the engine under everything in this module.

---

### `transition` — Smooth Travel Between Two States

Start with the two longhand properties that matter most:

```css
.btn {
  background-color: #2563eb;
  transition-property: background-color;   /* WHICH property to animate */
  transition-duration: 0.2s;               /* HOW LONG the journey takes */
}

.btn:hover {
  background-color: #1d4ed8;
}
```

That is a complete, working transition. Hover: the colour now *fades* to the darker blue over 0.2 seconds.

In practice everyone uses the shorthand. Learn to read its parts:

```css
/*           property         duration  timing-function  delay */
transition: background-color  0.2s      ease             0s;
```

- **property** — which property to animate (`background-color`, `transform`, …)
- **duration** — how long, in seconds (`0.2s`) or milliseconds (`200ms`) — same thing, pick one style
- **timing-function** — the *speed curve* of the journey (next section); optional, defaults to `ease`
- **delay** — wait before starting; optional, defaults to `0s`, rarely needed on hover effects

**Where the `transition` line goes matters.** Put it on the *base* rule, not on `:hover`:

```css
/* ✅ on the base rule — animates in BOTH directions */
.btn { transition: background-color 0.2s ease; }
.btn:hover { background-color: #1d4ed8; }

/* ❌ on :hover only — smooth on the way in, SNAPS back on the way out */
.btn:hover {
  background-color: #1d4ed8;
  transition: background-color 0.2s ease;
}
```

Why: the transition that applies is the one on the state the element is *moving toward*. Leaving hover means returning to the base state — if the base state has no transition, the return trip is instant. Putting it on the base rule covers both directions.

To animate several properties, separate them with commas:

```css
.card {
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 8px 24px rgba(0,0,0,0.12);
}
```

There is also `transition: all 0.2s ease`, which animates *every* property that changes. Convenient for experiments, but in finished code list the properties explicitly — `all` can catch properties you never meant to animate and cause jank.

---

### Timing Functions — The Speed Curve

Duration says *how long* the journey takes; the timing function says *how the speed varies along the way*. A car can cover the same road in the same time by accelerating hard then coasting, or by creeping then flooring it — same duration, very different feel.

| Value | Behaviour | Best for |
|-------|----------|----------|
| `ease` | Slow start, fast middle, slow end | Default — feels natural for most UI |
| `linear` | Constant speed | Looping animations (spinners) — any other curve makes a loop visibly "pulse" |
| `ease-in` | Starts slow, ends fast | Elements leaving the screen |
| `ease-out` | Starts fast, ends slow | Elements entering the screen — arrives quickly, settles gently |
| `ease-in-out` | Slow start and end | Back-and-forth motion |
| `cubic-bezier(x1,y1,x2,y2)` | Custom curve | When the presets are not enough |

Two rules of thumb cover 95% of cases: **`ease` for hover effects, `linear` for anything that loops.** If an entrance animation feels sluggish, try `ease-out`.

---

### `transform` — Move, Scale, Rotate Without Breaking Layout

Suppose you want a card to rise 4px on hover. You *could* change its `margin-top` — but that would shove every element below it down 4px too, because margin participates in layout. The page would shudder.

`transform` solves this: it moves the element *visually* while its original space in the layout stays reserved. Neighbours never move. As a bonus, browsers run transforms on the GPU, so they stay silky even on weak devices.

```css
/* Translate — slide the element from where it would normally be */
transform: translateX(20px);        /* 20px to the right */
transform: translateY(-8px);        /* 8px up (negative = up) */
transform: translate(-50%, -50%);   /* the classic centring trick from M09 */

/* Scale — grow or shrink from the centre */
transform: scale(1.05);    /* 5% larger */
transform: scale(0.9);     /* 10% smaller */
transform: scaleX(0);      /* squashed flat horizontally */

/* Rotate */
transform: rotate(45deg);
transform: rotate(-180deg);
```

To apply several transforms at once, put them **in one declaration, separated by spaces**:

```css
transform: translateY(-4px) scale(1.02);
```

Gotcha: writing two `transform:` lines does **not** combine them — the second declaration overwrites the first, like any repeated CSS property.

`transform` on its own is instant, like any property. The magic happens when you pair it with a transition:

```css
.card {
  transition: transform 0.2s ease;
}
.card:hover {
  transform: translateY(-4px);   /* now it glides up instead of jumping */
}
```

---

### What Can Be Animated?

Interpolation needs in-between values, so a property is animatable only if its values can be *blended*:

| Animates smoothly | Why |
|-------------------|-----|
| `transform`, `opacity` | Numbers — and the two best performers; prefer these |
| `background-color`, `color`, `border-color` | Colours blend channel by channel |
| `width`, `height`, `margin`, `top`/`left` | Lengths — work, but trigger layout recalculation; can stutter |

| Cannot animate | Why |
|----------------|-----|
| `display` | There is no halfway point between `none` and `block` |
| `font-family` | Fonts do not blend |

Practical rule: **animate `transform` and `opacity` whenever possible.** They cover movement, size, rotation, and fading — and they are the cheapest for the browser. This is why the card example uses `transform: translateY(-4px)` instead of animating `top` or `margin`.

---

### When a Trigger Isn't Enough — `@keyframes`

Transitions need a trigger: hover, focus, something changing. But a loading spinner must spin the moment it appears, forever, with nobody hovering anything. For self-running motion you script a timeline with **`@keyframes`**:

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to   { opacity: 1; }
}
```

`fadeIn` is a name you invent. `from` and `to` are the first and last frames; the browser interpolates everything between, exactly like a transition.

For more control, use percentages of the total duration — and animate several properties per frame:

```css
@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);   /* start: invisible, 20px below its spot */
  }
  to {
    opacity: 1;
    transform: translateY(0);      /* end: visible, in place */
  }
}

@keyframes pulse-ring {
  0%   { box-shadow: 0 0 0 0   rgba(239, 68, 68, 0.5); }
  70%  { box-shadow: 0 0 0 8px rgba(239, 68, 68, 0); }
  100% { box-shadow: 0 0 0 0   rgba(239, 68, 68, 0); }
}
```

A `@keyframes` block by itself does nothing — it is a recording that no one is playing. Playing it is the job of `animation`.

---

### `animation` — Playing the Timeline

Attach a keyframes sequence to an element with the `animation` properties:

```css
.enter-card {
  animation-name: slideUp;             /* which @keyframes to play */
  animation-duration: 0.4s;            /* how long one run takes */
  animation-timing-function: ease-out; /* speed curve, same values as transitions */
  animation-delay: 0s;                 /* wait before starting */
  animation-iteration-count: 1;        /* how many times; `infinite` to loop */
  animation-fill-mode: both;           /* see next section — important! */
}
```

The shorthand puts duration before name or after — order is flexible except *the first time value is the duration, the second is the delay*:

```css
/*          name     duration  timing    fill-mode */
animation: slideUp   0.4s      ease-out  both;

/* a spinner: loop forever at constant speed */
animation: spin 0.8s linear infinite;
```

Transition vs animation, side by side:

| | `transition` | `animation` |
|---|---|---|
| Starts when | a property changes (hover, focus, class change) | the element appears (or `animation` is applied) |
| States | exactly 2 — before and after | any number of keyframes |
| Loops | no | yes — `animation-iteration-count: infinite` |
| Typical use | hover/focus effects | spinners, entrance effects, attention pulses |

---

### `animation-fill-mode` — Preventing the Snap-Back

Run an entrance animation without `fill-mode` and you will meet the classic surprise: the card slides in beautifully… then **teleports back to its pre-animation state** the moment the animation ends. By default, keyframe styles apply *only while the animation is running*.

`animation-fill-mode` controls what the element looks like *outside* the animation's running time:

| Value | Behaviour |
|-------|----------|
| `none` | Default — keyframe styles vanish when the animation ends (the snap-back) |
| `forwards` | Keep the final keyframe's styles after the animation ends |
| `backwards` | Apply the *first* keyframe's styles during the delay, before it starts |
| `both` | `forwards` + `backwards` — almost always what you want |

Why `backwards` matters: with a staggered entrance, card 3 waits 160ms before animating. Without `backwards`, it sits there *fully visible* during the wait, then blinks to invisible to start its animation. With `both`, it correctly starts hidden, waits hidden, animates in, and stays.

Rule of thumb: **every entrance animation gets `both`.** Infinite loops (spinners) do not need it — they never end.

---

### `prefers-reduced-motion` — Motion as an Accessibility Setting

Some users have vestibular disorders — for them, large or constant on-screen motion causes genuine dizziness and nausea, so operating systems offer a "reduce motion" setting. CSS can read it:

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

This blanket override makes every animation and transition finish in a hundredth of a millisecond — effectively instant — for users who asked for that. Same media-query syntax you learned in M12, just querying a user preference instead of a screen width.

Make this a habit, not an afterthought: every page with animation ships with this block at the bottom of its stylesheet.

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
<summary>🔁 `animation-direction` — playing timelines backwards and forwards</summary>

By default a looping animation restarts from the first keyframe each cycle. `animation-direction: alternate` makes it play forwards, then backwards, then forwards — a smooth back-and-forth without writing mirrored keyframes:

```css
@keyframes float {
  from { transform: translateY(0); }
  to   { transform: translateY(-10px); }
}

.floating-icon {
  animation: float 2s ease-in-out infinite alternate;
}
```

The icon bobs up and down forever. Without `alternate` it would jump back to the bottom at the start of every cycle.

</details>

<details>
<summary>🔄 CSS Custom Properties in animations</summary>

CSS variables can be used inside `@keyframes`:

```css
:root { --brand-glow: rgba(37, 99, 235, 0.4); }

@keyframes pulse {
  0%, 100% { box-shadow: 0 0 0 0 var(--brand-glow); }
  50%      { box-shadow: 0 0 0 8px transparent; }
}
```

For complex interactive motion, CSS variables let you control animations from JavaScript later by updating the variable value.

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

**Scenario:** You are building a UI component showcase for **Vivid** — a design system library. One page, five demo blocks: button transitions, a card lift effect, loading spinners, a staggered entrance animation, and a pulsing notification badge. Each block introduces exactly one new concept, in the order you just read them.

See `vivid_example.html` in this folder for the finished result. Build your own before peeking.

---

### Step 1: Create the file

In `M13Transitions`, create `vivid.html` with the standard skeleton:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vivid — UI Component Showcase</title>
    <style>
      /* all CSS goes here */
    </style>
  </head>
  <body>

    <div class="showcase">
      <!-- demo blocks go here -->
    </div>

  </body>
</html>
```

---

### Step 2: Base styles

Every demo block will share the same white-card look. Add to the `<style>` block:

```css
*, *::before, *::after {
  box-sizing: border-box;
}

body {
  font-family: system-ui, sans-serif;
  background-color: #f4f4f8;
  color: #1a1a2e;
  padding: 3rem 2rem;
  margin: 0;
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
  margin: 0 0 1.5rem;
}
```

Nothing new here — flexbox from M10, box-sizing from M08.

---

### Step 3: Your first transition — buttons

Add the first demo block inside `.showcase`:

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

Now style the primary button — **deliberately without a transition first**:

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
}

.btn-primary {
  background-color: #4f46e5;
  color: white;
}

.btn-primary:hover {
  background-color: #312e81;
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(79,70,229,0.35);
}
```

**Look at it:** save, open in the browser, hover the button. It works, but everything — colour, lift, shadow — *snaps* instantly. This is the default jump.

Now add one line to `.btn`:

```css
.btn {
  /* ...existing properties... */
  transition: background-color 0.15s ease, border-color 0.15s ease,
              transform 0.15s ease, box-shadow 0.15s ease;
}
```

**Look again:** the button now glides. Same two states, different journey.

**Experiment before moving on:**
1. Change every `0.15s` to `2s` and hover — you can watch the interpolation crawl. Feel how wrong slow UI motion is. Change it back.
2. Move the `transition` line from `.btn` to `.btn-primary:hover`, hover, then move the mouse *away* — smooth in, snap out. This is why the transition lives on the base rule. Move it back.

Finish the other two buttons (their hover states reuse the same transition — it is already on `.btn`):

```css
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
  background-color: #991b1b;
  transform: translateY(-1px);
}
```

---

### Step 4: Card lift — transform + transition

Second demo block:

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
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.lift-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 12px 30px rgba(0,0,0,0.1);
}

.card-icon { font-size: 1.5rem; margin-bottom: 0.75rem; }

.lift-card h3 {
  font-size: 0.95rem;
  font-weight: 700;
  margin: 0 0 0.4rem;
}

.lift-card p {
  font-size: 0.82rem;
  color: #777;
  line-height: 1.5;
  margin: 0;
}
```

**Look at it:** hover a card — it floats up 6px and casts a deeper shadow, and *the cards next to it do not move at all*. That is `transform` keeping its hands off the layout.

**Experiment:** replace `transform: translateY(-6px)` with `margin-top: -6px` in the hover rule and hover the middle card. Watch the layout twitch. Put `transform` back.

---

### Step 5: First `@keyframes` — loading spinners

No hover here: spinners must spin on their own. Third demo block:

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

First, the timeline — one full rotation:

```css
@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}
```

Then the element that plays it:

```css
.spinner-row {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.spinner {
  border-radius: 50%;              /* circle */
  border: 3px solid #e5e5ef;       /* light grey ring */
  border-top-color: #4f46e5;       /* one purple arc — this is what you "see" spin */
  animation: spin 0.8s linear infinite;
}

.spinner-sm { width: 24px;  height: 24px; }
.spinner-md { width: 40px;  height: 40px; }
.spinner-lg { width: 56px;  height: 56px; border-width: 5px; }
```

The trick: the element is a grey ring with one side coloured. Rotating the whole element makes the coloured arc chase its tail — a spinner from one element and zero images.

Read the `animation` shorthand aloud: *play `spin`, take 0.8s per turn, at constant speed, forever.*

**Experiment:** change `linear` to `ease` — the spinner now speeds up and slows down every turn, which reads as stuttering. This is why loops use `linear`. Change it back.

---

### Step 6: Entrance animation — stagger and the snap-back

Fourth demo block:

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

The timeline — fade in while sliding up:

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
```

Play it — **deliberately without fill-mode first**:

```css
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
  animation: slideUp 0.4s ease-out;
}
```

Now stagger the three cards so they cascade in:

```css
.enter-card:nth-child(1) { animation-delay: 0ms; }
.enter-card:nth-child(2) { animation-delay: 80ms; }
.enter-card:nth-child(3) { animation-delay: 160ms; }
```

**Look at it and find the two bugs.** Refresh the page (F5) and watch closely:
- Cards 2 and 3 are *visible* during their delay, blink invisible, then animate in
- (If the animation were longer you would also see the end-state snap)

Both bugs are the missing fill-mode. Fix the `animation` line:

```css
  animation: slideUp 0.4s ease-out both;
```

**Refresh again:** every card now starts hidden, waits hidden, slides in on schedule, and stays. `both` = first keyframe applies during the delay (`backwards`) + last keyframe sticks after the end (`forwards`).

---

### Step 7: Pulsing notification badge — a looping multi-frame timeline

Fifth demo block:

```html
<div class="demo-block">
  <p class="demo-title">Pulsing badge</p>
  <div class="icon-wrap">
    <span class="icon-bell">🔔</span>
    <span class="pulse-badge">3</span>
  </div>
</div>
```

This timeline uses percentages — three frames, not just `from`/`to`:

```css
@keyframes pulse-ring {
  0%   { box-shadow: 0 0 0 0   rgba(239, 68, 68, 0.5); }  /* ring starts tight and red */
  70%  { box-shadow: 0 0 0 8px rgba(239, 68, 68, 0); }    /* expands and fades by 70% */
  100% { box-shadow: 0 0 0 0   rgba(239, 68, 68, 0); }    /* rests until the loop restarts */
}
```

The expanding "ring" is a `box-shadow` spreading outward while its colour fades to transparent. Holding 70%–100% invisible gives a pause between pulses — pulse, rest, pulse, rest.

```css
.icon-wrap {
  position: relative;     /* anchor for the absolutely-positioned badge — M09 */
  display: inline-block;
}

.icon-bell { font-size: 2rem; }

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

**Look at it:** a red badge on the bell, breathing out a fading ring every 1.5 seconds. No fill-mode needed — infinite loops never end, so there is no "after" to fill.

---

### Step 8: Respect reduced motion

At the very bottom of your `<style>` block:

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

**Test it without touching your OS settings** (Chrome/Edge):

1. Open DevTools (F12)
2. Press **Ctrl+Shift+P** (Cmd+Shift+P on Mac) to open the Command Menu
3. Type `reduced` and choose **Emulate CSS prefers-reduced-motion: reduce**

(The same option lives in the **Rendering** panel: DevTools menu ⋮ → **More tools** → **Rendering** → scroll to *Emulate CSS media feature prefers-reduced-motion*. It is not in the F1 Settings page.)

Refresh: spinners frozen, badge still, cards appear instantly. To turn it off, run the Command Menu again and choose **Do not emulate CSS prefers-reduced-motion** — motion returns.

Your page now treats motion as an enhancement, not a requirement.

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

* [ ] **Concept Check**  
  Without looking at the module, explain in your own words:
  - When you would use a `transition` and when you would need an `animation`
  - Why the `transition` property belongs on the base rule, not on `:hover`
  - What goes wrong with an entrance animation when `animation-fill-mode` is missing
  - Why spinners use `linear` while hover effects use `ease`
