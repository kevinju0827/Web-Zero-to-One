# M14 CSS Grid

## The "Why?"

Flexbox is brilliant at arranging items in a **single line**—one row, or one column. But the moment your design needs control over **rows and columns at the same time**, Flexbox starts to fight you.

* A magazine-style page where the header spans the full width, the sidebar takes one column, and the article fills two columns
* A photo gallery where one "hero" image takes up a 2×2 block and the smaller thumbnails fill in around it
* A dashboard with a header, sidebar, main content, and footer—each in its own region of a fixed blueprint

These are **two-dimensional layouts**, and that is exactly what CSS Grid was built for. Grid lets you draw a blueprint of rows and columns, then drop elements into specific cells. It is the most powerful layout system available in CSS today, and it has replaced years of hacks with a clean, declarative model.

## Goals

Understand how to define a two-dimensional layout using a grid container and learn how to place items into specific cells.  
By the end of this module, you should be able to apply `display: grid`, define column and row tracks with `grid-template-columns` and `grid-template-rows`, use the `fr` unit and the `repeat()` function, space cells apart with `gap`, and make individual items span multiple rows or columns with `grid-column` and `grid-row`.

## Core Concepts

### 1. The Grid Container

Just like Flexbox, you start with a parent and turn it into a grid container:

```css
.container {
  display: grid;
}
```

Direct children of the container automatically become **grid items**.

### 2. Defining Tracks: Columns and Rows

A "track" is just CSS-speak for a column or a row. You define them on the container with:

* **`grid-template-columns`** — the number and width of columns
* **`grid-template-rows`** — the number and height of rows

```css
.container {
  display: grid;
  grid-template-columns: 200px 1fr 1fr;   /* Three columns */
  grid-template-rows: 80px auto;          /* Two rows */
}
```

### 3. The `fr` Unit

`fr` stands for "fractional unit." It represents **a share of the leftover space** in the container after fixed sizes have been accounted for.

```css
/* Three columns, all equal width */
grid-template-columns: 1fr 1fr 1fr;

/* Three columns where the middle one is twice as wide */
grid-template-columns: 1fr 2fr 1fr;

/* A fixed sidebar plus a fluid main area */
grid-template-columns: 250px 1fr;
```

`fr` is what makes Grid feel modern: you describe **proportions** instead of doing arithmetic with percentages.

### 4. The `repeat()` Function

When you have many tracks of the same size, `repeat()` saves a lot of typing:

```css
/* Long form */
grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr;

/* Shorthand */
grid-template-columns: repeat(6, 1fr);
```

You can also combine `repeat()` with `auto-fit` or `auto-fill` for responsive grids that adapt to the container width automatically:

```css
/* As many 200px+ columns as will fit, stretching to fill the row */
grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
```

### 5. `gap`

Add space between rows and columns without any margin hacks:

```css
.container {
  display: grid;
  gap: 20px;            /* Same gap for rows and columns */
  /* or: */
  row-gap: 16px;
  column-gap: 24px;
}
```

### 6. Placing Items: `grid-column` and `grid-row`

By default, items flow into cells one at a time. To make a single item **span multiple cells**, use these properties on the *item*:

```css
.header   { grid-column: span 3; }   /* Take up 3 columns */
.sidebar  { grid-row: span 2; }      /* Take up 2 rows */
.feature  { grid-column: 1 / 3; }    /* From column line 1 to line 3 (= columns 1 and 2) */
```

Grid lines are numbered starting at 1 on the left/top. `grid-column: 1 / 3` means "start at line 1 and end at line 3," which is the same as "span 2 columns."

## Guided Practice

In this practice, we will build a **photographer's portfolio website** for a fictional landscape artist named "Mira Okafor". A photo portfolio is the canonical use case for CSS Grid because every photograph has its own aspect ratio and visual weight — some shots deserve to be huge, some are tall portraits, some are wide panoramas. Grid lets us compose them into a single magazine-style layout, then collapse it gracefully on mobile. See `photo_portfolio.html` in this folder for the finished result.

The blueprint we're building:

```
+---------------+---------------+-------+-------+
|                               |       |       |
|         HERO (2 × 2)          | TALL  | PHOTO |
|                               |  (2)  |       |
|                               |       +-------+
|                               |       | PHOTO |
+---------------+---------------+-------+-------+
|              WIDE PANORAMA (2 × 1)    | PHOTO |
+---------------+---------------+-------+-------+
```

