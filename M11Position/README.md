# M11 Position

## The "Why?"

By default, every element on a webpage flows from top to bottom and from left to right—the browser places things one after another in the **normal document flow**. This works well for paragraphs of text, but it falls apart the moment you want to build a modern interface.

How does a navigation bar stay at the top while the user scrolls?
How does a "New" badge sit perfectly on the corner of an avatar?
How does a chat button float in the bottom-right corner of the screen?

The CSS `position` property is the answer to all of these. It lets you break out of the normal flow and place elements **exactly where you want them**—relative to themselves, relative to a parent, or even relative to the entire browser viewport. Position is the foundation of every layered, interactive UI you see on the modern web.

## Goals

Understand how the `position` property changes the way elements are placed on a page.  
By the end of this module, you should be able to clearly distinguish between `static`, `relative`, `absolute`, `fixed`, and `sticky`, combine them with the offset properties (`top`, `right`, `bottom`, `left`), and use `z-index` to manage how overlapping elements stack on top of each other.

## Core Concepts

### The `position` Property

The `position` property controls how an element participates in the document flow and what its offset properties refer to. There are five values you need to know.

1. **`static` (Default)**  
   The element follows the normal document flow. This is what every element starts as. The offset properties (`top`, `right`, `bottom`, `left`) and `z-index` have **no effect** on a `static` element.

2. **`relative`**  
   The element stays in the normal flow (it still occupies its original space), but you can now "nudge" it from its original position using the offset properties. Neighbors do **not** shift to fill the gap it leaves behind.  
   `relative` is most commonly used to set up a **reference point** for absolutely-positioned children.

3. **`absolute`**  
   The element is **removed from the normal flow**—neighbors collapse together as if it never existed. It is then positioned relative to its **nearest positioned ancestor** (any ancestor whose `position` is not `static`). If no such ancestor exists, it positions relative to the entire page (`<html>`).

4. **`fixed`**  
   The element is removed from the normal flow and positioned relative to the **browser viewport** (the visible part of the screen). It stays in the same place even when the user scrolls. Perfect for floating buttons, cookie banners, and chat widgets.

5. **`sticky`**  
   A hybrid of `relative` and `fixed`. The element behaves like `relative` until the user scrolls past a defined threshold (e.g. `top: 0`), at which point it "sticks" to that position like `fixed`. Once its parent container scrolls out of view, it scrolls away with it.

### The Offset Properties

`top`, `right`, `bottom`, and `left` tell the browser how far to push an element away from the edges of its reference. They only take effect when `position` is **not** `static`.

```css
.box {
  position: absolute;
  top: 10px;     /* 10px down from the top edge of the reference */
  right: 20px;   /* 20px in from the right edge of the reference */
}
```

### Stacking with `z-index`

Once elements start overlapping, you need a way to control which one appears on top. The `z-index` property does exactly that.

* A higher `z-index` value means the element stacks **in front of** elements with lower values.
* `z-index` only works on elements whose `position` is not `static`.
* Think of the screen as having a depth axis pointing toward you—`z-index` slides elements forward or backward along that axis.

```css
.modal      { position: fixed;  z-index: 1000; } /* on top */
.tooltip    { position: absolute; z-index: 500; }
.background { position: relative; z-index: 1; }   /* behind */
```

## Guided Practice

In this practice, we will build a fragment of a **music streaming app called "Soundwave"** (think Spotify or Apple Music). It is the perfect playground for `position` because the interface naturally layers things on top of each other: a navigation bar that follows you as you scroll, album covers with hanging "NEW" tags and play buttons sitting on top of the artwork, and a persistent "Now Playing" bar at the bottom of the screen. See `music_player_example.html` in this folder for the finished result.

* Step 1: Set Up the Dark Canvas

  Music apps almost always use a dark theme. Start with that mood, and give the page enough height to actually demonstrate scrolling.
  * Create an HTML file and add a `<style>` tag inside the `<head>`.
  * Add the following CSS:
  ```css
  * { box-sizing: border-box; }
  body {
    font-family: 'Segoe UI', system-ui, sans-serif;
    margin: 0;
    background: #0f172a;
    color: #f1f5f9;
    min-height: 200vh;        /* tall enough to scroll */
    padding-bottom: 110px;    /* leave room for the fixed Now Playing bar */
  }
  main { max-width: 1200px; margin: 0 auto; padding: 2rem; }
  ```
    * Add this skeleton HTML to your `<body>`. You will fill each section in the steps below.
  ```html
  <nav class="top-nav"><!-- Step 2 --></nav>
  <main><!-- Steps 3–5 --></main>
  <div class="now-playing"><!-- Step 5 --></div>
  ```

