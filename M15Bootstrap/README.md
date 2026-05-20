# M15 Bootstrap

## The "Why?"

By now, you have hand-built everything: typography, the box model, Flexbox, CSS Grid, and responsive layouts. You know how to write CSS from scratch. But in the professional world, **time is money**. Writing 80 lines of CSS for a navbar—on every project—gets old very quickly.

**Bootstrap** is a "batteries-included" frontend framework. It bundles a polished set of CSS components (buttons, navbars, cards, modals, alerts) and a powerful responsive grid system into a single file you can drop into any project. Instead of writing custom styles for a button, you just add `class="btn btn-primary"`. Instead of writing media queries for a 3-column layout, you just write `class="col-md-4"`.

Bootstrap is the most widely-used frontend framework on the planet. Knowing it means you can ship a professional-looking site in hours instead of days, and you can read and modify almost any existing codebase you'll encounter on the job.

## Goals

Learn how to integrate Bootstrap into a project and use its grid system, components, and utility classes to build a responsive page quickly.  
By the end of this module, you should be able to include Bootstrap via CDN, build layouts using the Bootstrap 12-column grid (`.container`, `.row`, `.col-*`), drop in pre-built components like `.navbar`, `.card`, and `.btn`, and fine-tune spacing, color, and alignment using utility classes like `m-3`, `p-5`, `text-center`, and `bg-light`.

## Core Concepts

### 1. Including Bootstrap (the CDN approach)

The fastest way to start is by adding **two lines** to your HTML—one in the `<head>` for CSS, and one near the end of `<body>` for the JavaScript bundle (which powers interactive components like dropdowns and modals).

```html
<!-- In <head> -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">

<!-- At the end of <body> -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```

A **CDN** (Content Delivery Network) is a global network of servers that hosts files like Bootstrap's CSS. Your browser downloads the file from the nearest server, which is fast and reliable, and you don't have to host anything yourself.

### 2. The Bootstrap Grid

Bootstrap's grid is a Flexbox-based, **12-column** system. You always nest the same three layers:

* **`.container`** — a centered wrapper with sensible max-widths and padding.
* **`.row`** — a horizontal wrapper that contains columns.
* **`.col-*`** — a column that takes up some number of the 12 available slots.

```html
<div class="container">
  <div class="row">
    <div class="col-6">Left half</div>
    <div class="col-6">Right half</div>
  </div>
</div>
```

### 3. Responsive Column Classes

The real power of the grid is the **responsive suffixes**: `sm`, `md`, `lg`, `xl`, `xxl`. They map to standard breakpoints and tell Bootstrap "use this width *from this screen size and up*."

| Class           | Active when…                          |
|-----------------|---------------------------------------|
| `.col-12`       | Always (mobile and up)                |
| `.col-md-6`     | On medium screens (≥ 768px) and up    |
| `.col-lg-4`     | On large screens (≥ 992px) and up     |

A common pattern combines them: `class="col-12 col-md-6 col-lg-4"` means "full width on phones, half-width on tablets, one-third width on desktops." That's a fully responsive 3-column layout in a single line.

### 4. Components

Bootstrap ships with dozens of pre-styled, ready-to-paste components. The ones you'll use most often:

* **`.navbar`** — top navigation bars (with a built-in mobile hamburger menu).
* **`.btn`** + color variants (`.btn-primary`, `.btn-outline-secondary`, etc.) — buttons.
* **`.card`** — content cards with image, title, body, and footer slots.
* **`.alert`** — colored notification banners.
* **`.modal`** — pop-up dialogs.
* **`.carousel`** — image sliders.

Don't memorize them. Just go to the [Bootstrap documentation](https://getbootstrap.com/docs/5.3/components/), copy the HTML snippet for the component you need, and adapt it.

### 5. Utility Classes

This is where Bootstrap really speeds things up. Utility classes are tiny, single-purpose helpers you apply directly to any element to control spacing, color, alignment, sizing, and more.

| Category    | Examples                                                |
|-------------|---------------------------------------------------------|
| Spacing     | `m-3` (margin), `p-5` (padding), `mt-2` (margin-top), `mx-auto` (horizontal auto-margin) |
| Text        | `text-center`, `text-primary`, `text-muted`, `fw-bold`  |
| Background  | `bg-light`, `bg-dark`, `bg-primary`                     |
| Display     | `d-flex`, `d-none`, `d-md-block`                        |
| Borders     | `border`, `border-0`, `rounded`, `rounded-pill`         |
| Sizing      | `w-100`, `h-100`, `mw-100`                              |