* Step 1: Set Up the Canvas

  A photography site should feel quiet and out of the way of the images themselves. Start with neutral colors and a serif headline font.
  * Create an HTML file and add a `<style>` tag inside the `<head>`.
  * Add the following CSS:
  ```css
  * { box-sizing: border-box; }

  body {
    font-family: Georgia, 'Times New Roman', serif;
    margin: 0;
    background: #fafaf9;
    color: #18181b;
    line-height: 1.5;
  }
  ```
  * Add the following HTML inside `<body>`:
  ```html
  <header style="text-align:center; padding:4rem 1.5rem 2rem;">
    <h1 style="font-weight:400; font-size:2.5rem; margin:0; letter-spacing:0.05em;">Mira Okafor</h1>
    <p style="color:#78716c; font-style:italic;">Light, distance, weather, time</p>
  </header>
  ```

* Step 2: Define the Magazine Grid Blueprint

  This is the most powerful step in Grid: a single CSS rule defines the entire layout. A 4-column grid with each row being 200px tall is enough to compose any magazine layout we want.
  * Add the following CSS:
  ```css
  .gallery {
    display: grid;
    grid-template-columns: repeat(4, 1fr);   /* 4 equal columns */
    grid-auto-rows: 200px;                   /* every row is 200px tall */
    gap: 1rem;
    max-width: 1300px;
    margin: 3rem auto;
    padding: 0 1.5rem;
  }

  .photo {
    position: relative;
    overflow: hidden;
    border-radius: 4px;
    background: #d6d3d1;
  }
  .photo img {
    width: 100%;
    height: 100%;
    object-fit: cover;       /* crop without distortion */
  }
  ```
  * Add the gallery HTML below the header. Use any 7 photos you like:
  ```html
  <section class="gallery">
    <figure class="photo"><img src="https://images.unsplash.com/photo-1469474968028-56623f02e42e?w=1200" alt=""></figure>
    <figure class="photo"><img src="https://images.unsplash.com/photo-1500382017468-9049fed747ef?w=600" alt=""></figure>
    <figure class="photo"><img src="https://images.unsplash.com/photo-1465146344425-f00d5f5c8f07?w=600" alt=""></figure>
    <figure class="photo"><img src="https://images.unsplash.com/photo-1499002238440-d264edd596ec?w=600" alt=""></figure>
    <figure class="photo"><img src="https://images.unsplash.com/photo-1418065460487-3e41a6c84dc5?w=1200" alt=""></figure>
    <figure class="photo"><img src="https://images.unsplash.com/photo-1470770841072-f978cf4d019e?w=600" alt=""></figure>
    <figure class="photo"><img src="https://images.unsplash.com/photo-1431794062232-2a99a5431c6c?w=600" alt=""></figure>
  </section>
  ```
  * **Observation:** Right now, every photo is a uniform 1×1 cell, so the gallery looks like a regular grid. Powerful, but not yet *interesting*. The magic is what we do next.

* Step 3: Make the Hero Image Span 2 Columns AND 2 Rows

  In a real photography portfolio, one image is the showstopper — your most striking shot deserves a 2×2 cell.
  * Add the following CSS:
  ```css
  .photo-hero {
    grid-column: span 2;     /* take up 2 columns */
    grid-row: span 2;        /* AND take up 2 rows */
  }
  ```
  * Update the first `<figure>` in the gallery:
  ```html
  <figure class="photo photo-hero"><img src="..." alt=""></figure>
  ```
  * **Observation:** The first photograph now occupies a 2×2 block in the upper-left corner, and Grid intelligently flows the remaining photos around it without you having to specify exactly where each one goes. This is what Grid does that no previous CSS layout system could.

* Step 4: Add a Tall Portrait and a Wide Panorama

  Different aspect ratios deserve different cell shapes. A portrait shot looks great as 1 col × 2 rows, and a panorama looks great as 2 cols × 1 row.
  * Add the following CSS:
  ```css
  .photo-tall {
    grid-row: span 2;        /* 1 column, 2 rows tall — for portraits */
  }
  .photo-wide {
    grid-column: span 2;     /* 2 columns wide, 1 row — for panoramas */
  }
  ```
  * Update the 3rd photo to `class="photo photo-tall"` and the 5th photo to `class="photo photo-wide"`.
  * **Observation:** The layout now has visual rhythm — large/small/tall/wide cells creating an asymmetric, magazine-like composition. This is the kind of layout that print designers have used for a century. CSS Grid finally brings it to the web cleanly.

* Step 5: Add Caption Overlays on Hover

  Each photo deserves a caption — but we don't want it cluttering the visual flow. A hover overlay is the classic pattern.
  * Add the following CSS:
  ```css
  .photo .caption {
    position: absolute;
    left: 0; right: 0; bottom: 0;
    padding: 1rem;
    background: linear-gradient(180deg, transparent, rgba(0, 0, 0, 0.75));
    color: white;
    font-family: 'Segoe UI', system-ui, sans-serif;
    opacity: 0;
    transition: opacity 0.3s;
  }
  .photo:hover .caption { opacity: 1; }
  .photo .caption strong { display: block; font-size: 1rem; }
  .photo .caption span { font-size: 0.8rem; opacity: 0.85; }
  ```
  * Add a `<figcaption class="caption">` inside each `<figure>`:
  ```html
  <figure class="photo photo-hero">
    <img src="..." alt="">
    <figcaption class="caption">
      <strong>Lake at first light</strong>
      <span>Patagonia, Chile · 2025</span>
    </figcaption>
  </figure>
  ```
  * **Observation:** Notice how the absolutely-positioned caption works flawlessly inside the Grid cell. Grid and the `position` property compose without fighting each other — Grid handles the macro layout of the page, `position` handles the micro layout inside one cell.