* Step 2: Build the Sticky Top Navigation

  Streaming apps keep their navigation pinned to the top so users always have one click to Home, Discover, or their Library. `position: sticky` is purpose-built for this. We will also add a gradient logo and a circular avatar using CSS `linear-gradient`.
  * Add the following CSS:
  ```css
  .top-nav {
    position: sticky;
    top: 0;
    padding: 1rem 2rem;
    background: rgba(15, 23, 42, 0.92);
    backdrop-filter: blur(10px);
    border-bottom: 1px solid #1e293b;
    z-index: 100;
    overflow: hidden;        /* Clearfix to contain floated children */
  }
  .logo {
    float: left;
    font-size: 1.4rem;
    font-weight: 800;
    background: linear-gradient(135deg, #a78bfa, #ec4899);
    -webkit-background-clip: text;
    background-clip: text;
    color: transparent;
    line-height: 36px;       /* Match avatar height for vertical centering */
  }
  .nav-links {
    float: right;
    line-height: 36px;
    margin-right: 1.75rem;
  }
  .nav-links a {
    color: #cbd5e1;
    text-decoration: none;
    font-weight: 500;
    margin-left: 1.75rem;    /* Add spacing between navigation links */
  }
  .nav-links a:hover { color: #f1f5f9; }
  .avatar {
    float: right;
    width: 36px; height: 36px;
    border-radius: 50%;
    background: linear-gradient(135deg, #a78bfa, #ec4899);
    border: 2px solid #f1f5f9;
  }
  ```
  * Replace the `<nav>` placeholder with the following HTML:
  ```html
  <nav class="top-nav">
    <div class="logo">♫ Soundwave</div>
    <div class="nav-links">
      <a href="#">Home</a>
      <a href="#">Discover</a>
      <a href="#">Library</a>
    </div>
    <div class="avatar" title="Profile"></div>
  </nav>
  ```
  * **Observation:** Scroll the page. The nav stays glued to the top — but unlike `fixed`, it still reserves its original space in the document flow when at rest. That's the trademark behavior of `sticky`. Also notice `color: transparent` combined with `background-clip: text` — this technique clips the gradient fill to the text shape itself instead of the element's box.

* Step 3: Add the Section Header and the `relative` HOT Tag

  Before we build the album cards, we need a section header row with a title on the left and a "See all" link on the right. This step also introduces `position: relative` in its purest form: nudging an inline element from its own baseline without disturbing its neighbours.
    * Add the following CSS:
  ```css
  .section-header {
    overflow: hidden;        /* Clearfix */
    margin: 0 0 1.5rem;
  }
  .section-header h1,
  .section-header h2 {
    float: left;
    margin: 0;
  }
  .section-header a {
    float: right;
    color: #a78bfa;
    text-decoration: none;
    font-size: 0.9rem;
    margin-top: 0.6rem;      /* Baseline alignment tweak */
  }
  /* relative nudge — lifts the badge slightly above the heading baseline */
  .hot-tag {
    position: relative;
    top: -4px;               /* Shift slightly upwards */
    display: inline-block;
    background: #f59e0b;
    color: #1e293b;
    padding: 0 8px;
    line-height: 18px;
    border-radius: 10px;
    font-size: 0.7rem;
    font-weight: 800;
    margin-left: 0.5rem;
    letter-spacing: 0.05em;
  }
  ```
  * Add the following HTML at the start of `<main>`:
  ```html
  <div class="section-header">
    <h1>New Releases <span class="hot-tag">HOT</span></h1>
    <a href="#">See all →</a>
  </div>
  <div class="album-grid">
    <!-- album cards go here in Step 4 -->
  </div>
  ```
    * **Observation:** The `.hot-tag` uses `position: relative` with `top: -4px` to float the pill slightly above the heading text. Its original space in the flow is **not** reclaimed — the heading's line height is unchanged. This is the key difference between a `relative` nudge and an `absolute` extraction: `relative` shifts the visual without disturbing neighbours.

