# M15 Bootstrap Components

![Module 15 of 16](https://img.shields.io/badge/Module-15_of_16-6366f1?style=flat-square)
![Beginner](https://img.shields.io/badge/Difficulty-Beginner-4ade80?style=flat-square)
![2 hours](https://img.shields.io/badge/Time-2_hours-60a5fa?style=flat-square)
![Prerequisites: M01–M14](https://img.shields.io/badge/Prerequisites-M01–M14-94a3b8?style=flat-square)

**Topics covered:** Bootstrap navbar · card · button variants · badge · alert · form controls · modal · accordion · `data-bs-*` attributes · Bootstrap JS

---

## The Why?

Bootstrap's grid and utilities (M14) handle layout and spacing. But Bootstrap also ships a component library — pre-built, interactive UI patterns like navigation bars, modals, accordions, and form controls that require both CSS *and* JavaScript to work.

These components cover patterns you would otherwise need to implement from scratch: a menu that opens and closes, a dialog that overlays the page, a collapsible FAQ list. Each one is triggered by `data-bs-*` HTML attributes — no JavaScript code required from you.

Understanding Bootstrap components means you can build interactive interfaces rapidly. More importantly, you will be able to read the Bootstrap documentation and add any component the docs describe — a transferable skill for every Bootstrap-based project you encounter.

By the end of this module you will be able to:
- Add a responsive navbar that collapses on mobile
- Build interactive modals, accordions, and alerts triggered by HTML attributes
- Use Bootstrap form controls and validation states
- Read Bootstrap component documentation and implement any component independently

---

## Core Concepts

### `data-bs-*` Attributes

Bootstrap components are activated by HTML attributes — no JavaScript code required from you.

```html
<!-- A button that opens a modal with id="myModal" -->
<button data-bs-toggle="modal" data-bs-target="#myModal">Open modal</button>

<!-- A button that dismisses an alert -->
<button data-bs-dismiss="alert">×</button>

<!-- A button that toggles a collapse -->
<button data-bs-toggle="collapse" data-bs-target="#faq1">Question 1</button>
```

These attributes are read by `bootstrap.bundle.min.js`. Without the JS file included, interactive components will not work.

---

### Navbar

Bootstrap's navbar handles responsive collapsing automatically — the `data-bs-toggle="collapse"` attribute on the hamburger button does the work.

```html
<nav class="navbar navbar-expand-md navbar-dark bg-dark">
  <div class="container">
    <!-- Logo -->
    <a class="navbar-brand fw-bold" href="#">Brand</a>

    <!-- Hamburger button (visible on mobile) -->
    <button class="navbar-toggler" type="button"
      data-bs-toggle="collapse" data-bs-target="#mainNav">
      <span class="navbar-toggler-icon"></span>
    </button>

    <!-- Collapsible nav links -->
    <div class="collapse navbar-collapse" id="mainNav">
      <ul class="navbar-nav ms-auto">
        <li class="nav-item"><a class="nav-link" href="#">Home</a></li>
        <li class="nav-item"><a class="nav-link" href="#">Products</a></li>
        <li class="nav-item"><a class="nav-link active" href="#">About</a></li>
      </ul>
    </div>
  </div>
</nav>
```

- `navbar-expand-md` — expands to horizontal on medium+ screens; collapses on small
- `navbar-dark` — light text for dark backgrounds (use `navbar-light` for light backgrounds)
- `ms-auto` on `<ul>` — pushes nav links to the right

---

### Card

Bootstrap's `.card` component provides consistent layout for content blocks:

```html
<div class="card" style="max-width: 320px;">
  <img src="..." class="card-img-top" alt="...">
  <div class="card-body">
    <h5 class="card-title">Card title</h5>
    <p class="card-text">Some quick example text.</p>
    <a href="#" class="btn btn-primary">Go somewhere</a>
  </div>
  <div class="card-footer text-muted small">
    Last updated 3 mins ago
  </div>
</div>
```

Combine with the grid: `<div class="col-12 col-md-4"><div class="card h-100">...</div></div>` — `h-100` makes cards fill their grid column height.

---

### Buttons and Badges

```html
<!-- Button variants -->
<button class="btn btn-primary">Primary</button>
<button class="btn btn-outline-secondary">Secondary</button>
<button class="btn btn-danger btn-sm">Small danger</button>
<button class="btn btn-success btn-lg" disabled>Disabled</button>

<!-- Badges -->
<span class="badge bg-primary">New</span>
<span class="badge bg-danger rounded-pill">12</span>

<!-- Badge inside a button -->
<button class="btn btn-primary">
  Notifications <span class="badge bg-light text-dark ms-1">4</span>
</button>
```

---

### Alert

```html
<!-- Static alert -->
<div class="alert alert-success" role="alert">
  <strong>Success!</strong> Your changes have been saved.
</div>

<!-- Dismissible alert — requires Bootstrap JS -->
<div class="alert alert-warning alert-dismissible fade show" role="alert">
  Check your email to verify your account.
  <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
</div>
```

---

### Modal

```html
<!-- Trigger button -->
<button class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#confirmModal">
  Delete item
</button>

<!-- Modal markup — can be placed anywhere in <body> -->
<div class="modal fade" id="confirmModal" tabindex="-1">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title">Confirm deletion</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <p>Are you sure? This action cannot be undone.</p>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
        <button type="button" class="btn btn-danger">Delete</button>
      </div>
    </div>
  </div>
</div>
```

---

### Accordion

```html
<div class="accordion" id="faqAccordion">

  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button" type="button"
        data-bs-toggle="collapse" data-bs-target="#faq1"
        data-bs-parent="#faqAccordion">
        What is your return policy?
      </button>
    </h2>
    <div id="faq1" class="accordion-collapse collapse show">
      <div class="accordion-body">
        We accept returns within 30 days of purchase for any reason.
      </div>
    </div>
  </div>

  <div class="accordion-item">
    <h2 class="accordion-header">
      <button class="accordion-button collapsed" type="button"
        data-bs-toggle="collapse" data-bs-target="#faq2"
        data-bs-parent="#faqAccordion">
        How long does shipping take?
      </button>
    </h2>
    <div id="faq2" class="accordion-collapse collapse">
      <div class="accordion-body">
        Standard shipping takes 3–5 business days. Express is 1–2 days.
      </div>
    </div>
  </div>

</div>
```

`data-bs-parent="#faqAccordion"` — closing one item automatically closes others.

---

### Form Controls

```html
<form>
  <!-- Text input -->
  <div class="mb-3">
    <label for="email" class="form-label">Email address</label>
    <input type="email" class="form-control" id="email" placeholder="you@example.com">
  </div>

  <!-- Select -->
  <div class="mb-3">
    <label for="size" class="form-label">Size</label>
    <select class="form-select" id="size">
      <option value="">Choose a size</option>
      <option value="s">Small</option>
      <option value="m">Medium</option>
      <option value="l">Large</option>
    </select>
  </div>

  <!-- Checkbox -->
  <div class="form-check mb-3">
    <input class="form-check-input" type="checkbox" id="newsletter">
    <label class="form-check-label" for="newsletter">Subscribe to newsletter</label>
  </div>

  <button type="submit" class="btn btn-primary">Submit</button>
</form>
```

---

## Going Further

<details>
<summary>🎨 Customising Bootstrap component colours</summary>

Bootstrap's component colours are controlled by CSS custom properties. Override them after the Bootstrap CDN link:

```css
:root {
  --bs-primary: #4f46e5;        /* indigo instead of Bootstrap blue */
  --bs-primary-rgb: 79, 70, 229;
  --bs-btn-bg: var(--bs-primary);
  --bs-btn-border-color: var(--bs-primary);
}
```

For buttons specifically, you can also override individual component variables:

```css
.btn-primary {
  --bs-btn-bg: #4f46e5;
  --bs-btn-border-color: #4f46e5;
  --bs-btn-hover-bg: #4338ca;
}
```

</details>

<details>
<summary>📱 Navbar customisation patterns</summary>

**Sticky navbar:**
```html
<nav class="navbar navbar-expand-md navbar-dark bg-dark sticky-top">
```

**Transparent navbar over a hero:**
```html
<nav class="navbar navbar-expand-md navbar-dark position-absolute w-100" style="background-color: rgba(0,0,0,0.3);">
```

**Active link styling** — Bootstrap's `.active` class on `<a class="nav-link active">` applies visually distinct styling. Set it on the current page's link.

</details>

<details>
<summary>⌨️ Bootstrap and accessibility</summary>

Bootstrap components include ARIA attributes and keyboard navigation out of the box:
- Modals trap focus when open and restore it on close
- Accordion buttons have `aria-expanded` updated automatically
- `.btn-close` includes `aria-label="Close"` by default

What Bootstrap does *not* do automatically:
- Set `aria-current="page"` on active nav links — you must add this manually
- Announce dynamic content changes to screen readers — use `aria-live` regions for alerts and toasts

For most course exercises, Bootstrap's defaults are sufficient. In production, audit with a screen reader.

</details>

<details>
<summary>🤖 AI and Bootstrap components</summary>

Bootstrap components are well-represented in AI training data. Common issues:

- **Mixing BS4 and BS5 patterns** — BS4 uses `data-toggle` and `data-target`; BS5 uses `data-bs-toggle` and `data-bs-target`. AI frequently mixes these; always specify Bootstrap 5.
- **Missing IDs on collapse/modal targets** — the `data-bs-target` value must exactly match the target element's `id`. AI sometimes generates mismatched values.
- **Missing `modal-dialog` wrapper** — the modal structure requires `modal > modal-dialog > modal-content`. AI sometimes flattens this.

Useful AI prompts:
- *"Build a Bootstrap 5 modal confirmation dialog triggered by a delete button. The modal should have a title, body text, and two buttons: Cancel (dismisses) and Delete (btn-danger)."*
- *"Convert this static navbar to a Bootstrap 5 responsive navbar that collapses to a hamburger on screens narrower than 768px."*

</details>

---

## Guided Practice

**Scenario:** You are extending the **Summit** outdoor gear page from M14 with Bootstrap components — a responsive navbar, a product modal, an FAQ accordion, and an email sign-up form.

See `summit_components_example.html` in this folder for the finished result.

---

### Step 1: Create the file

In `M15BootstrapComponents`, create `summit_components.html`. Copy the Bootstrap CDN links and the base content structure from M14's `summit_example.html` as a starting point.

---

### Step 2: Add a responsive Bootstrap navbar

Replace any existing header with:

```html
<nav class="navbar navbar-expand-md navbar-dark bg-dark sticky-top">
  <div class="container">
    <a class="navbar-brand fw-bold" href="#">Summit</a>

    <button class="navbar-toggler" type="button"
      data-bs-toggle="collapse" data-bs-target="#summitNav"
      aria-controls="summitNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>

    <div class="collapse navbar-collapse" id="summitNav">
      <ul class="navbar-nav mx-auto">
        <li class="nav-item"><a class="nav-link active" href="#">Gear</a></li>
        <li class="nav-item"><a class="nav-link" href="#">Apparel</a></li>
        <li class="nav-item"><a class="nav-link" href="#">Footwear</a></li>
        <li class="nav-item"><a class="nav-link" href="#">Expeditions</a></li>
      </ul>
      <div class="d-flex gap-2">
        <a href="#" class="btn btn-outline-light btn-sm">Sign in</a>
        <a href="#" class="btn btn-success btn-sm">Shop</a>
      </div>
    </div>
  </div>
</nav>
```

Resize the browser below 768px and confirm the hamburger toggle appears and works.

---

### Step 3: Add a product modal

Inside the product card section, replace the "Ridgeline Shell" card's price with a "Quick view" button that opens a modal:

```html
<!-- Replace the price paragraph with: -->
<p class="fw-bold mt-2">$289</p>
<button class="btn btn-outline-dark btn-sm mt-2 w-100"
  data-bs-toggle="modal" data-bs-target="#ridgelineModal">
  Quick view
</button>
```

Add the modal just before `</body>` (before the Bootstrap JS script):

```html
<div class="modal fade" id="ridgelineModal" tabindex="-1">
  <div class="modal-dialog modal-lg">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title fw-bold">Ridgeline Shell</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
      </div>
      <div class="modal-body">
        <div class="row g-4">
          <div class="col-12 col-md-5">
            <div class="bg-secondary rounded-3" style="height: 250px;"></div>
          </div>
          <div class="col-12 col-md-7">
            <span class="badge bg-success mb-2">New arrival</span>
            <h4 class="fw-bold">Ridgeline Shell</h4>
            <p class="text-muted">3-layer waterproof jacket. Packable. 420g.</p>
            <ul class="small text-muted mb-3">
              <li>20,000mm waterproof rating</li>
              <li>Helmet-compatible hood</li>
              <li>Stuffs into chest pocket</li>
              <li>Recycled nylon face fabric</li>
            </ul>
            <p class="fs-4 fw-bold mb-3">$289</p>
            <div class="mb-3">
              <label class="form-label small fw-bold">Size</label>
              <select class="form-select form-select-sm">
                <option>XS</option><option>S</option><option selected>M</option>
                <option>L</option><option>XL</option>
              </select>
            </div>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-success">Add to cart</button>
      </div>
    </div>
  </div>
</div>
```

---

### Step 4: Add a dismissible alert

Add a promo announcement banner below the navbar:

```html
<div class="alert alert-warning alert-dismissible fade show mb-0 rounded-0 text-center" role="alert">
  🎒 <strong>Free shipping</strong> on orders over $150 — ends Sunday.
  <button type="button" class="btn-close" data-bs-dismiss="alert"></button>
</div>
```

---

### Step 5: Add an FAQ accordion

Add a new section below the product cards:

```html
<section class="py-5 bg-light">
  <div class="container" style="max-width: 760px;">
    <h2 class="fw-bold mb-4">Frequently asked questions</h2>

    <div class="accordion" id="faqAccordion">

      <div class="accordion-item border-0 mb-2 rounded-3 overflow-hidden">
        <h2 class="accordion-header">
          <button class="accordion-button fw-semibold" type="button"
            data-bs-toggle="collapse" data-bs-target="#faq1"
            data-bs-parent="#faqAccordion">
            What is your return policy?
          </button>
        </h2>
        <div id="faq1" class="accordion-collapse collapse show">
          <div class="accordion-body text-muted">
            We accept returns within 30 days of purchase for any reason. Items must be unused and in original packaging.
          </div>
        </div>
      </div>

      <div class="accordion-item border-0 mb-2 rounded-3 overflow-hidden">
        <h2 class="accordion-header">
          <button class="accordion-button collapsed fw-semibold" type="button"
            data-bs-toggle="collapse" data-bs-target="#faq2"
            data-bs-parent="#faqAccordion">
            How do I choose the right size?
          </button>
        </h2>
        <div id="faq2" class="accordion-collapse collapse">
          <div class="accordion-body text-muted">
            Each product page includes a detailed size guide with chest, waist, and hip measurements. For layering systems, we recommend sizing up one.
          </div>
        </div>
      </div>

      <div class="accordion-item border-0 mb-2 rounded-3 overflow-hidden">
        <h2 class="accordion-header">
          <button class="accordion-button collapsed fw-semibold" type="button"
            data-bs-toggle="collapse" data-bs-target="#faq3"
            data-bs-parent="#faqAccordion">
            Do you ship internationally?
          </button>
        </h2>
        <div id="faq3" class="accordion-collapse collapse">
          <div class="accordion-body text-muted">
            Yes — we ship to 62 countries. International orders typically arrive in 7–14 business days. Duties and taxes may apply at customs.
          </div>
        </div>
      </div>

    </div>
  </div>
</section>
```

---

### Step 6: Add a newsletter sign-up form

```html
<section class="py-5">
  <div class="container" style="max-width: 540px;">
    <h2 class="fw-bold mb-2">Stay in the loop</h2>
    <p class="text-muted mb-4">New gear drops, expedition stories, and exclusive offers — delivered to your inbox.</p>

    <form>
      <div class="mb-3">
        <label for="firstName" class="form-label">First name</label>
        <input type="text" class="form-control" id="firstName" placeholder="Your first name">
      </div>
      <div class="mb-3">
        <label for="signupEmail" class="form-label">Email address</label>
        <input type="email" class="form-control" id="signupEmail" placeholder="you@example.com">
        <div class="form-text">We never share your email. Unsubscribe any time.</div>
      </div>
      <div class="mb-3">
        <label class="form-label">Interests</label>
        <div class="form-check">
          <input class="form-check-input" type="checkbox" id="intClimbing">
          <label class="form-check-label" for="intClimbing">Climbing</label>
        </div>
        <div class="form-check">
          <input class="form-check-input" type="checkbox" id="intHiking" checked>
          <label class="form-check-label" for="intHiking">Hiking</label>
        </div>
        <div class="form-check">
          <input class="form-check-input" type="checkbox" id="intTrail">
          <label class="form-check-label" for="intTrail">Trail running</label>
        </div>
      </div>
      <button type="submit" class="btn btn-success w-100">Subscribe</button>
    </form>
  </div>
</section>
```

---

### Step 7: Test all interactive components

Open the page and verify:
- Navbar collapses on narrow screens and reopens with the hamburger button
- The promo alert dismisses when the × is clicked
- The "Quick view" button opens the product modal; the modal closes with Cancel or ×
- Accordion items open and close; opening one item closes the others

---

### Step 8: Inspect Bootstrap JS in DevTools

Open DevTools → Sources panel → look under the CDN domain for `bootstrap.bundle.min.js`. Open the Console and type `bootstrap.Modal.VERSION` — it should return the version string. This confirms Bootstrap JS is loaded and active.

---

### Step 9: Ask AI to enhance

Paste your `summit_components.html` into Gemini and prompt:

> *"Here is a Bootstrap 5 page with a navbar, modal, accordion, and form. Add: a Bootstrap toast notification that appears in the bottom-right corner when the 'Add to cart' button in the modal is clicked (use data-bs-toggle='toast'), a Bootstrap dropdown in the navbar for a 'Gear' menu with three sub-items, and a Bootstrap progress bar set to 75% inside a card labelled 'Expedition fund'. Keep all Bootstrap 5 conventions and existing code intact."*

Save as `summit_components_styled.html`.

---

## Checkpoints

* [ ] **E-commerce Product Page**  
  Build a product detail page using Bootstrap components. Requirements:
  - Sticky navbar with brand + links + cart button
  - Hero section: two-column (`col-12 col-md-6`) — image placeholder on left, product info on right
  - Product info includes: title, badge (e.g., "In stock"), price, a size `<select class="form-select">`, quantity `<input class="form-control" type="number">`, and two buttons (`btn-primary` + `btn-outline-*`)
  - A dismissible `alert alert-info` banner at the top of the page
  - A reviews accordion (3 items, each with a reviewer name and text) below the product section
  - Footer with brand name and copyright

* [ ] **Contact Page with Form Validation States**  
  Build a contact page. Requirements:
  - Bootstrap navbar at top
  - Contact form with: name (text), email, subject (select), message (textarea), submit button
  - Add `is-valid` class to the email field and `is-invalid` to the message field — observe Bootstrap's visual validation states and the `valid-feedback`/`invalid-feedback` helper text
  - A success alert (`alert-success`) below the form with `alert-dismissible`
  - A modal triggered by a "View our office locations" link — modal body contains a simple list of three locations
  - Footer