The spacing scale (`-0` through `-5`) is consistent across every utility, which makes vertical rhythm easy to maintain.

## Guided Practice

In this practice, we will build the landing page for a fictional tech conference called **"DevConf '26"**. A conference page is a perfect Bootstrap showcase because every major component lives on a single page: a navbar with a CTA, a colorful hero, a responsive speaker grid, a schedule list, ticket pricing tiers, sponsor logos, an FAQ accordion, and a multi-column footer. See `tech_conference.html` in this folder for the finished result. (Once you're done, also study `star_enjoy_coffee_example.html` — a polished e-commerce-style landing page built with the same primitives.)

* Step 1: Include Bootstrap and Bootstrap Icons

  Every Bootstrap site starts the same way: one `<link>` in the `<head>`, one `<script>` near the end of `<body>`. We'll also include the optional Bootstrap Icons font for the checkmarks in our pricing table.
  * Create an HTML file. Inside `<head>`, add:
  ```html
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css">
  ```
  * Just before `</body>`, add:
  ```html
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
  ```
  * **Observation:** Even with an empty `<body>`, your fonts and link colors now look cleaner. That's Bootstrap's `normalize.css` and base typography kicking in for free.

* Step 2: Build a Sticky Navbar with a CTA Button

  Every modern conference page pins its navigation to the top with a bright "Get Tickets" call to action. Bootstrap's `.navbar` component, plus a couple of utility classes, gives us all of this — including the mobile hamburger menu — without writing a single media query.
  * Add the following HTML at the top of `<body>`:
  ```html
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top">
    <div class="container">
      <a class="navbar-brand fw-bold" href="#">⚡ DevConf '26</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navMenu">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navMenu">
        <ul class="navbar-nav ms-auto align-items-lg-center">
          <li class="nav-item"><a class="nav-link" href="#speakers">Speakers</a></li>
          <li class="nav-item"><a class="nav-link" href="#schedule">Schedule</a></li>
          <li class="nav-item"><a class="nav-link" href="#tickets">Tickets</a></li>
          <li class="nav-item ms-lg-3 mt-2 mt-lg-0">
            <a class="btn btn-warning" href="#tickets">Get Tickets →</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  ```
  * **Observation:** Resize the browser narrower than ~992px. The links collapse into a hamburger menu. Click it — Bootstrap's JS bundle handles the entire expand/collapse animation automatically. Notice the **responsive utility** `ms-lg-3 mt-2 mt-lg-0` on the CTA: on mobile, the button gets top margin; on desktop, it gets left margin. One element, two layouts.

* Step 3: Build a Colorful Hero with Stats

  Conference heroes need to do three things at once: announce the date, sell the vibe, and give attendees their first CTA. Use Bootstrap's `display-3`/`lead`/`btn-lg` typography classes and the `.row` / `.col-*` grid for the stats row.
  * Add the following HTML below the navbar:
  ```html
  <header class="bg-dark text-white py-5" style="padding-top: 8rem !important;">
    <div class="container text-center py-5">
      <span class="badge bg-warning text-dark px-3 py-2 mb-3 rounded-pill">
        March 15–17, 2026 · San Francisco
      </span>
      <h1 class="display-3 fw-bold mb-3">The conference for<br>people who actually ship.</h1>
      <p class="lead opacity-75 mx-auto" style="max-width:640px;">
        Three days of talks, workshops, and unstructured hallway conversations
        with the engineers building the next decade of the web.
      </p>
      <div class="mt-4 d-flex gap-2 justify-content-center flex-wrap">
        <a href="#tickets" class="btn btn-warning btn-lg px-4">Get Tickets</a>
        <a href="#schedule" class="btn btn-outline-light btn-lg px-4">See the Schedule</a>
      </div>

      <!-- Stats row -->
      <div class="row g-3 mt-5">
        <div class="col-6 col-md-3">
          <div class="display-5 fw-bold text-warning">42</div>
          <div class="small text-uppercase opacity-75">Speakers</div>
        </div>
        <div class="col-6 col-md-3">
          <div class="display-5 fw-bold text-warning">3</div>
          <div class="small text-uppercase opacity-75">Tracks</div>
        </div>
        <div class="col-6 col-md-3">
          <div class="display-5 fw-bold text-warning">1,800</div>
          <div class="small text-uppercase opacity-75">Attendees</div>
        </div>
        <div class="col-6 col-md-3">
          <div class="display-5 fw-bold text-warning">19</div>
          <div class="small text-uppercase opacity-75">Countries</div>
        </div>
      </div>
    </div>
  </header>
  ```
  * **Observation:** The stats row uses `col-6 col-md-3` — 2 stats per row on mobile, 4 across on tablets and up. The single buttons row uses `d-flex gap-2 justify-content-center flex-wrap` — that's a *Flexbox container expressed entirely as Bootstrap utility classes*. Every layout decision you previously made in Modules 12–14 is also possible directly in HTML attributes.

* Step 4: Build the Speakers Grid (Responsive Cards)

  Use Bootstrap's grid to display speaker bios that automatically reflow: 1 column on phones, 2 on small tablets, 4 on desktops.
  * Add the following HTML below the hero:
  ```html
  <section id="speakers" class="container py-5">
    <div class="d-flex justify-content-between align-items-baseline mb-4">
      <h2 class="mb-0">Featured Speakers</h2>
      <a href="#" class="text-decoration-none">See all 42 →</a>
    </div>
    <div class="row g-4">
      <div class="col-12 col-sm-6 col-lg-3 text-center">
        <img src="https://images.unsplash.com/photo-1494790108377-be9c29b29330?w=300"
             class="rounded-circle mb-3" style="width:120px; height:120px; object-fit:cover;" alt="">
        <h5>Amara Patel</h5>
        <p class="text-muted small mb-2">Principal Engineer, Stripe</p>
        <p class="small">"Designing APIs that survive 10 years"</p>
      </div>
      <!-- repeat for 3 more speakers, change image URL, name, role, and talk title -->
    </div>
  </section>
  ```
  * **Observation:** Notice the responsive ladder `col-12 col-sm-6 col-lg-3`. On a phone, each speaker takes the full row. On a small tablet, two fit side-by-side. On a desktop, all four line up across the row. This *single line* of class names replaces what would have been three media queries.

* Step 5: Build a Ticket Pricing Table with a Featured Tier

  Three pricing tiers laid out in Bootstrap cards. The middle tier gets a yellow border and a "EARLY BIRD" badge to draw the eye.
  * Add the following HTML:
  ```html
  <section id="tickets" class="container py-5">
    <div class="text-center mb-5">
      <h2 class="mb-2">Tickets</h2>
      <p class="text-muted">Early-bird pricing ends January 31, 2026.</p>
    </div>
    <div class="row g-4 justify-content-center">

      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100 text-center">
          <div class="card-body p-4">
            <h5 class="text-uppercase text-muted">Student</h5>
            <div class="display-5 fw-bold my-3">$149</div>
            <ul class="list-unstyled text-start mb-4">
              <li class="mb-2"><i class="bi bi-check2 text-success me-2"></i>All 3 days</li>
              <li class="mb-2"><i class="bi bi-check2 text-success me-2"></i>Student lounge</li>
            </ul>
            <button class="btn btn-outline-dark w-100">Buy ticket</button>
          </div>
        </div>
      </div>

      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100 text-center border-warning border-2">
          <div class="card-body p-4">
            <span class="badge bg-warning text-dark mb-2 rounded-pill">EARLY BIRD</span>
            <h5 class="text-uppercase text-muted">Standard</h5>
            <div class="display-5 fw-bold my-3">$549</div>
            <ul class="list-unstyled text-start mb-4">
              <li class="mb-2"><i class="bi bi-check2 text-success me-2"></i>All 3 days</li>
              <li class="mb-2"><i class="bi bi-check2 text-success me-2"></i>All workshops</li>
              <li class="mb-2"><i class="bi bi-check2 text-success me-2"></i>Lunch &amp; coffee</li>
            </ul>
            <button class="btn btn-warning w-100">Buy ticket</button>
          </div>
        </div>
      </div>

      <div class="col-12 col-md-6 col-lg-4">
        <div class="card h-100 text-center">
          <div class="card-body p-4">
            <h5 class="text-uppercase text-muted">VIP</h5>
            <div class="display-5 fw-bold my-3">$1,499</div>
            <ul class="list-unstyled text-start mb-4">
              <li class="mb-2"><i class="bi bi-check2 text-success me-2"></i>Everything above</li>
              <li class="mb-2"><i class="bi bi-check2 text-success me-2"></i>Speakers' dinner</li>
            </ul>
            <button class="btn btn-outline-dark w-100">Buy ticket</button>
          </div>
        </div>
      </div>

    </div>
  </section>
  ```
  * **Observation:** Every card uses `h-100` (full height of the row), which guarantees all three tiers are exactly the same height, even though their content lists are different lengths. This is the kind of micro-detail Bootstrap saves you from having to debug.

* Step 6: Add an Interactive FAQ Accordion

  Accordions need JavaScript to expand and collapse. Bootstrap's `.accordion` component already includes that JavaScript — you just paste the markup and it works.
  * Add the following HTML:
  ```html
  <section class="container py-5">
    <h2 class="text-center mb-4">FAQ</h2>
    <div class="accordion mx-auto" id="faqAccordion" style="max-width:720px;">
      <div class="accordion-item">
        <h3 class="accordion-header">
          <button class="accordion-button collapsed" type="button"
                  data-bs-toggle="collapse" data-bs-target="#faq1">
            Will the talks be recorded?
          </button>
        </h3>
        <div id="faq1" class="accordion-collapse collapse" data-bs-parent="#faqAccordion">
          <div class="accordion-body">Yes — every talk will be uploaded to YouTube within two weeks.</div>
        </div>
      </div>
      <!-- repeat for more FAQ items -->
    </div>
  </section>
  ```
  * **Observation:** Click an FAQ item. It smoothly expands. Click another — the first one closes automatically. You didn't write a single line of JavaScript. The `data-bs-*` attributes are how Bootstrap wires DOM behavior to its JS bundle declaratively. Used right, it means your "static" HTML can have rich interactive components for free.

## Checkpoints

* [ ] Build Your "Personal Developer Portfolio"  
      You're going to build the page you'll actually use to get your first internship, freelance gig, or job. A portfolio site is the most important Bootstrap project you'll ever build, and at the end of M16 we'll deploy this exact page to the public internet. Create a single HTML file using **Bootstrap 5 via CDN** and write **at most 30 lines** of custom CSS (color overrides only — no layout CSS). The page must satisfy every requirement below:
      * **Bootstrap Setup**: Include the Bootstrap 5 CSS via CDN in `<head>` and the Bootstrap 5 JS bundle just before `</body>`.
      * **Responsive Navbar with Anchor Links**: A `.navbar` component with your name on the left and at least 4 sections in the menu — `About`, `Projects`, `Skills`, `Contact` — each link jumping to a corresponding section on the page using `href="#section-id"`. The navbar must collapse to a hamburger on mobile.
      * **Hero / About Section**: A two-column hero with a photo or avatar on one side (`col-md-4`) and your name + short intro on the other (`col-md-8`). On mobile, the two columns must stack vertically — use the responsive grid classes, do not write a media query.
      * **Projects Grid (Bootstrap Cards)**: A section with **at least 3 project cards** built using `.card`. Each card has a project image (`.card-img-top`), a title (`.card-title`), a short description, two technology badges (`<span class="badge bg-secondary">React</span>` etc.), and a "View project" button. Use `h-100` on every card so they're equal height.
      * **Skills Section with Bootstrap Badges**: A grid or wrapped row of at least 8 skill badges — `HTML`, `CSS`, `JavaScript`, etc. — built with `.badge`. Use **at least three different `bg-*` color utilities** (e.g. `bg-primary`, `bg-success`, `bg-info`).
      * **Contact Section with a Bootstrap Form**: A working contact form using `.form-control`, `.form-label`, and a submit `.btn btn-primary`. At minimum: name field, email field, message textarea. (It doesn't have to actually send — just look polished.)
      * **At Least One Interactive Component**: Include **one** Bootstrap component that requires the JS bundle: an **accordion** ("Frequently Asked Questions about me"), a **carousel** of project screenshots, or a **modal** ("Download my résumé"). It must work without you writing any JS.
      * **Utility-Driven Spacing**: Demonstrate at least **six** different utility classes (`my-5`, `py-4`, `mx-auto`, `g-4`, `text-muted`, `fw-bold`, `shadow-sm`, `rounded-3`, `text-center`, etc.) and be able to explain in one sentence what each one does.
      * **Mobile Verification**: Open Chrome's Device Toggle. The page must look polished and have no horizontal scrollbar at 375px (phone), 768px (tablet), and 1280px (desktop). Specifically verify: the navbar collapses, the hero stacks, the project cards reflow, the contact form remains usable, and the JS-powered component still works on mobile.