* Step 4: Build the Album Card Grid (the `relative` + `absolute` pattern)

  This is the workhorse of every modern UI: a `relative` parent that anchors several `absolute` children. We will attach three absolutely-positioned elements to each album cover — a "NEW" badge, an optional "EXPLICIT" label, and a green play button that fades in on hover. We will also add six distinct cover gradients and a hover lift effect on the card itself.
  * Add the following CSS:
  ```css
  .album-grid {
    margin-right: -1.5rem;   /* Offset the right margin of the last card */
  }
  .album-card {
    display: inline-block;   /* Set layout inline to allow side-by-side positioning */
    vertical-align: top;     /* Ensure top alignment for all cards */
    width: 220px;
    background: #1e293b;
    border-radius: 12px;
    padding: 1rem;
    margin-right: 1.2rem;
    margin-bottom: 1.5rem;
    transition: transform 0.2s, background 0.2s;
  }
  .album-card:hover { background: #334155; transform: translateY(-4px); }

  .album-cover {
    position: relative;       /* Anchor for absolute badges / buttons */
    width: 100%;
    height: 188px;            /* 220px card - 32px padding = 188px */
    border-radius: 8px;
    margin-bottom: 1rem;
    text-align: center;       /* Center emoji horizontally */
    line-height: 188px;       /* Center emoji vertically */
    font-size: 3rem;
    color: rgba(255, 255, 255, 0.85);
    overflow: hidden;
  }
  /* Six cover colour themes */
  .cover-1 { background: linear-gradient(135deg, #6366f1, #ec4899); }
  .cover-2 { background: linear-gradient(135deg, #f59e0b, #ef4444); }
  .cover-3 { background: linear-gradient(135deg, #10b981, #06b6d4); }
  .cover-4 { background: linear-gradient(135deg, #8b5cf6, #3b82f6); }
  .cover-5 { background: linear-gradient(135deg, #ec4899, #f43f5e); }
  .cover-6 { background: linear-gradient(135deg, #14b8a6, #6366f1); }

  /* NEW badge — hangs outside the top-left corner */
  .new-badge {
    position: absolute;
    top: -8px; left: -8px;
    background: #ef4444;
    color: white;
    padding: 0 10px;
    line-height: 22px;        /* Match height to ensure centering */
    border-radius: 4px;
    font-size: 0.7rem;
    font-weight: 800;
    letter-spacing: 0.05em;
    box-shadow: 0 4px 10px rgba(239, 68, 68, 0.4);
    z-index: 2;
  }
  /* EXPLICIT pill — inside the top-right corner */
  .explicit-tag {
    position: absolute;
    top: 8px; right: 8px;
    background: rgba(0, 0, 0, 0.6);
    color: #f1f5f9;
    padding: 0 8px;
    line-height: 18px;
    border-radius: 3px;
    font-size: 0.65rem;
    font-weight: 700;
    letter-spacing: 0.05em;
    z-index: 2;
  }
  /* Play FAB — hidden by default, revealed on card hover */
  .play-fab {
    position: absolute;
    bottom: 10px; right: 10px;
    width: 44px; height: 44px;
    border-radius: 50%;
    background: #22c55e;
    color: white;
    text-align: center;       /* Center play icon horizontally */
    line-height: 44px;        /* Center play icon vertically */
    font-size: 1.1rem;
    cursor: pointer;
    box-shadow: 0 6px 14px rgba(34, 197, 94, 0.4);
    opacity: 0;
    transform: translateY(8px);
    transition: opacity 0.2s, transform 0.2s;
    z-index: 2;
  }
  .album-card:hover .play-fab { opacity: 1; transform: translateY(0); }

  .album-title  { margin: 0; font-weight: 700; font-size: 1rem; }
  .album-artist { margin: 0.25rem 0 0; color: #94a3b8; font-size: 0.9rem; }
  ```
    * Replace the `album-grid` placeholder from Step 3 with the following HTML, then add a second section below it:
  ```html
  <!-- New Releases grid -->
  <div class="album-grid">
    <div class="album-card">
      <div class="album-cover cover-1">
        🎵
        <span class="new-badge">NEW</span>
        <span class="explicit-tag">EXPLICIT</span>
        <div class="play-fab">▶</div>
      </div>
      <p class="album-title">Midnight Echoes</p>
      <p class="album-artist">Luna Vega</p>
    </div>
    <div class="album-card">
      <div class="album-cover cover-2">
        🔥
        <span class="new-badge">NEW</span>
        <div class="play-fab">▶</div>
      </div>
      <p class="album-title">Solar Drift</p>
      <p class="album-artist">Atlas Reign</p>
    </div>
    <div class="album-card">
      <div class="album-cover cover-3">
        🌊
        <span class="new-badge">NEW</span>
        <div class="play-fab">▶</div>
      </div>
      <p class="album-title">Tidewater Hymns</p>
      <p class="album-artist">Marina Cove</p>
    </div>
    <div class="album-card">
      <div class="album-cover cover-4">
        ✨
        <span class="new-badge">NEW</span>
        <span class="explicit-tag">EXPLICIT</span>
        <div class="play-fab">▶</div>
      </div>
      <p class="album-title">Neon Cathedral</p>
      <p class="album-artist">VOIDLINE</p>
    </div>
  </div>

  <!-- Recommended section -->
  <div class="section-header" style="margin-top: 3.5rem;">
    <h2>Recommended for you</h2>
    <a href="#">See all →</a>
  </div>
  <div class="album-grid">
    <div class="album-card">
      <div class="album-cover cover-5">
        🎧
        <div class="play-fab">▶</div>
      </div>
      <p class="album-title">Focus Flow</p>
      <p class="album-artist">Deep work playlist</p>
    </div>
    <div class="album-card">
      <div class="album-cover cover-6">
        💜
        <div class="play-fab">▶</div>
      </div>
      <p class="album-title">Throwback Vibes</p>
      <p class="album-artist">2010s favorites</p>
    </div>
  </div>
  ```
  * **Observation:** Three children — `.new-badge`, `.explicit-tag`, and `.play-fab` — are all anchored to three different corners of the same `.album-cover` parent using `top` / `right` / `bottom` / `left`. Try temporarily removing `position: relative` from `.album-cover`: every badge jumps to the corner of the entire page, because `absolute` falls back to the nearest positioned ancestor, which in this case becomes `<html>`. Also notice that `.play-fab` starts with `opacity: 0` and `transform: translateY(8px)` — it is still in the stacking context and occupies space, but is invisible until the parent card receives `:hover`.

