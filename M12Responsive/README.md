# M12 Responsive Design

## The "Why?"

The days when people only browsed the web on a desktop computer are long gone. A single website today is viewed on **dozens of different screen sizes**—from massive 4K monitors and ultrawide laptops down to tablets, phones, and even smartwatches.

A layout that looks beautiful at 1920px wide is often unusable at 375px. Text overflows, images stretch, navigation collapses into an unreadable mess, and visitors immediately bounce.

**Responsive design** is the practice of building websites that adapt to whatever screen they land on, like water that takes the shape of the container it's poured into. With the right techniques—a viewport meta tag, fluid units, and a few well-placed media queries—a single HTML file can deliver a great experience to every visitor, regardless of device.

## Goals

Understand the core principles of responsive web design and learn how to apply them with CSS.  
By the end of this module, you should be able to set the viewport meta tag, write `@media` rules to change styles based on screen width, use the **mobile-first approach**, and pick fluid units (`%`, `rem`, `vw`) that scale naturally with the screen.

## Core Concepts

### 1. The Viewport Meta Tag

Mobile browsers, by default, pretend to be desktops. They render the page at roughly 980px wide and then shrink it to fit the screen—making your text microscopic. To tell the browser "no, this page is already mobile-friendly," you **must** add this line inside the `<head>`:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

* `width=device-width` — match the actual device width (e.g. 390px on an iPhone).
* `initial-scale=1.0` — start at 100% zoom, no auto-shrinking.

Without this tag, none of your responsive CSS will work correctly on a real phone.

### 2. Media Queries

A **media query** is an "if/then" rule in CSS: *if* the screen matches certain conditions, *then* apply these styles. The most common condition is screen width.

```css
/* Default styles apply everywhere */
.container { width: 100%; }

/* These styles only apply when the screen is 768px wide or wider */
@media (min-width: 768px) {
  .container { width: 750px; margin: 0 auto; }
}
```

Two condition keywords you will use constantly:

* **`min-width`** — applies when the screen is **at least** this wide. Use this for the mobile-first approach.
* **`max-width`** — applies when the screen is **at most** this wide. Use this for desktop-first overrides.

### 3. Breakpoints

