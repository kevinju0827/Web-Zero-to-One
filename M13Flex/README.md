# M13 Flexbox

## The "Why?"

Before Flexbox arrived, aligning things in CSS was famously painful. Developers used `float`, `inline-block`, or even HTML `<table>` tags to put items side-by-side—each with its own bugs and gotchas. Vertically centering a single line of text was so notoriously hard that "how do I center a div?" became a running joke in the industry.

**Flexbox** (the Flexible Box Module) was designed specifically to solve this. It is a **one-dimensional** layout system: you arrange items along a single row, or a single column, and Flexbox handles the spacing, alignment, and wrapping for you. With just a few CSS properties, you can build navigation bars, button rows, sidebars, perfectly centered hero sections, and responsive card grids—cleanly, without hacks.

If Grid is for building a whole 2D page layout, Flexbox is for arranging the contents inside any **single component**. You will use it on almost every site you ever build.

## Goals

Master Flexbox by learning how the container controls the layout of its children along two perpendicular axes.  
By the end of this module, you should be able to apply `display: flex`, switch direction with `flex-direction`, distribute space with `justify-content`, align across the cross axis with `align-items`, allow wrapping with `flex-wrap`, and grow/shrink individual items with the `flex` shorthand.

## Core Concepts

### 1. Container vs. Items

Flexbox always involves two layers:

* The **flex container** — the parent element where you apply `display: flex`.
* The **flex items** — the direct children, which automatically become flex items.

Most Flexbox properties go on the container and affect all the children. A few special ones go on the items themselves.

```css
.container {
  display: flex; /* The parent becomes a flex container */
}
```

### 2. The Two Axes

Flexbox lays things out along two axes:

* The **main axis** — the direction items are laid out. By default it goes left → right.
* The **cross axis** — the axis perpendicular to the main axis. By default it goes top → bottom.

`flex-direction` lets you choose which way the main axis points:

| Value             | Main axis direction        |
|-------------------|----------------------------|
| `row` (default)   | left → right               |
| `row-reverse`     | right → left               |
| `column`          | top → bottom               |
| `column-reverse`  | bottom → top               |

When you change `flex-direction` from `row` to `column`, the axes swap — meaning `justify-content` and `align-items` swap with them. This catches everyone the first time.

### 3. Main Axis Properties (on the container)

These control spacing **along** the main axis.

* **`justify-content`** — distribute space along the main axis.
  * `flex-start` — pack to the start
  * `flex-end` — pack to the end
  * `center` — pack to the center
  * `space-between` — items at the edges, equal gap between them
  * `space-around` — equal gap around every item
  * `space-evenly` — equal gap between every item *and* the edges
* **`gap`** — sets a fixed gap **between** flex items (much cleaner than using margins).

### 4. Cross Axis Properties (on the container)

These control alignment **across** the cross axis.

* **`align-items`** — align items on the cross axis.
  * `stretch` (default) — items fill the cross axis
  * `flex-start` / `flex-end` — pack to one side
  * `center` — center on the cross axis
  * `baseline` — align by text baseline

### 5. Wrapping

By default, flex items try to fit on a single line and will shrink to do so. If you want them to wrap onto multiple lines when there isn't enough room, set:

```css
.container {
  display: flex;
  flex-wrap: wrap;
}
```

### 6. Item Properties (on the items)

A few important properties live on the items themselves:

* **`flex: 1`** — shorthand telling an item to grow and fill the available space. If three items all have `flex: 1`, they'll share the row equally.
* **`flex: 0 0 200px`** — fix the item's size at 200px and don't allow it to grow or shrink.
* **`order`** — change the visual order of items without changing the HTML.

## Guided Practice

In this practice, we will build a **SaaS pricing page** for a fictional product called "Stackly". A pricing page is the canonical Flexbox showcase because it stacks almost every Flex pattern in one screen: a navbar with logo and CTA (`space-between`), a perfectly centered hero, three pricing cards in a row of equal-height columns, an equally-distributed stats banner, and a vertical FAQ list. See `pricing_plans.html` in this folder for the finished result.