* Step 5: Add the Fixed "Now Playing" Bar

  Spotify, Apple Music, YouTube Music — every streaming app puts a persistent player at the bottom of the screen so the music doesn't stop when you change pages. `position: fixed` is the right tool: it ignores the document flow entirely and anchors to the **viewport**. Note the highlighted play button, which gets a distinctive green background to stand out from the other controls.
  * Add the following CSS:
  ```css
  .now-playing {
    position: fixed;
    bottom: 0; left: 0; right: 0;
    padding: 0.75rem 1.5rem;
    background: #1e1b4b;
    border-top: 1px solid #312e81;
    z-index: 200;            /* must sit above the sticky nav */
    overflow: hidden;        /* Clearfix for floated elements */
  }
  .now-playing .thumb {
    float: left;
    width: 48px; height: 48px;
    border-radius: 6px;
    background: linear-gradient(135deg, #6366f1, #ec4899);
  }
  .now-playing .info {
    float: left;
    margin-left: 1rem;
    padding-top: 4px;        /* Vertically align text */
  }
  .now-playing .info strong { display: block; }
  .now-playing .info span { color: #94a3b8; font-size: 0.85rem; }
  .controls {
    float: right;
    padding-top: 6px;
  }
  .controls button {
    float: left;
    margin-left: 0.5rem;
    width: 36px; height: 36px;
    border-radius: 50%;
    border: none;
    background: #312e81;
    color: white;
    font-size: 0.9rem;
    cursor: pointer;
    text-align: center;
    line-height: 36px;       /* Center button icons vertically */
  }
  .controls button:hover { background: #4338ca; }
  .controls button.play { background: #22c55e; } /* highlighted play/pause */
  ```
    * Replace the `<div class="now-playing">` placeholder with:
  ```html
  <div class="now-playing">
    <div class="thumb"></div>
    <div class="info">
      <strong>Midnight Echoes</strong>
      <span>Luna Vega · 3:42 / 4:18</span>
    </div>
    <div class="controls">
      <button>⏮</button>
      <button class="play">⏸</button>
      <button>⏭</button>
    </div>
  </div>
  ```
  * **Observation:** Scroll all the way down. The sticky nav scrolls *with* the page once the viewport passes its natural position (because it is still inside the flow), but the Now Playing bar stays welded to the bottom of the viewport no matter what. That is the core difference between `sticky` (anchors relative to its scroll container) and `fixed` (anchors relative to the screen). Also notice `z-index: 200` on `.now-playing` — higher than the nav's `z-index: 100` — so the player always sits in front even if the two elements overlap at certain viewport heights.

