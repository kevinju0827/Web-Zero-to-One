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

In this practice, we will build a fragment of a **music streaming app called "Soundwave"** (think Spotify or Apple Music). It is the perfect playground for `position` because the interface naturally layers things on top of each other: a navigation bar that follows you as you scroll, album covers with hanging "NEW" tags and play buttons sitting on top of the artwork, and a persistent "Now Playing" bar at the bottom of the screen. See `music_player.html` in this folder for the finished result.

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

* Step 2: Build the Sticky Top Navigation

  Streaming apps keep their navigation pinned to the top so users always have one click to Home, Discover, or their Library. `position: sticky` is purpose-built for this.
  * Add the following CSS:
  ```css
  .top-nav {
    position: sticky;
    top: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
    background: rgba(15, 23, 42, 0.92);
    backdrop-filter: blur(10px);
    border-bottom: 1px solid #1e293b;
    z-index: 100;
  }
  .logo { font-size: 1.4rem; font-weight: 800; color: #a78bfa; }
  .nav-links { display: flex; gap: 1.75rem; }
  .nav-links a { color: #cbd5e1; text-decoration: none; }
  .avatar {
    width: 36px; height: 36px;
    border-radius: 50%;
    background: linear-gradient(135deg, #a78bfa, #ec4899);
  }
  ```
  * Add the following HTML inside `<body>`:
  ```html
  <nav class="top-nav">
    <div class="logo">♫ Soundwave</div>
    <div class="nav-links">
      <a href="#">Home</a>
      <a href="#">Discover</a>
      <a href="#">Library</a>
    </div>
    <div class="avatar"></div>
  </nav>

  <main>
    <h1>New This Week</h1>
  </main>
  ```
  * **Observation:** Scroll the page. The nav stays glued to the top — but unlike `fixed`, it still reserves its original space in the document flow when at rest. That's the trademark behavior of `sticky`.

* Step 3: Build the Album Card (the relative + absolute pattern)

  This is the workhorse of every modern UI: a `relative` parent that anchors several `absolute` children. We're going to attach **three** different absolutely-positioned things to one album cover — a "NEW" tag, an "EXPLICIT" badge, and a green play button.
  * Add the following CSS:
  ```css
  .album-card {
    background: #1e293b;
    border-radius: 12px;
    padding: 1rem;
    width: 220px;
  }

  .album-cover {
    position: relative;        /* anchor for all the badges */
    aspect-ratio: 1 / 1;
    border-radius: 8px;
    margin-bottom: 1rem;
    background: linear-gradient(135deg, #6366f1, #ec4899);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 3rem;
  }

  /* Hanging NEW tag — sticks out of the top-left corner */
  .new-badge {
    position: absolute;
    top: -8px;
    left: -8px;
    background: #ef4444;
    color: white;
    padding: 4px 10px;
    border-radius: 4px;
    font-size: 0.7rem;
    font-weight: 800;
    box-shadow: 0 4px 10px rgba(239, 68, 68, 0.4);
  }

  /* EXPLICIT pill — inside the top-right corner */
  .explicit-tag {
    position: absolute;
    top: 8px;
    right: 8px;
    background: rgba(0, 0, 0, 0.6);
    color: #f1f5f9;
    padding: 2px 8px;
    border-radius: 3px;
    font-size: 0.65rem;
    font-weight: 700;
  }

  /* Floating play button — bottom-right of the cover */
  .play-fab {
    position: absolute;
    bottom: 10px;
    right: 10px;
    width: 44px; height: 44px;
    border-radius: 50%;
    background: #22c55e;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 6px 14px rgba(34, 197, 94, 0.4);
    cursor: pointer;
  }

  .album-title  { margin: 0; font-weight: 700; }
  .album-artist { margin: 0.25rem 0 0; color: #94a3b8; font-size: 0.9rem; }
  ```
  * Add the following HTML inside `<main>`:
  ```html
  <div class="album-card">
    <div class="album-cover">
      🎵
      <span class="new-badge">NEW</span>
      <span class="explicit-tag">EXPLICIT</span>
      <div class="play-fab">▶</div>
    </div>
    <p class="album-title">Midnight Echoes</p>
    <p class="album-artist">Luna Vega</p>
  </div>
  ```
  * **Observation:** Three different child elements are anchored to three different corners of the same parent — purely with `top` / `right` / `bottom` / `left`. Try removing `position: relative` from `.album-cover`. Every badge will jump to the corner of the entire page, because `absolute` falls back to the `<html>` element when no positioned ancestor exists.

* Step 4: Add the Fixed "Now Playing" Bar

  Spotify, Apple Music, YouTube Music — every streaming app puts a persistent player at the bottom of the screen so the music doesn't disappear when you change pages. `position: fixed` is exactly the right tool: it ignores its parent entirely and anchors to the viewport.
  * Add the following CSS:
  ```css
  .now-playing {
    position: fixed;
    bottom: 0; left: 0; right: 0;
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 0.75rem 1.5rem;
    background: #1e1b4b;
    border-top: 1px solid #312e81;
    z-index: 200;          /* must sit above the sticky nav */
  }
  .now-playing .thumb {
    width: 48px; height: 48px;
    border-radius: 6px;
    background: linear-gradient(135deg, #6366f1, #ec4899);
  }
  .now-playing .info { flex: 1; }
  .now-playing .info strong { display: block; }
  .now-playing .info span { color: #94a3b8; font-size: 0.85rem; }
  .controls { display: flex; gap: 0.5rem; }
  .controls button {
    width: 36px; height: 36px;
    border-radius: 50%;
    border: none;
    background: #312e81;
    color: white;
    cursor: pointer;
  }
  ```
  * Add the following HTML at the **end** of `<body>` (note: the position in the markup doesn't matter — `fixed` ignores the flow):
  ```html
  <div class="now-playing">
    <div class="thumb"></div>
    <div class="info">
      <strong>Midnight Echoes</strong>
      <span>Luna Vega · 3:42 / 4:18</span>
    </div>
    <div class="controls">
      <button>⏮</button>
      <button>⏸</button>
      <button>⏭</button>
    </div>
  </div>
  ```
  * **Observation:** Scroll all the way down. The sticky nav scrolls *with* the page once you exit the page top (because it's inside the flow), but the Now Playing bar stays welded to the bottom of the viewport. That's the difference between `sticky` (relative to its parent) and `fixed` (relative to the screen).

* Step 5: Manage Stacking with `z-index`

  We now have three "layered" elements all wanting to sit on top of the page content: the sticky nav, the fixed player bar, and (eventually) modal dialogs or tooltips. Without explicit `z-index` values, they would stack in document order — and one wrong scroll could hide the player behind a card.
  * Confirm the layering rules already in your CSS:
  ```css
  .top-nav      { z-index: 100; }   /* above page content */
  .now-playing  { z-index: 200; }   /* above the nav */
  /* future modals would use z-index: 1000+ */
  ```
  * **Observation:** Open Chrome's DevTools (F12), inspect `.top-nav`, and toggle its `z-index` to `1` in the Styles panel. Scroll until a tall album cover overlaps the nav — the cover now hides the nav. Restore the value and the nav comes back to the top of the stack. Picking sensible `z-index` "tiers" early (e.g. `nav: 100`, `player: 200`, `modal: 1000`) is what keeps real-world UIs from breaking.

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