* Step 1: Set Up the Canvas

  Start with the base styles and a clean container.
  * Create an HTML file and add a `<style>` tag inside the `<head>`.
  * Add the following CSS:
  ```css
  * { box-sizing: border-box; }

  body {
    font-family: 'Segoe UI', system-ui, sans-serif;
    margin: 0;
    background: #f8fafc;
    color: #0f172a;
    line-height: 1.6;
  }
  ```

* Step 2: Build the Navbar with `space-between`

  Logo on the left, menu items + CTA on the right — pushed apart by `justify-content: space-between`. This is the single most common Flexbox pattern on the web.
  * Add the following CSS:
  ```css
  .nav {
    display: flex;
    justify-content: space-between;   /* push the brand and menu to opposite ends */
    align-items: center;              /* vertical center on the cross axis */
    padding: 1rem 2rem;
    background: white;
    border-bottom: 1px solid #e2e8f0;
  }
  .nav .brand { font-weight: 800; color: #4f46e5; }
  .nav .menu {
    display: flex;                    /* nested flex row */
    align-items: center;
    gap: 1.25rem;                     /* clean spacing without margin math */
  }
  .nav .menu a { color: #475569; text-decoration: none; font-weight: 500; }
  .nav .menu .btn-primary {
    background: #4f46e5;
    color: white;
    padding: 0.5rem 1.1rem;
    border-radius: 8px;
  }
  ```
  * Add the HTML inside `<body>`:
  ```html
  <nav class="nav">
    <div class="brand">⌬ Stackly</div>
    <div class="menu">
      <a href="#">Features</a>
      <a href="#">Docs</a>
      <a href="#">Log in</a>
      <a href="#" class="btn-primary">Start free</a>
    </div>
  </nav>
  ```
  * **Observation:** Notice the nested flex containers. `.nav` arranges its two children (brand + menu) across the row, while `.menu` is its own flex container arranging the links inside it. Flexbox composes cleanly — you can nest containers as deep as you want.

* Step 3: Build the Hero Using Perfect Centering

  A pricing hero is the classic "centered headline" pattern. With Flexbox, this takes two properties.
  * Add the following CSS:
  ```css
  .hero {
    display: flex;
    flex-direction: column;          /* stack the eyebrow, headline, and CTA */
    align-items: center;             /* horizontal center because we're in column mode */
    text-align: center;
    padding: 4rem 1.5rem 3rem;
  }
  .hero .eyebrow {
    color: #4f46e5;
    font-weight: 700;
    text-transform: uppercase;
    font-size: 0.85rem;
  }
  .hero h1 { font-size: 2.5rem; margin: 0.5rem 0 0.75rem; }
  .hero p  { color: #64748b; max-width: 600px; margin: 0 0 1.75rem; }
  ```
  * Add the HTML below the navbar:
  ```html
  <section class="hero">
    <span class="eyebrow">Pricing</span>
    <h1>Simple, fair pricing.</h1>
    <p>Start free. Upgrade when your team grows. Cancel any time.</p>
  </section>
  ```
  * **Observation:** Once you change `flex-direction` to `column`, the axes swap — `align-items` now controls *horizontal* alignment (because the cross axis is now horizontal), and `justify-content` would control *vertical* alignment. This trip-up catches everyone the first time.