* Step 6: Demonstrate `z-index` Stacking

  We now have three "layers" competing for the foreground: the sticky nav, the fixed player bar, and any future modals or tooltips. This step makes the stacking order tangible by adding a visual demo of three overlapping absolutely-positioned cards inside a `position: relative` container.
  * Add the following CSS:
  ```css
  /* z-index demo */
  .stack-demo { position: relative; height: 160px; margin-top: 1rem; }
  .stack-card {
    position: absolute;
    width: 200px; height: 120px;
    padding: 1rem;
    border-radius: 8px;
    color: white;
    font-weight: 700;
  }
  .stack-back   { top: 0;    left: 0;    background: #6366f1; z-index: 1; }
  .stack-middle { top: 20px; left: 80px; background: #ec4899; z-index: 2; }
  .stack-front  { top: 40px; left: 160px; background: #22c55e; z-index: 3; }
  ```
    * Add the following HTML at the bottom of `<main>`, after the Recommended section:
  ```html
  <div class="section-header" style="margin-top: 3.5rem;">
    <h2>z-index in action</h2>
  </div>
  <p style="color:#94a3b8;">
    Three absolutely-positioned cards overlapping.
    The highest <code>z-index</code> wins the front row.
  </p>
  <div class="stack-demo">
    <div class="stack-card stack-back">z-index: 1</div>
    <div class="stack-card stack-middle">z-index: 2</div>
    <div class="stack-card stack-front">z-index: 3</div>
  </div>

  <p style="color:#94a3b8; margin-top:6rem;">
    Keep scrolling — the navigation stays glued to the top,
    and the Now Playing bar stays glued to the bottom no matter how far you go.
  </p>
  ```
    * Confirm the three `z-index` tiers already in your CSS form a consistent hierarchy:
  ```css
  /* page content / cards — no explicit z-index needed (auto) */
  .top-nav     { z-index: 100; }  /* above page content */
  .now-playing { z-index: 200; }  /* above the nav */
  /* future modals would use z-index: 1000+ */
  ```
  * **Observation:** Open Chrome DevTools (F12), inspect `.top-nav`, and change its `z-index` to `1` in the Styles panel. Scroll until an album card overlaps the nav — the card now hides the nav bar. Restore the value and the nav returns to the foreground. Repeat the experiment on `.stack-back`: increase its `z-index` above `3` and watch it jump in front of `.stack-front`. Defining sensible `z-index` tiers early — nav: 100, player: 200, modal: 1000 — is what keeps real-world UIs from randomly hiding the wrong layer.

## Checkpoints

* [ ] Build an "Online Course Player" Page  
  Imagine you're building a Udemy- or Coursera-style course screen. The user is watching a video lesson, with the course outline next to it, related lessons below, and a few persistent UI elements anchored to the screen. Create a single HTML file (with a `<style>` tag) that satisfies every requirement below using only `position`, the offset properties, and `z-index`:
  * **Sticky Course Header**: A top bar showing the course title and the user's progress (e.g. "Lesson 4 of 12") that stays pinned at the top of the viewport while the lesson list scrolls beneath it.
  * **Lesson Thumbnail with Layered Badges**: Build at least three lesson cards in the page body. Each card has a thumbnail (`position: relative`) with the following children:
  * A **duration badge** (e.g. "12:34") in the bottom-right corner using `position: absolute`.
  * A status badge in the top-left corner — either "NEW", "COMPLETED" ✓, or "IN PROGRESS" — using `position: absolute` and a negative `top` / `left` offset so it visibly hangs over the corner of the thumbnail.
  * A semi-transparent **▶ play button** centered over the thumbnail using `position: absolute` with `top: 50%; left: 50%; transform: translate(-50%, -50%);`.
  * **Floating "Ask a Question" Button**: A round button anchored to the bottom-right of the screen with `position: fixed`. It must remain visible at the same screen coordinates no matter how far the user scrolls.
  * **Fixed "Back to Top" Arrow**: A second `fixed` button above or beside the question button (also bottom-right), so you have at least two fixed elements that don't overlap each other.
  * **Stacking Tiers**: Define three explicit `z-index` tiers in your CSS — for example `--z-nav: 100`, `--z-floating: 200`, `--z-modal: 1000` — and apply them so the sticky header always sits above the page content, and the fixed buttons always sit above the sticky header.
  * **Self-Validation**: Open Chrome DevTools, inspect each positioned element, and confirm in the "Computed" panel that the `position`, the offset values, and the `z-index` you set are actually being applied. Scroll the entire page top-to-bottom and verify that no badge, button, or sticky element ever ends up behind something it shouldn't.