* Step 6: Add a Responsive Series Grid With `auto-fit`

  Below the featured gallery, we'll add a "Series" section that uses Grid's smartest feature: `auto-fit` + `minmax()` for layouts that **automatically adjust their column count** based on available space, with no media queries needed.
  * Add the following CSS:
  ```css
  .series-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1rem;
    max-width: 1300px;
    margin: 5rem auto;
    padding: 0 1.5rem;
  }
  .series-card {
    aspect-ratio: 4 / 5;     /* every card is a portrait-shaped tile */
    background: #d6d3d1;
    border-radius: 4px;
  }
  ```
  * Add the HTML:
  ```html
  <h2 style="max-width:1300px; margin:5rem auto 1rem; padding:0 1.5rem; font-weight:400;">Series</h2>
  <section class="series-grid">
    <div class="series-card"></div>
    <div class="series-card"></div>
    <div class="series-card"></div>
    <div class="series-card"></div>
    <div class="series-card"></div>
  </section>
  ```
  * **Observation:** Resize the browser. The series grid automatically packs **as many 240px+ columns as will fit**, and stretches them with `1fr` to fill the row. This is the responsive-grid superpower — one line of CSS replaces five media queries.

* Step 7: Collapse the Magazine Layout on Mobile

  On a 375px-wide phone, a 4-column grid would crush every photograph into a tiny square. We collapse to a 2-column layout and reset the spans.
  * Add the following CSS:
  ```css
  @media (max-width: 768px) {
    .gallery {
      grid-template-columns: 1fr 1fr;       /* drop from 4 to 2 columns */
      grid-auto-rows: 160px;
    }
    .photo-hero, .photo-wide { grid-column: span 2; }
    .photo-tall { grid-row: auto; }         /* reset the tall span */
  }
  ```
  * **Observation:** Open Chrome's DevTools, click the Device Toggle, and drag the width from 1400px down to 375px. The gallery collapses from a 4-column magazine to a tidy 2-column mobile layout. Open the **Elements** panel, hover over `.gallery`, and Chrome will overlay the grid lines on the page — confirming your spans land exactly where you intended.

## Checkpoints

* [ ] Build a "Tech News Magazine" Homepage  
      You're building the homepage for an online tech news magazine. The page needs to show a featured story prominently, a sidebar of trending headlines, several category sections, and a newsletter signup — all composed on a single Grid blueprint. Create a single HTML file (with a `<style>` tag) that satisfies every requirement below using **only CSS Grid** (no Flexbox needed for the layout itself):
      * **Top Banner Grid**: At the top of the page, build a grid with a featured story that spans **2 columns × 2 rows** on the left, a tall "Trending" sidebar that spans **1 column × 2 rows** on the right, and 2 smaller article cards stacked vertically next to the featured story. Use proportional column widths via `fr` (e.g. `grid-template-columns: 2fr 1fr 1fr;`).
      * **Category Sections with `auto-fit`**: Below the banner, add at least 2 category sections (e.g. "AI", "Hardware", "Startups"). Each section is its own grid using `grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));` so the cards reflow automatically without any media query.
      * **Featured Quote Block**: Somewhere in the layout, place a pull-quote (a large styled quote from an article) that spans the **full width** of its grid using `grid-column: 1 / -1;`. Explain (in a comment or in your notes) why `1 / -1` is sometimes preferable to `span N`.
      * **Asymmetric Aspect Ratios**: At least one card in your banner must be visibly **taller** than its neighbors using `grid-row: span 2;`, and at least one must be visibly **wider** using `grid-column: span 2;`. The point is to demonstrate non-uniform cell sizing — like a real magazine.
      * **`gap` Only, No Margins**: Use the `gap` property for all spacing between cards. Do not use `margin` on the cards themselves.
      * **Mobile Collapse**: Add a media query (`@media (max-width: 768px)`) that collapses the entire layout to **1 or 2 columns** on phones and resets every `span` so nothing breaks at narrow widths.
      * **Self-Validation**: Open Chrome DevTools. In the Elements panel, hover over each of your grid containers — Chrome overlays the grid lines on the page. Use the overlay to confirm every featured card lands in exactly the cells you intended, and that the layout still looks intentional at 375px, 768px, and 1280px wide.