* Step 4: Build the Three Pricing Tiers (the critical Flexbox pattern)

  Here is where Flexbox really earns its keep. We want three cards side-by-side, **all the same height** regardless of how much content each one contains, and we want the "Get Started" button **always aligned at the bottom** of each card. Two key tricks: the outer row uses `align-items: stretch` (the default) so heights match, and each card uses `flex-direction: column` with `margin-top: auto` on the CTA to push it to the bottom.
  * Add the following CSS:
  ```css
  /* The row of tiers */
  .tiers {
    display: flex;
    flex-wrap: wrap;                 /* allow wrapping on small screens */
    gap: 1.5rem;
    justify-content: center;
    align-items: stretch;            /* equal heights for every card */
    padding: 2rem 1.5rem 4rem;
    max-width: 1100px;
    margin: 0 auto;
  }

  /* Each individual card */
  .tier {
    display: flex;
    flex-direction: column;          /* stack header → price → features → cta */
    background: white;
    border-radius: 16px;
    padding: 2rem;
    box-shadow: 0 4px 12px rgba(15, 23, 42, 0.06);
    flex: 1 1 280px;                 /* grow, shrink, base width 280px */
    max-width: 340px;
  }

  /* The feature list */
  .features {
    list-style: none;
    padding: 0;
    margin: 0 0 1.75rem;
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
  }
  .features li { display: flex; align-items: center; gap: 0.5rem; }

  /* The magic line: push the CTA button to the bottom of the card */
  .tier .cta {
    margin-top: auto;                /* absorb all remaining vertical space above */
    background: #e2e8f0;
    padding: 0.8rem;
    text-align: center;
    border-radius: 10px;
    font-weight: 700;
    text-decoration: none;
    color: #0f172a;
  }
  ```
  * Add the HTML:
  ```html
  <section class="tiers">
    <div class="tier">
      <h3>Starter</h3>
      <p>For solo builders.</p>
      <div class="price"><strong style="font-size:2.5rem;">$0</strong> / month</div>
      <ul class="features">
        <li>✓ 1 project</li>
        <li>✓ Up to 3 collaborators</li>
        <li>✓ Community support</li>
      </ul>
      <a class="cta" href="#">Get started free</a>
    </div>

    <div class="tier">
      <h3>Team</h3>
      <p>For growing teams.</p>
      <div class="price"><strong style="font-size:2.5rem;">$24</strong> / user / mo</div>
      <ul class="features">
        <li>✓ Unlimited projects</li>
        <li>✓ Up to 25 collaborators</li>
        <li>✓ Custom domains</li>
        <li>✓ Slack &amp; email support</li>
        <li>✓ Audit log (90 days)</li>
      </ul>
      <a class="cta" href="#">Start trial</a>
    </div>

    <div class="tier">
      <h3>Enterprise</h3>
      <p>For compliance needs.</p>
      <div class="price"><strong style="font-size:2.5rem;">Custom</strong></div>
      <ul class="features">
        <li>✓ Everything in Team</li>
        <li>✓ SSO &amp; SCIM</li>
        <li>✓ SOC 2 report</li>
      </ul>
      <a class="cta" href="#">Talk to sales</a>
    </div>
  </section>
  ```
  * **Observation:** The middle "Team" card has more features than the others, yet **all three cards are exactly the same height** and **all three CTAs are flush at the bottom**. This is the killer Flexbox use case that took dozens of lines of buggy CSS before Flexbox existed. Try removing `margin-top: auto` from the CTA — the buttons immediately collapse upward, leaving ugly gaps below them.

* Step 5: Add a Stats Banner with Equal-Sized Columns

  Marketing pages love these "12K customers / 99.99% uptime / 38 countries" banners. Each stat should claim an equal share of the row, regardless of how many digits its number has.
  * Add the following CSS:
  ```css
  .stats {
    display: flex;
    justify-content: space-around;
    background: #0f172a;
    color: white;
    padding: 2.5rem 1.5rem;
    flex-wrap: wrap;
  }
  .stat { flex: 1; min-width: 140px; text-align: center; }
  .stat .num { font-size: 2.25rem; font-weight: 800; color: #fbbf24; }
  .stat .label { color: #94a3b8; font-size: 0.9rem; }
  ```
  * Add the HTML:
  ```html
  <section class="stats">
    <div class="stat"><div class="num">12K+</div><div class="label">Teams shipping</div></div>
    <div class="stat"><div class="num">99.99%</div><div class="label">Uptime</div></div>
    <div class="stat"><div class="num">38</div><div class="label">Countries</div></div>
    <div class="stat"><div class="num">4.9 / 5</div><div class="label">Support rating</div></div>
  </section>
  ```
  * **Observation:** `flex: 1` on every stat makes them claim equal width. The number `99.99%` doesn't take more room than `38`, because Flexbox is distributing space by ratio, not by content. This is the trick behind every clean, evenly-aligned marketing banner you've ever seen.

