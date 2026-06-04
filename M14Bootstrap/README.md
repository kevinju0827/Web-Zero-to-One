# M14 Bootstrap Basics

![Module 14 of 16](https://img.shields.io/badge/Module-14_of_16-6366f1?style=flat-square)
![Beginner](https://img.shields.io/badge/Difficulty-Beginner-4ade80?style=flat-square)
![2 hours](https://img.shields.io/badge/Time-2_hours-60a5fa?style=flat-square)
![Prerequisites: M06 + M10](https://img.shields.io/badge/Prerequisites-M06_+_M10-94a3b8?style=flat-square)

**Topics covered:** external stylesheets (`<link>`) · what Bootstrap is · the Bootstrap CDN · a tour of Bootstrap · component classes (button, badge, card, navbar, carousel, toast) · utility classes (colour, spacing, typography, display) · `.container` and a first look at columns

---

## The Why?

For nine modules you have written CSS by hand — every colour, every bit of spacing, every button. It works, but it is slow, and most of what you write is the same patterns every project needs: a styled button, a card, a navigation bar, even spacing.

**Bootstrap is one enormous, professionally-written CSS file.** Someone has already written the rules for all those common patterns and given each one a class name. You link their file the same way you would link your own stylesheet, then style elements by *adding class names* instead of writing CSS.

That is the whole idea. Bootstrap does not replace what you learned — it is built on the exact Flexbox, spacing, and colour concepts from earlier modules. It just packages them so you can build a polished, consistent page in minutes. Bootstrap is also the most widely used CSS framework in the world, so reading it is a skill you will reuse on real projects everywhere.

By the end of this module you will be able to:
- Move your CSS into a separate file and load it with `<link>`
- Explain what Bootstrap is and add it to any page via the CDN
- Use class names to turn plain HTML into styled buttons, cards, and navbars
- Apply utility classes for colour, spacing, and typography
- Find any other component or utility in the Bootstrap documentation yourself

---

## Core Concepts

### From Your Own Stylesheet to Bootstrap's

So far your CSS has lived in a `<style>` block inside `<head>`. CSS can also live in its **own file** and be loaded with a `<link>` tag. Move your rules into `styles.css`:

```css
/* styles.css */
.btn {
  background-color: #2a5a3a;
  color: white;
  padding: 0.75rem 1.5rem;
  border-radius: 0.5rem;
}
```

…then load that file from your HTML:

```html
<head>
  <link rel="stylesheet" href="styles.css">
</head>
```

Now any element with `class="btn"` is styled by the rule in `styles.css`. The HTML and the CSS are separate files joined by one `<link>`.

**Bootstrap is exactly this — at scale.** Instead of *your* small `styles.css`, you link Bootstrap's huge pre-written stylesheet. It already contains thousands of class rules like `.btn`, `.card`, and `.navbar`. You did not write them, but the moment you link the file you can use them.

You do not even download the file. You link it straight from a **CDN** (Content Delivery Network — a fast public server that hosts popular files). Paste these two tags, copied from the [official Bootstrap quick-start](https://getbootstrap.com/docs/5.3/getting-started/introduction/):

```html
<head>
  <!-- Bootstrap CSS — gives you every Bootstrap class -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB" crossorigin="anonymous">
</head>
<body>
  <!-- your content -->

  <!-- Bootstrap JS — powers interactive components (navbar toggle, carousel, toast) -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js" integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI" crossorigin="anonymous"></script>
</body>
```

- The `<link>` goes in `<head>` — it loads the CSS (the part you use in this module).
- The `<script>` goes just before `</body>` — it loads the JavaScript that makes a few components interactive. Include it now so everything works.
- `integrity` and `crossorigin` let the browser verify the file downloaded from the CDN was not tampered with. Copy them as-is.

No installation, no npm, no build step.

---

### A Tour of Bootstrap

Before using any one feature, it helps to know the *shape* of what Bootstrap offers. The [documentation](https://getbootstrap.com/docs/5.3/) is organised into a handful of areas:

| Area | What it gives you | Example |
|------|-------------------|---------|
| **Reboot** | Sensible global defaults applied automatically | `box-sizing: border-box` on everything, reset margins |
| **Content** | Base styling for text, tables, images | `.table`, `.img-fluid` |
| **Components** | Pre-built UI blocks | `.btn`, `.card`, `.navbar`, `.carousel` |
| **Forms** | Styled inputs and form layouts | `.form-control`, `.form-select` |
| **Layout** | The responsive grid system | `.container`, `.row`, `.col` |
| **Utilities** | Tiny single-purpose classes | `.text-center`, `.mt-3`, `.bg-primary` |
| **Helpers** | Small layout aids | `.ratio`, `.stretched-link` |

You will not memorise all of it — nobody does. The skill is knowing these areas exist so you can look up the right page. **Reboot** is free and automatic: just by linking Bootstrap, every element gets `box-sizing: border-box`, headings and paragraphs lose their default margins, and images behave sensibly. Many resets you wrote by hand in earlier modules are already done.

The rest of this module covers the quickest wins first: **component classes** (the most visible change), then **utilities** (small tweaks), then a first look at **layout**. The full grid system and customisation come in M15.

---

### Component Classes — Plain Tags Become UI

A **component** is a pre-built UI block you activate by adding class names. Start with the simplest one.

**Buttons** — take a plain `<button>` and add two classes:

```html
<button class="btn btn-primary">Primary</button>
<button class="btn btn-success">Success</button>
<button class="btn btn-outline-danger">Outline</button>
<button class="btn btn-primary btn-lg">Large</button>
<button class="btn btn-secondary btn-sm">Small</button>
```

`.btn` is the base; `.btn-primary`, `.btn-success`, etc. set the colour; `.btn-lg`/`.btn-sm` set the size. You *could* style a button like this yourself (you did in M08) — Bootstrap just makes it one attribute.

**Badges** — small labels, equally easy:

```html
<span class="badge bg-primary">New</span>
<span class="badge bg-danger rounded-pill">12</span>
```

Buttons and badges are quick wins. But the real value of a component library shows up when a component would take you *a lot* of HTML, CSS, and JavaScript to build by hand. Here are four — shown at basic-usage level. You do not need to memorise the markup; copy it from the docs and adjust.

**Card** — a self-contained content block with an image, body, and footer:

```html
<div class="card" style="width: 18rem;">
  <img src="https://images.unsplash.com/photo-1551632811-561732d1e306?w=600&h=400&fit=crop" class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Ridgeline Shell</h5>
    <p class="card-text">3-layer waterproof jacket. Packable. 420g.</p>
    <a href="#" class="btn btn-primary">Buy</a>
  </div>
</div>
```

**Navbar** — a responsive navigation bar. On narrow screens it can collapse into a hamburger menu (that part uses the JS bundle):

```html
<nav class="navbar navbar-expand-md navbar-dark bg-dark">
  <div class="container">
    <a class="navbar-brand" href="#">Summit</a>
    <ul class="navbar-nav flex-row gap-3">
      <li class="nav-item"><a class="nav-link active" href="#">Gear</a></li>
      <li class="nav-item"><a class="nav-link" href="#">Apparel</a></li>
    </ul>
  </div>
</nav>
```

**Carousel** — an image slideshow that auto-rotates and responds to arrow buttons, all from the JS bundle:

```html
<div id="demo" class="carousel slide" data-bs-ride="carousel">
  <div class="carousel-inner">
    <div class="carousel-item active"><img src="https://images.unsplash.com/photo-1454496522488-7a8e488e8606?w=1200&h=500&fit=crop" class="d-block w-100" alt="..."></div>
    <div class="carousel-item"><img src="https://images.unsplash.com/photo-1488646953014-85cb44e25828?w=1200&h=500&fit=crop" class="d-block w-100" alt="..."></div>
  </div>
  <button class="carousel-control-prev" data-bs-target="#demo" data-bs-slide="prev">
    <span class="carousel-control-prev-icon"></span>
  </button>
  <button class="carousel-control-next" data-bs-target="#demo" data-bs-slide="next">
    <span class="carousel-control-next-icon"></span>
  </button>
</div>
```

**Toast** — a small pop-up notification:

```html
<div class="toast show">
  <div class="toast-header">
    <strong class="me-auto">Summit</strong>
    <button type="button" class="btn-close" data-bs-dismiss="toast"></button>
  </div>
  <div class="toast-body">Added to your cart.</div>
</div>
```

Imagine writing the carousel from scratch: the HTML structure, the CSS for sliding transitions, and the JavaScript for the timer and arrow buttons. Bootstrap hands you all of it for the price of some class names and `data-bs-*` attributes. The [Components page](https://getbootstrap.com/docs/5.3/components/) lists dozens more — accordion, modal, dropdown, spinner, tooltip — and you now know how to read it.

---

### Utility Classes — Small, Single-Purpose Tweaks

Where a component is a whole UI block, a **utility** does one tiny thing. They are how you fine-tune spacing, colour, and text without writing CSS.

**Colour** — backgrounds and text:

```html
<div class="bg-primary text-white">Blue box, white text</div>
<div class="bg-light">Light grey box</div>
<p class="text-success">Green text</p>
<p class="text-muted">Muted grey text</p>
```

Colour names are *semantic*: `primary`, `secondary`, `success`, `danger`, `warning`, `info`, `light`, `dark`.

**Spacing** — margin (`m`) and padding (`p`) on a 0–5 scale:

```
{property}{side}-{size}      e.g. mt-3, px-4, mb-0, py-2
```

| Class | Means |
|-------|-------|
| `mt-3` | `margin-top: 1rem` |
| `mb-0` | `margin-bottom: 0` |
| `px-4` | padding left + right `1.5rem` |
| `py-2` | padding top + bottom `0.5rem` |
| `mx-auto` | centre horizontally |

Sides: `t` top, `b` bottom, `s` start (left), `e` end (right), `x` left+right, `y` top+bottom, or blank for all sides.

**Typography:**

```html
<h1 class="display-4 fw-bold">Big bold heading</h1>
<p class="lead">Larger introductory paragraph</p>
<p class="text-center text-uppercase">Centred uppercase text</p>
```

**Display & Flexbox** — the same Flexbox you learned in M10, as utilities:

```html
<div class="d-flex justify-content-between align-items-center">
  <span>Left</span>
  <span>Right</span>
</div>

<div class="d-none">Hidden</div>
```

`d-flex` is `display: flex`; `justify-content-between` and `align-items-center` are the M10 properties you already know — just spelled as classes.

---

### `.container` and a First Look at Columns

One layout class you need right away: **`.container`** centres your content and keeps it from stretching too wide on big screens.

```html
<div class="container">
  <!-- centred, with comfortable max-width and side padding -->
</div>
```

Inside a container, Bootstrap lays content out on a **12-column grid**. A `.row` is a flex row; `.col-*` children divide the 12 columns between them:

```html
<div class="container">
  <div class="row">
    <div class="col-4">One third</div>
    <div class="col-4">One third</div>
    <div class="col-4">One third</div>
  </div>
</div>
```

The column numbers add up to 12. Add a breakpoint — `col-md-6` — and the layout changes by screen size. That is enough to build this module's practice page. **The full grid system — gutters, breakpoints, alignment, offsets, nesting — is the focus of M15.**

---

## Going Further

<details>
<summary>📦 Reboot — what Bootstrap sets globally</summary>

Just by linking Bootstrap's CSS, its **Reboot** layer normalises the browser's defaults so every project starts from the same baseline:

- `box-sizing: border-box` on all elements (the M08 rule, applied for you)
- Margins removed from headings, paragraphs, and lists
- `font-family`, base `font-size`, and `line-height: 1.5` set on `<body>`
- Images set to `display: block` and easy to make responsive

So several resets you wrote manually in earlier modules are already included the moment you add Bootstrap.

</details>

<details>
<summary>🎯 When to use a utility vs write your own class</summary>

**Use a Bootstrap utility** for common, one-off tweaks: spacing, colour, text alignment (`mt-3`, `text-center`, `bg-light`).

**Write your own class** when you need something Bootstrap does not provide, or a brand-specific style you will reuse (a custom hero gradient, an exact font size).

**Avoid inline `style=""`** except for genuine one-offs (like a fixed placeholder height) — it has the highest specificity and is hard to maintain.

Your own `<style>` block or stylesheet, loaded *after* Bootstrap's `<link>`, always wins on ties — that is how you override Bootstrap (covered in depth in M15).

</details>

<details>
<summary>🤖 AI and Bootstrap</summary>

Bootstrap is well-represented in AI training data, making it one of the more reliable areas for generation. Watch for:

- **Bootstrap 4 vs 5 class names** — BS4 used `ml-`/`mr-` for margins; BS5 uses `ms-`/`me-` (start/end). Always specify Bootstrap 5.
- **Outdated CDN links** — check the docs for the current version; this course uses 5.3.8.
- **Custom CSS for things a utility already does** — AI often writes custom padding when `py-4` would do. Review for redundancy.

Useful prompts:
- *"Style this button using Bootstrap 5 classes only — no custom CSS."*
- *"Turn this plain navigation `<ul>` into a Bootstrap 5 navbar component."*

</details>

---

## Guided Practice

**Scenario:** You are building the landing page for **Summit** — an outdoor gear brand: a navbar, a hero, a feature row, a product-card grid, a stats bar, and a footer.

**First, open `summit_plain_example.html` in this folder and read it.** It is this exact page built the old way — plain HTML with a hand-written `<style>` block of roughly 190 lines. Notice how much CSS the navbar, buttons, badges, and cards take.

Now you will rebuild the same page with Bootstrap, writing almost no CSS of your own. The finished result is `summit_example.html`.

---

### Step 1: Create the file and link Bootstrap

In `M14Bootstrap`, create `summit.html`. Title it `Summit — Outdoor Gear`. Add the Bootstrap CSS `<link>` in `<head>` and the Bootstrap JS `<script>` just before `</body>` (copy both from the *From Your Own Stylesheet to Bootstrap's* section).

---

### Step 2: Add the navbar

The component that took the most CSS in the plain file is one class list here:

```html
<nav class="navbar navbar-expand-md navbar-dark bg-dark">
  <div class="container">
    <a class="navbar-brand fw-bold" href="#">Summit</a>
    <ul class="navbar-nav flex-row gap-3">
      <li class="nav-item"><a class="nav-link active" aria-current="page" href="#">Gear</a></li>
      <li class="nav-item"><a class="nav-link" href="#">Apparel</a></li>
      <li class="nav-item"><a class="nav-link" href="#">Footwear</a></li>
      <li class="nav-item"><a class="nav-link" href="#">Expeditions</a></li>
    </ul>
  </div>
</nav>
```

---

### Step 3: Add the hero with a container, columns, and utilities

```html
<section class="bg-dark text-white py-5">
  <div class="container py-4">
    <div class="row align-items-center">
      <div class="col-12 col-md-7">
        <p class="text-uppercase fw-bold mb-2" style="color: #6eaa70; font-size: 0.75rem; letter-spacing: 0.15em;">
          Gear built for real terrain
        </p>
        <h1 class="display-4 fw-bold mb-3">Climb higher.<br>Go further.</h1>
        <p class="lead text-white-50 mb-4">
          Equipment for mountaineers, trail runners, and everyone who treats the outdoors as a destination, not a backdrop.
        </p>
        <div class="d-flex gap-3 flex-wrap">
          <a href="#" class="btn btn-success btn-lg px-4">Shop gear</a>
          <a href="#" class="btn btn-outline-light btn-lg px-4">Our story</a>
        </div>
      </div>
      <div class="col-12 col-md-5 mt-4 mt-md-0">
        <img src="https://images.unsplash.com/photo-1551632811-561732d1e306?w=800&h=560&fit=crop" class="rounded-3 w-100" style="height:280px; object-fit:cover;" alt="Hiker ascending a rocky mountain ridge at golden hour">
      </div>
    </div>
  </div>
</section>
```

Every space, colour, and column here is a utility or layout class — no custom CSS.

---

### Step 4: Add the feature highlights row

```html
<section class="py-5 bg-light">
  <div class="container">
    <div class="row g-4 text-center">
      <div class="col-12 col-md-4">
        <div class="p-4">
          <div class="fs-1 mb-3">🏔️</div>
          <h3 class="fw-bold mb-2">Built for altitude</h3>
          <p class="text-muted">Tested above 4,000m. Every seam, buckle, and layer engineered for cold and wind.</p>
        </div>
      </div>
      <div class="col-12 col-md-4">
        <div class="p-4">
          <div class="fs-1 mb-3">⚖️</div>
          <h3 class="fw-bold mb-2">Gram-conscious design</h3>
          <p class="text-muted">We obsess over weight so you carry less without losing capability.</p>
        </div>
      </div>
      <div class="col-12 col-md-4">
        <div class="p-4">
          <div class="fs-1 mb-3">♻️</div>
          <h3 class="fw-bold mb-2">Sustainable materials</h3>
          <p class="text-muted">Recycled fabrics, bluesign-certified dyes, and a repair-not-replace warranty.</p>
        </div>
      </div>
    </div>
  </div>
</section>
```

---

### Step 5: Add a product card grid

This is the `.card` component sitting in grid columns — four across on desktop, two on tablet, one on mobile:

```html
<section class="py-5">
  <div class="container">
    <h2 class="fw-bold mb-4">New arrivals</h2>
    <div class="row g-4">

      <div class="col-12 col-sm-6 col-lg-3">
        <div class="card h-100 border-0 shadow-sm">
          <div class="bg-secondary" style="height: 180px;"></div>
          <div class="card-body">
            <span class="badge bg-success mb-2">New</span>
            <h5 class="card-title fw-bold">Ridgeline Shell</h5>
            <p class="card-text text-muted small">3-layer waterproof jacket. Packable. 420g.</p>
            <p class="fw-bold mt-2">$289</p>
          </div>
        </div>
      </div>

      <div class="col-12 col-sm-6 col-lg-3">
        <div class="card h-100 border-0 shadow-sm">
          <div class="bg-secondary" style="height: 180px;"></div>
          <div class="card-body">
            <span class="badge bg-warning text-dark mb-2">Sale</span>
            <h5 class="card-title fw-bold">Summit 28L Pack</h5>
            <p class="card-text text-muted small">Daypack with hydration sleeve and helmet carry.</p>
            <p class="fw-bold mt-2">$149 <small class="text-muted text-decoration-line-through">$189</small></p>
          </div>
        </div>
      </div>

      <div class="col-12 col-sm-6 col-lg-3">
        <div class="card h-100 border-0 shadow-sm">
          <div class="bg-secondary" style="height: 180px;"></div>
          <div class="card-body">
            <h5 class="card-title fw-bold">Alpenglow Beanie</h5>
            <p class="card-text text-muted small">Merino wool, mid-weight. One size.</p>
            <p class="fw-bold mt-2">$55</p>
          </div>
        </div>
      </div>

      <div class="col-12 col-sm-6 col-lg-3">
        <div class="card h-100 border-0 shadow-sm">
          <div class="bg-secondary" style="height: 180px;"></div>
          <div class="card-body">
            <span class="badge bg-danger mb-2">Low stock</span>
            <h5 class="card-title fw-bold">Trailblazer Trekking Poles</h5>
            <p class="card-text text-muted small">Carbon fibre, foldable, 170g each.</p>
            <p class="fw-bold mt-2">$195</p>
          </div>
        </div>
      </div>

    </div>
  </div>
</section>
```

---

### Step 6: Add a stats bar and footer

```html
<section class="bg-dark text-white py-4">
  <div class="container">
    <div class="row text-center g-4">
      <div class="col-6 col-md-3">
        <p class="display-5 fw-bold mb-0">14</p>
        <p class="text-white-50 small">Years in the field</p>
      </div>
      <div class="col-6 col-md-3">
        <p class="display-5 fw-bold mb-0">38k</p>
        <p class="text-white-50 small">Expeditions equipped</p>
      </div>
      <div class="col-6 col-md-3">
        <p class="display-5 fw-bold mb-0">62</p>
        <p class="text-white-50 small">Countries reached</p>
      </div>
      <div class="col-6 col-md-3">
        <p class="display-5 fw-bold mb-0">100%</p>
        <p class="text-white-50 small">Recycled packaging</p>
      </div>
    </div>
  </div>
</section>

<footer class="bg-dark text-white-50 py-4">
  <div class="container">
    <div class="row">
      <div class="col-12 col-md-6">
        <p class="fw-bold text-white mb-1">Summit</p>
        <p class="small">Outdoor gear built for serious terrain.</p>
      </div>
      <div class="col-12 col-md-6 text-md-end mt-3 mt-md-0">
        <p class="small">&copy; 2026 Summit Outdoor Co. · <a href="#" class="text-white-50">Privacy</a></p>
      </div>
    </div>
  </div>
</footer>
```

---

### Step 7: Compare the two files

Open `summit.html` and `summit_plain_example.html` side by side. They render almost identically — but the plain version needed ~190 lines of CSS, while yours has essentially none. Scroll the plain file's `<style>` block and find, for each rule, the Bootstrap class that replaced it (`.btn`, `.card`, `.navbar`, `.bg-dark`, `.py-5`, …). That mapping *is* Bootstrap.

---

## Checkpoints

* [ ] **Component Sampler**
  Build a single HTML file (Bootstrap linked) with one `<section>` for each component, each labelled with a heading:
  - A row of buttons: at least three colour variants, one outline, one `btn-lg`, one `btn-sm`
  - Three badges, including one `rounded-pill`
  - Two cards side by side using `col-md-6`, each with an image area, title, text, and a button
  - A navbar at the top with a brand and three links
  - No custom CSS for any of these — Bootstrap classes only

* [ ] **Utility Rebuild**
  Take any plain HTML page you wrote in an earlier module (or the provided `summit_plain_example.html`) and rebuild one section using only Bootstrap:
  - Replace hand-written spacing with `m-*` / `p-*` utilities
  - Replace hand-written colours with `bg-*` / `text-*` utilities
  - Wrap the content in a `.container`
  - List, in an HTML comment at the top, every Bootstrap class you used and the custom CSS rule it replaced