A **breakpoint** is the screen width at which your layout changes. There is no official standard, but these widths are common in the industry (and match Bootstrap's defaults):

| Device class       | Width range          | Typical breakpoint |
|--------------------|----------------------|--------------------|
| Phone              | up to 575px          | (base styles)      |
| Large phone / small tablet | 576px and up | `min-width: 576px` |
| Tablet             | 768px and up         | `min-width: 768px` |
| Laptop / desktop   | 992px and up         | `min-width: 992px` |
| Large desktop      | 1200px and up        | `min-width: 1200px` |

### 4. The Mobile-First Approach

Write your **base CSS for mobile**, then progressively add `@media (min-width: ...)` rules to enhance the layout as the screen gets larger.

```css
/* Mobile base: single column, full-width image */
.card { width: 100%; }

/* Tablet: two columns */
@media (min-width: 768px) {
  .card { width: 50%; }
}

/* Desktop: three columns */
@media (min-width: 992px) {
  .card { width: 33.333%; }
}
```

This approach keeps the CSS simple and the smallest devices fast, because they download the least amount of layout code.

### 5. Fluid Units

Pixels (`px`) are fixed. Responsive layouts also rely on **relative units** that scale with the context:

* **`%`** — percentage of the parent's size. Great for widths.
* **`rem`** — relative to the root font size (usually 16px). Great for font sizes and spacing.
* **`vw` / `vh`** — 1% of the viewport width / height. Great for hero sections.
* **`max-width`** instead of a fixed `width` — lets an element shrink on small screens but never exceed a sensible maximum.

```css
img      { max-width: 100%; }   /* Never overflow the parent */
.hero    { height: 60vh; }      /* Always 60% of the screen height */
h1       { font-size: 2rem; }   /* Scales with the user's font setting */
```

## Guided Practice

In this practice, we will build the homepage for a fictional travel blog called **"Wanderlust"**. A travel blog is the perfect playground for responsive design — it has a hero with a big photo, a grid of destination cards, a sidebar of popular posts, and a newsletter form. Each piece needs to reshape itself for phones, tablets, and desktops. See `travel_blog.html` in this folder for the finished result.

The layout transitions we'll build:

| Screen size       | Navbar           | Hero               | Destination grid | Sidebar |
|-------------------|------------------|--------------------|------------------|---------|
| Mobile (< 640px)  | Hamburger button | Text above photo   | 1 column         | Hidden  |
| Tablet (≥ 640px)  | Full links       | Side-by-side       | 2 columns        | Hidden  |
| Desktop (≥ 1024px)| Full links       | Side-by-side, bigger | 3 columns      | Visible |

* Step 1: Set Up the Viewport and Mobile-First Base

  Responsive design only works on real phones if you opt in to it with the viewport meta tag. Then write your default CSS assuming a *narrow* phone screen.
  * Create an HTML file. Inside `<head>`, add:
  ```html
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  ```
  * Add a `<style>` tag with the base mobile-first styles:
  ```css
  * { box-sizing: border-box; }

  body {
    font-family: 'Segoe UI', system-ui, sans-serif;
    margin: 0;
    color: #1f2937;
    background: #fffaf3;
    line-height: 1.6;
  }
  a { color: #c2410c; text-decoration: none; }
  ```
  * **Observation:** No media queries yet — these styles apply on every screen size and will be progressively enhanced.

* Step 2: Build a Navbar that Collapses to a Hamburger on Mobile

  This is one of the most common responsive patterns. On mobile, we show only the brand and a hamburger button. On tablets and up, the full navigation links are revealed.
  * Add the CSS:
  ```css
  .nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 1.5rem;
    background: white;
    box-shadow: 0 1px 4px rgba(0,0,0,0.05);
  }
  .nav .brand { font-weight: 800; color: #c2410c; }
  .nav .hamburger { background: none; border: none; font-size: 1.5rem; }
  .nav .links { display: none; }                  /* hide on mobile */
  .nav .links a { color: #1f2937; margin-left: 1.5rem; font-weight: 500; }

  @media (min-width: 768px) {
    .nav .hamburger { display: none; }            /* hide on tablet+ */
    .nav .links { display: block; }               /* show the links instead */
  }
  ```
  * Add the HTML inside `<body>`:
  ```html
  <nav class="nav">
    <div class="brand">✈ Wanderlust</div>
    <button class="hamburger">☰</button>
    <div class="links">
      <a href="#">Destinations</a>
      <a href="#">Guides</a>
      <a href="#">Stories</a>
    </div>
  </nav>
  ```
  * **Observation:** Resize the browser narrower than 768px — the links vanish and the hamburger appears. Wider than 768px and it flips. We are **showing different markup on different screens** purely with CSS.

* Step 3: Build a Hero That Stacks on Mobile and Splits on Desktop

  Mobile screens are tall and narrow, so we stack the headline above a smaller photo. On desktop, we have horizontal room — switch to a two-column grid and increase the headline size.
  * Add the CSS:
  ```css
  .hero { padding: 2rem 1.5rem; background: linear-gradient(135deg, #fed7aa, #fdba74); }
  .hero-inner { max-width: 1100px; margin: 0 auto; }
  .hero h1 { font-size: 2rem; margin: 0 0 0.75rem; color: #7c2d12; }
  .hero p  { color: #9a3412; margin: 0 0 1.25rem; }
  .hero img { max-width: 100%; border-radius: 16px; margin-top: 1.5rem; }

  @media (min-width: 768px) {
    .hero { padding: 4rem 2rem; }
    .hero h1 { font-size: 3rem; }                /* bigger headline */
    .hero-inner {
      display: grid;
      grid-template-columns: 1fr 1fr;            /* side-by-side */
      gap: 3rem;
      align-items: center;
    }
    .hero img { margin-top: 0; }
  }
  ```
  * Add the HTML below the navbar:
  ```html
  <header class="hero">
    <div class="hero-inner">
      <div>
        <h1>Slow travel,<br>real moments.</h1>
        <p>Hand-picked itineraries from people who actually lived there — not algorithms.</p>
      </div>
      <img src="https://images.unsplash.com/photo-1469854523086-cc02fe5d8800?w=800" alt="Mountain road">
    </div>
  </header>
  ```
  * **Observation:** Use `max-width: 100%` on the image so it never overflows, no matter how narrow the screen gets. Without that single line, your travel photos will blow past the right edge of the phone every single time.

* Step 4: Build a Destination Grid That Reflows 1 → 2 → 3 Columns

  This is the heart of the page — the same content, three different layouts. Mobile-first means we start with one column and only add more columns as space allows.
  * Add the CSS:
  ```css
  .destinations {
    display: grid;
    grid-template-columns: 1fr;                  /* mobile: 1 column */
    gap: 1.5rem;
  }
  @media (min-width: 640px) {
    .destinations { grid-template-columns: repeat(2, 1fr); }   /* tablet: 2 */
  }
  @media (min-width: 1024px) {
    .destinations { grid-template-columns: repeat(3, 1fr); }   /* desktop: 3 */
  }

  .card { background: white; border-radius: 12px; overflow: hidden;
          box-shadow: 0 4px 8px rgba(0,0,0,0.06); }
  .card img { width: 100%; height: 200px; object-fit: cover; }
  .card-body { padding: 1.25rem; }
  .card-body h3 { margin: 0 0 0.5rem; }
  ```
  * Add HTML for three or four destination cards:
  ```html
  <div class="destinations" style="max-width:1200px; margin: 2.5rem auto; padding: 0 1.5rem;">
    <article class="card">
      <img src="https://images.unsplash.com/photo-1542051841857-5f90071e7989?w=600" alt="Tokyo">
      <div class="card-body"><h3>Tokyo, Japan</h3><p>Neon-lit alleyways and the world's best convenience-store coffee.</p></div>
    </article>
    <article class="card">
      <img src="https://images.unsplash.com/photo-1502602898657-3e91760cbb34?w=600" alt="Paris">
      <div class="card-body"><h3>Paris, France</h3><p>Skip the Eiffel. Wander the Marais at sunset instead.</p></div>
    </article>
    <article class="card">
      <img src="https://images.unsplash.com/photo-1537996194471-e657df975ab4?w=600" alt="Bali">
      <div class="card-body"><h3>Ubud, Bali</h3><p>Rice terraces and a quiet co-working scene.</p></div>
    </article>
  </div>
  ```
  * **Observation:** Notice how `object-fit: cover` on the image is doing crucial responsive work — it crops photos to a uniform height regardless of their original aspect ratio, so the grid never breaks visually.

* Step 5: Reveal a Sidebar Only on Desktop

  Sidebars work brilliantly on wide screens and ruin the experience on a phone. Use a media query to **hide content entirely** on small screens.
  * Wrap the destinations grid and add a sidebar:
  ```css
  .page { max-width: 1200px; margin: 0 auto; padding: 2.5rem 1.5rem; }
  .sidebar { display: none; }                    /* hidden by default */

  @media (min-width: 1024px) {
    .page {
      display: grid;
      grid-template-columns: 1fr 300px;          /* fluid main + fixed sidebar */
      gap: 2.5rem;
    }
    .sidebar { display: block; }                 /* reveal on desktop */
  }
  ```
  * Restructure the destinations HTML inside `.page`:
  ```html
  <div class="page">
    <main>
      <h2 style="color:#7c2d12;">This month's picks</h2>
      <div class="destinations">…the cards from Step 4…</div>
    </main>
    <aside class="sidebar">
      <h4 style="color:#7c2d12;">Popular this week</h4>
      <p>How to pack carry-on for 3 weeks</p>
      <p>The case for one-bag travel</p>
    </aside>
  </div>
  ```
  * **Observation:** This is the **mobile-first content priority** rule in action: the most important content (the destination cards) is visible on every device, and supplementary content (the sidebar) only appears when the screen has room for it.

* Step 6: Test Everything in Chrome DevTools

  Real responsive design is verified in the browser, not assumed in the editor.
  * Open the page in Chrome and press **F12**, then click the Device Toggle icon (or press `Ctrl + Shift + M` / `Cmd + Shift + M`).
  * Drag the width slider from 320px up to 1440px. Watch the four transitions happen in order:
    1. At ~640px, the destination grid jumps from 1 → 2 columns.
    2. At ~768px, the hero splits side-by-side and the hamburger turns into full nav links.
    3. At ~1024px, the destination grid jumps from 2 → 3 columns and the sidebar appears.
  * **Observation:** A real responsive page has **multiple** breakpoints, each triggering a different transition. The goal is to make every transition feel intentional, not jarring — try the page at 639px and 641px and confirm nothing breaks at the boundary.

## Checkpoints

* [ ] Build a "Local Coffee Shop" Homepage  
      You're building the homepage for a small specialty coffee shop. It needs to look great on a customer's phone (most people will visit while walking past the shop), but also work nicely on a laptop for people browsing from home. Create a single HTML file (with a `<style>` tag) that satisfies every requirement below using only the viewport meta tag and CSS media queries:
      * **Viewport Setup**: Include the `<meta name="viewport">` tag and be able to explain *why* it's required (what would happen on a real iPhone without it).
      * **Mobile-First Hero**: A hero section with the café name, a tagline, and an "Order Now" call-to-action button. On mobile it stacks vertically and centers the text; on desktop (≥ 768px) it switches to side-by-side with a photo of a latte beside the text.
      * **Menu Grid That Reflows**: A grid of at least 6 menu items (drinks or pastries), each with an image, name, and price. The grid must:
        * Show **1 column** on phones (< 640px)
        * Switch to **2 columns** on tablets (≥ 640px)
        * Switch to **3 columns** on desktops (≥ 1024px)
      * **Conditionally-Visible Element**: Add something that is **visible on one screen size but hidden on another** — for example, a "Reserve a Table" sticky button that only appears on mobile (`display: none` above 768px), or a "Hours & Location" sidebar that only appears on desktop.
      * **Fluid Hero Image**: At least one image must use `max-width: 100%;` and `object-fit: cover;` so it never overflows, and so it crops gracefully at any aspect ratio.
      * **Fluid Units**: Use at least one relative unit other than `px` (such as `rem`, `%`, `vw`, or `vh`) and be able to explain why you chose it for that specific property.
      * **DevTools Verification**: Open Chrome DevTools' Device Toggle and test at **three widths**: 375px (iPhone), 768px (iPad), and 1280px (laptop). Confirm the menu reflows, the conditionally-visible element behaves correctly, and nothing overflows the viewport horizontally at any width.