* Step 6: Build a Vertical FAQ List

  We close out with the simplest pattern: a column of items spaced apart by `gap`.
  * Add the following CSS:
  ```css
  .faq {
    max-width: 720px;
    margin: 0 auto;
    padding: 4rem 1.5rem;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }
  details {
    background: white;
    border-radius: 12px;
    padding: 1rem 1.25rem;
    box-shadow: 0 2px 6px rgba(15, 23, 42, 0.04);
  }
  details summary { font-weight: 700; cursor: pointer; }
  ```
  * Add the HTML:
  ```html
  <section class="faq">
    <h2 style="text-align:center;">Frequently asked</h2>
    <details>
      <summary>Can I switch plans later?</summary>
      <p>Yes. Upgrade or downgrade any time — we prorate everything to the day.</p>
    </details>
    <details>
      <summary>What if I exceed my plan limits?</summary>
      <p>We'll email you. You'll have 14 days to upgrade or trim your usage.</p>
    </details>
    <details>
      <summary>Do you offer student discounts?</summary>
      <p>Yes — 50% off Team plans for verified students.</p>
    </details>
  </section>
  ```
  * **Observation:** Notice the consistent rhythm. `gap: 1rem` gives every item the same vertical space — no margin math, no last-child resets. That's the modern Flexbox spacing pattern.

## Checkpoints

* [ ] Build a "Messaging App" UI (Slack / Discord / Messenger style)  
      You're going to lay out a chat application. A chat UI is **the** Flexbox showcase: it has a thin sidebar of channels, a main conversation column, and a message bar pinned to the bottom — and almost everything inside it is a row or column of items aligned along an axis. Create a single HTML file (with a `<style>` tag) that satisfies every requirement below using only Flexbox:
      * **Full-Screen Two-Column Shell**: Make the page exactly the height of the viewport (`height: 100vh`). Use `display: flex` on the body or a wrapper to create two columns: a fixed-width sidebar (~260px) on the left, and a main content area that fills the rest of the screen using `flex: 1`.
      * **Sidebar with Vertical Channel List**: The sidebar uses `flex-direction: column`. At the top, a brand/workspace name. Below it, a list of at least 5 "channels" (e.g. `# general`, `# random`, `# engineering`) stacked vertically. At the **bottom of the sidebar**, pin a user profile badge (avatar + name). Use `margin-top: auto` on the profile badge to push it to the bottom regardless of how many channels are above it.
      * **Conversation Header with `space-between`**: At the top of the main column, a header showing the channel name on the left and a row of action icons (search, call, video, settings) on the right — split using `justify-content: space-between`.
      * **Scrollable Message List**: A middle area that takes all remaining vertical space (`flex: 1`) and scrolls when there are many messages. Inside, render at least 8 messages. Each message is itself a flex row containing an avatar circle on the left and a message bubble on the right (`align-items: flex-start` so the avatar lines up with the top of long messages).
      * **Message Input Pinned to the Bottom**: A flex row at the bottom of the main column containing a text input that uses `flex: 1` to fill the available width, and a "Send" button beside it. The input row must stay at the bottom of the viewport, even if the message list is short — because the parent column uses `flex: 1` to expand and push it down.
      * **Three Equal-Width Stats in the Sidebar**: Somewhere in the sidebar, include a small "channel info" row with **3 stats** — for example: members count, files count, pinned count. Each must take equal width using `flex: 1`.
      * **Self-Validation**: Resize the browser between 600px and 1400px wide and verify nothing breaks: the sidebar stays a constant width, the conversation header stays split left/right, the message list scrolls instead of pushing the input off-screen, and the profile badge stays glued to the bottom of the sidebar.
