# M05 CSS Basics

![Module 5 of 15](https://img.shields.io/badge/Module-5_of_15-6366f1?style=flat-square)
![Beginner](https://img.shields.io/badge/Difficulty-Beginner-4ade80?style=flat-square)
![1.5-2 hours](https://img.shields.io/badge/Time-1.5--2_hours-60a5fa?style=flat-square)
![Prerequisites: M01–M04](https://img.shields.io/badge/Prerequisites-M01–M04-94a3b8?style=flat-square)

**Topics covered:** CSS syntax · `<style>` tag · element / class / ID selectors · descendant selector · grouping · universal selector · pseudo-classes · the cascade · specificity

---

## The Why?

Every page you have built so far looks like a wall of text — plain black content on a white background. HTML describes *what* the content is. It has almost nothing to say about *how* it looks. That job belongs to **CSS** (Cascading Style Sheets).

Consider the inline `style` attribute you may have seen before: `<p style="color: red;">`. It works, but imagine a page with 50 paragraphs. You would have to paste that attribute on every single `<p>` tag. Change your mind about the colour? Edit it 50 times. This approach breaks down immediately in any real project.

CSS solves this by separating *presentation* from *content*. Write one rule — target all 50 paragraphs in a single declaration. Update the colour once; it changes everywhere. This is the principle behind the phrase **separation of concerns**: HTML owns the structure, CSS owns the appearance.

By the end of this module you will be able to:
- Write valid CSS rules and understand the syntax
- Target HTML elements using element, class, and ID selectors
- Use descendant, grouping, universal, and pseudo-class selectors
- Explain what the cascade is and predict which rule wins a conflict
- Understand specificity and why it matters

---

## Core Concepts

### How CSS Connects to HTML

There are three ways to add CSS to an HTML page:

**1. Inline `style` attribute — avoid for anything non-trivial**

```html
<p style="color: red;">Text</p>
```

Only appropriate for one-off overrides. Hard to maintain and overrides the cascade in ways that are difficult to undo.

**2. `<style>` block in `<head>` — used throughout this course**

```html
<head>
  <style>
    p {
      color: #374151;
      line-height: 1.7;
    }
  </style>
</head>
```

**3. External stylesheet — the production standard**

```html
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

The CSS lives in a separate `.css` file. One stylesheet can be shared across hundreds of pages — change it once and every page updates. This course uses `<style>` blocks for simplicity, but the rules you write are identical either way.

---

### CSS Rule Anatomy

Every CSS rule has two parts: a **selector** that targets elements, and a **declaration block** that lists the styles to apply.

```css
selector {
  property: value;
  property: value;
}
```

```mermaid
graph LR
    SEL["selector\n.article-card"]
    BLOCK["declaration block { }"]
    D1["property: value\nborder: 1px solid #e2e8f0"]
    D2["property: value\npadding: 1.5rem"]
    D3["property: value\nmargin-bottom: 2rem"]
    SEL --> BLOCK
    BLOCK --> D1
    BLOCK --> D2
    BLOCK --> D3
```

**Terminology:**
- **Selector** — which elements to target
- **Property** — what aspect to change (`color`, `font-size`, `background-color`)
- **Value** — the setting to apply (`red`, `24px`, `#f8fafc`)
- **Declaration** — one `property: value` pair, ending with a semicolon
- **Declaration block** — all the declarations wrapped in `{ }`

**CSS comments** use `/* */`:

```css
/* This styles all paragraphs */
p {
  color: #374151; /* dark grey */
}
```

---

### Element Selector

Targets **every instance** of a tag. The simplest selector — just write the tag name.

```css
p {
  font-family: system-ui, sans-serif;
  line-height: 1.7;
}

h2 {
  color: #1e3a8a;
}
```

Use element selectors to establish global defaults — all `<p>` tags share the same base font, all `<h2>` tags share a colour. Individual exceptions are handled with class or ID selectors.

---

### Class Selector: `.classname`

Targets **any element** that carries a specific `class` attribute. Use a period `.` before the class name in CSS.

```html
<p class="intro">Welcome to Pulse Magazine.</p>
<p>This is a normal paragraph.</p>
<h3 class="intro">Also styled as intro.</h3>
```

```css
.intro {
  font-size: 1.2rem;
  font-weight: bold;
  color: #0f172a;
}
```

A single element can carry multiple classes — just separate them with a space:

```html
<span class="genre-tag featured">Album Review</span>
```

```css
.genre-tag  { background-color: #f1f5f9; padding: 0.25rem 0.5rem; }
.featured   { background-color: #dbeafe; color: #1d4ed8; }
```

Both sets of styles apply simultaneously.

---

### ID Selector: `#id`

Targets **one specific element** by its `id` attribute. Use `#` before the ID name in CSS. An ID value must be unique on the page — no two elements should share the same `id`.

```html
<header id="site-header">
  <h1>Pulse</h1>
</header>
```

```css
#site-header {
  background-color: #0f172a;
  color: white;
  text-align: center;
}
```

Use ID selectors for unique, one-off elements: a site header, a hero banner, a main navigation bar. For anything repeated, use a class.

---

### Descendant Selector

Targets elements **inside** a specific ancestor. Write the ancestor first, then a space, then the target.

```css
/* Only <a> tags inside <nav> — not <a> tags elsewhere */
nav a {
  color: #475569;
  text-decoration: none;
}

/* Only <p> tags inside .article-card */
.article-card p {
  font-size: 0.95rem;
}
```

Descendant selectors let you style elements differently depending on where they appear in the page — the same `<a>` tag can look different inside a navigation versus inside a paragraph.

---

### Grouping Selector: `,`

Apply the same styles to multiple selectors at once using a comma.

```css
/* h1, h2, and h3 all get the same font */
h1, h2, h3 {
  font-family: Georgia, serif;
}

/* Two different classes get the same border */
.article-card, .sidebar-card {
  border: 1px solid #e2e8f0;
  border-radius: 8px;
}
```

---

### Universal Selector: `*`

Matches **every element** on the page. Useful for applying a rule globally — for example, setting `box-sizing` (covered in M08):

```css
/* Make width include padding and border on every element */
*, *::before, *::after {
  box-sizing: border-box;
}
```

Unlike element or class selectors, `*` carries zero specificity, so any other selector can override it.

---

### Pseudo-class Selectors

A pseudo-class targets an element based on its **state** or **position**, not just its tag, class, or ID. Write a colon `:` after the selector.

**Interaction states:**

```css
/* Change colour when the user hovers */
nav a:hover {
  color: #2563eb;
}

/* Style a button when it is clicked/active */
button:active {
  background-color: #1d4ed8;
}
```

**Structural pseudo-classes:**

```css
/* First <li> inside any list */
li:first-child { font-weight: bold; }

/* Last <li> inside any list */
li:last-child  { border-bottom: none; }

/* Every even-numbered row in a table */
tr:nth-child(even) { background-color: #f8fafc; }

/* Third element */
.card:nth-child(3) { border-color: #6366f1; }
```

---

### The Cascade

CSS stands for *Cascading* Style Sheets. The cascade is the algorithm the browser uses to decide which rule applies when multiple rules target the same element.

**Rule 1 — Specificity.** More specific selectors beat less specific ones (see next section).

**Rule 2 — Source order.** When specificity is equal, the rule that appears **later** in the stylesheet wins.

```css
p {
  color: blue;   /* written first */
}

p {
  color: green;  /* written second — this wins */
}
```

This means the order you write rules matters. Global defaults go first; overrides go later.

---

### Specificity

Specificity is a score the browser assigns to each selector. The selector with the **higher score** wins the conflict.

```mermaid
graph LR
    A["① Inline style\nstyle='color:red'\nHighest — always wins"]
    B["② ID selector\n#banner"]
    C["③ Class / attribute /\npseudo-class selector\n.highlight · :hover"]
    D["④ Element selector\np · h1 · div\nLowest"]
    A -->|beats| B -->|beats| C -->|beats| D
```

**Practical examples:**

```css
p              { color: black; }   /* Element — lowest specificity */
.intro         { color: blue;  }   /* Class — beats element */
#hero          { color: green; }   /* ID — beats class */
```

```html
<!-- Which colour wins? -->
<p id="hero" class="intro">Text</p>
```

Answer: **green** — the ID selector has the highest specificity.

**`!important`** — overrides all specificity rules:

```css
p { color: red !important; }
```

Treat `!important` as a last resort. It breaks the natural cascade and makes debugging painful. If you need it often, the real problem is a specificity design issue, not a missing `!important`.

---

## Going Further

<details>
<summary>📄 External stylesheets and the `<link>` tag</summary>

In production, CSS never lives in a `<style>` block — it lives in one or more separate `.css` files. This allows the same styles to be shared across every page of a site.

**File structure:**
```
project/
├── index.html
├── about.html
└── style.css       ← one CSS file for both pages
```

**HTML — link the stylesheet in `<head>`:**
```html
<link rel="stylesheet" href="style.css">
```

**Why this matters:**
- The browser caches `style.css` after the first request — subsequent pages load faster because the CSS is already stored locally
- One change to `style.css` updates every page simultaneously
- Keeps HTML files clean and readable

The path in `href` follows the same relative vs absolute rules you learned in M02.

</details>

<details>
<summary>🧮 Specificity — the 0,0,0 calculation</summary>

Specificity can be calculated as three numbers: `(ID, Class, Element)`.

| Selector | Score |
|----------|-------|
| `p` | 0, 0, 1 |
| `.intro` | 0, 1, 0 |
| `p.intro` | 0, 1, 1 |
| `#hero` | 1, 0, 0 |
| `#hero p` | 1, 0, 1 |
| `#hero .intro p` | 1, 1, 1 |

Compare left to right: a single `1` in the ID column beats any number of class or element points. `#hero` (1,0,0) always beats `.intro.highlight.active` (0,3,0).

Practical implication: avoid styling everything with IDs. An ID-heavy stylesheet is difficult to override without reaching for `!important`.

</details>

<details>
<summary>🎨 CSS custom properties (variables)</summary>

CSS custom properties let you store values in named variables and reuse them throughout your stylesheet. They are declared with a `--` prefix, typically on `:root` to make them globally available.

```css
:root {
  --color-primary:   #2563eb;
  --color-surface:   #f8fafc;
  --font-body:       system-ui, sans-serif;
  --spacing-section: 3rem;
}

h1, h2 {
  color: var(--color-primary);
}

.card {
  background-color: var(--color-surface);
  padding: var(--spacing-section);
  font-family: var(--font-body);
}
```

Update `--color-primary` in one place and every heading and border that uses it changes instantly. This is the CSS equivalent of a design token system — it is why CSS variables are now a standard feature of professional stylesheets.

</details>

<details>
<summary>🤖 Using AI to write CSS selectors</summary>

Selectors are one of the most natural things to ask AI for. Useful prompts:

- *"Write CSS to target all `<a>` tags inside `.nav-menu`, but only when hovered."*
- *"How do I select every odd-numbered `.card` element?"*
- *"My `.title` class is not applying to my `<h2>`. Here is my HTML and CSS — what is overriding it?"*

**Debugging specificity with AI:**  
Paste both the conflicting HTML and the conflicting CSS rules. Ask: *"Which of these CSS rules will win, and why?"* AI is excellent at explaining specificity conflicts.

**Caution:** AI occasionally generates overly specific selectors (`div > ul > li > a`) when a simple class selector would do. If the generated CSS looks complicated, ask it to simplify.

</details>

---

## Guided Practice

**Scenario:** You are building the homepage for **Bloom** — a fictional indoor plant and flower shop. The page has a branded header, a navigation bar, a product listing, and one featured product that needs to stand out from the rest using the cascade.

See `pulse_example.html` in this folder for the finished result.

---

### Step 1: Create the file

In `M05CSSBasics`, create `bloom.html` with the standard document skeleton. Set the title to `Bloom — Indoor Plants & Flowers`. Add an empty `<style>` block inside `<head>` — all CSS for this exercise goes there.

---

### Step 2: Add the HTML structure

Inside `<body>`, add:

```html
<header id="site-header">
  <h1>Bloom</h1>
  <p>Indoor plants and seasonal flowers, delivered.</p>
</header>

<nav>
  <a href="#">Plants</a>
  <a href="#">Flowers</a>
  <a href="#">Care Guides</a>
  <a href="#">About</a>
</nav>

<div class="content">

  <h2>Popular This Week</h2>

  <article class="product" id="featured">
    <span class="sale">SALE</span>
    <h3>Monstera Deliciosa</h3>
    <p>The iconic split-leaf plant. Thrives in indirect light. Ships in a 6-inch nursery pot.</p>
    <p><span class="price">$24.00</span> &nbsp; <s>$32.00</s></p>
    <a href="#">Add to cart</a>
  </article>

  <article class="product">
    <h3>Pothos (Golden)</h3>
    <p>Near-indestructible trailing vine. Perfect for beginners. Survives low light and irregular watering.</p>
    <p class="price">$12.00</p>
    <a href="#">Add to cart</a>
  </article>

  <article class="product">
    <h3>Snake Plant</h3>
    <p>Architectural, upright leaves. Tolerates drought. Ships in a 4-inch pot.</p>
    <p class="price">$18.00</p>
    <a href="#">Add to cart</a>
  </article>

  <h2>Seasonal Flowers</h2>

  <article class="product">
    <span class="sale">SALE</span>
    <h3>Garden Roses — Summer Mix</h3>
    <p>Six stems, mixed pastel hues. Fragrant and long-lasting. Arrives in water-sealed packaging.</p>
    <p><span class="price">$22.00</span> &nbsp; <s>$28.00</s></p>
    <a href="#">Add to cart</a>
  </article>

</div>

<footer>
  <p>&copy; 2026 Bloom Plants &middot; Free delivery on orders over $40</p>
</footer>
```

Open `bloom.html` in Chrome. Unstyled content — ready for CSS.

---

### Step 3: Apply element selectors and a grouping selector

Element selectors target every instance of a tag — they establish global defaults. Add these rules:

```css
body {
  font-family: system-ui, sans-serif;
  background-color: #fdf8fa;
  color: #2c1a0e;
  margin: 0;             /* removes the browser's default 8px body gap */
}

h2 {
  font-size: 1.2rem;
  color: #7a1e3c;
}

p {
  line-height: 1.7;
  color: #5a4030;
}

/* Grouping selector: h1 and h2 share the same letter-spacing */
h1, h2 {
  letter-spacing: -0.3px;
}
```

Refresh. Every `<p>` and `<h2>` updates at once. The comma in `h1, h2` applies one rule to two selectors simultaneously. The `margin: 0` on `body` removes the narrow white gap that browsers add around the page edges by default.

---

### Step 4: Style the header with an ID selector

```css
#site-header {
  background-color: #7a1e3c;
  color: #fde8d5;
}

/* Descendant selector: only <p> tags inside #site-header */
#site-header p {
  color: #f4aac8;
  font-size: 1rem;
}
```

`#site-header p` is a **descendant selector** — it targets `<p>` tags inside `#site-header` only, leaving the product `<p>` tags unchanged.

`#site-header` uses an **ID selector** because only one element on the page is the site header. IDs are for unique, one-of-a-kind elements.

---

### Step 5: Style the nav with a pseudo-class

```css
nav {
  background-color: #a8294e;
}

/* Descendant selector: <a> inside <nav> only */
nav a {
  color: #fdd5e5;
  text-decoration: none;
  font-size: 0.9rem;
}

/* Pseudo-class: applies only when the mouse hovers */
nav a:hover {
  color: #ffffff;
  text-decoration: underline;
}
```

Hover over the navigation links. The `:hover` pseudo-class fires on interaction — no JavaScript needed.

---

### Step 6: Style product listings with a class selector

```css
.content {
  max-width: 860px;
}

/* Class selector: targets every element with class="product" */
.product {
  background-color: #ffffff;
  border-left: 4px solid #f0a8c0;
}

/* Descendant + class: <h3> inside any .product */
.product h3 {
  color: #7a1e3c;
  font-size: 1rem;
}

/* Pseudo-class on a class selector */
.product:hover {
  background-color: #fff5f8;
}
```

All four product entries now share the same style because all four carry `class="product"`.

---

### Step 7: Add the price and sale badge classes

```css
.price {
  font-weight: 700;
  color: #a8294e;
  font-size: 0.95rem;
}

.sale {
  background-color: #b5622a;
  color: white;
  font-size: 0.72rem;
  font-weight: 700;
}
```

---

### Step 8: Use an ID override to demonstrate specificity

The featured Monstera carries both `class="product"` and `id="featured"`. Add a rule targeting only `#featured`:

```css
/* ID specificity (0-1-0) beats class specificity (0-0-1)     */
/* so #featured wins the border-left conflict with .product   */
#featured {
  border-left-color: #b5622a;
  border-left-width: 6px;
}
```

`.product` sets `border-left: 4px solid #95d5b2`. The `#featured` rule overrides only the colour and width — the border style (`solid`) is inherited from `.product` because `#featured` does not set it.

Open Chrome DevTools (F12 → Elements → select the Monstera article → Styles panel). You will see `.product`'s `border-left-color` crossed out with a strikethrough, and `#featured`'s value winning. That crossed-out rule is the cascade in action.

---

### Step 9: Style the footer and ask AI to enhance

```css
footer {
  background-color: #7a1e3c;
  color: #f4aac8;
  padding: 1.5rem 2rem;
  margin-top: 3rem;
  font-size: 0.88rem;
}
```

Now paste your `bloom.html` into Gemini and prompt:

> *"Here is a plant shop homepage. Add styles inside the existing `<style>` block to: load a Google Font for the headings, add a subtle background image or gradient to the header, make each product card display its content side by side (product info on the left, price on the right), and add a smooth colour transition on the hover effect. Keep all existing CSS and HTML intact — only add new rules."*

Save the result as `bloom_styled.html` and compare.

---

## Checkpoints

* [ ] **Recipe Book Page**  
  Build an HTML page for a fictional recipe book with a `<style>` block. The page must include at least three recipe entries. Requirements:
  - An **element selector** that sets a consistent `font-family` and `line-height` on all `<p>` tags
  - A **class selector** (`.recipe-card`) styling every recipe entry with a `border`, `border-radius`, and background colour
  - An **ID selector** (`#chef-pick`) for one featured recipe — give it a distinct background and `border-color`
  - A **descendant selector** that styles `<h3>` tags inside `.recipe-card` differently from other `<h3>` tags on the page
  - At least one **pseudo-class** — a `:hover` effect on a link or button
  - A **grouping selector** used somewhere (e.g. `h2, h3 { ... }`)
  - No inline `style=""` attributes anywhere — all CSS in the `<style>` block

* [ ] **Event Listing Page**  
  Build a concert or event listing page for a fictional venue. Requirements:
  - A page header styled with an ID selector — dark background, light text
  - At least four event cards built with a shared class (`.event-card`) — same border, padding, and font
  - Each card has a date displayed in a `<span class="event-date">` — style this class with a distinct colour and font weight
  - One "sold out" event card: add a second class (`.sold-out`) to it and use CSS to grey out its text and add a visual indicator (e.g. `opacity: 0.5` or a strikethrough on the event title)
  - Demonstrate the **cascade**: write two conflicting rules for the same element (same specificity), and confirm in Chrome DevTools that the later one wins — DevTools shows overridden rules with a strikethrough
  - A navigation bar with `:hover` styling on the links
