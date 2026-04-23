# M08 Block and Inline

## The "Why?"

In the previous module, we learned how to use selectors in a `<style>` tag to separate design from HTML structure. As you start applying these styles and adding more elements to your webpage, you will likely notice a distinct pattern: some elements naturally stack on top of each other like a tower of bricks, while others happily sit side-by-side on the same line.

If you want to build modern, aesthetic websites, understanding *why* elements behave this way is non-negotiable. This behavior is dictated by the browser's normal document flow. By mastering the concepts of "block" and "inline," you take control of your page layout, transforming a vertical list of content into a beautifully structured interface.

## Goals

Understand the fundamental differences between Block-level and Inline-level elements.  
By the end of this module, you should be able to identify common block and inline tags, and confidently use the CSS `display` property to manipulate their default behaviors to suit your layout needs.

## Core Concepts

HTML elements generally fall into two main display categories right out of the box: **Block** and **Inline**.

### Block-level Elements

A block-level element always starts on a new line and takes up the full width available (stretching from the far left edge to the far right edge of its parent container). Think of them as heavy boxes that demand their own entire row.

* Common examples: `<p>`, `<h1>` through `<h6>`, `<ul>`, `<li>`.
* Characteristics: Because they act as physical boxes, you can freely set their `width` and `height` properties in CSS.

```html
<p style="background-color: lightblue;">
  I am a block! I take up the whole width, even if my text is short.
</p>
<p style="background-color: lightcoral; width: 500px">
  I am forced onto a new line!
</p>
```

### Inline-level Elements

An inline element does not start on a new line. It only takes up as much width as absolutely necessary to wrap its content. Think of them as words in a sentence; they simply flow next to each other.

* Common examples: `<a>`, `<strong>`, `<i>`.
* Characteristics: You **cannot** set their `width` or `height` properties. They completely ignore those CSS rules because their dimensions are dictated entirely by the text inside them.

> **Exception: The `<img>` Tag**: While technically an inline element, `<img>` is unique because it is "replaced content." This means it **does** have an intrinsic width and height, and you **can** set its width and height in CSS, unlike other inline elements.

```html
<i style="background-color: yellow;">I am inline.</i>
<i style="background-color: lightgreen;">I sit right next to my neighbor!</i>
```

### The `display` Property

What if you want a link (`<a>`) to look and function like a large, clickable block button? Or what if you want two `<div>` containers to sit side-by-side to create a two-column layout? You can override their default browser behavior using the CSS `display` property.

1. `display: block;` Forces an element to behave like a block (taking up the full row and accepting width/height).
2. `display: inline;` Forces an element to behave like inline text (shrinking to its content and sitting side-by-side).
3. `display: inline-block;` The best of both worlds! The element sits side-by-side with others (like inline), but it respects the `width` and `height` properties you set in CSS (like a block). This is incredibly useful for creating grid-like layouts, image galleries, or navigation buttons.
4. `display: none;` Completely hides the element from the page. It will look and act as if the element doesn't exist in the HTML at all, freeing up the space it previously occupied.

Here is a step-by-step English Guided Practice designed to teach the `display` property, structured similarly to your course material and focusing on practical scenarios without relying on the Box Model, `<div>`, or `<span>`.

## Guided Practice

Now, let's use the `display` property to build a **"Modern Web Startup Layout"**! This scenario perfectly illustrates why we need to change default behaviors: we will turn a vertical list into a horizontal navigation bar, transform a simple text link into a clickable pill-shaped button, and see how inline text flows naturally.

* Step 1: Set Up the HTML Structure
  Create a new HTML file. To separate CSS rules from HTML, add a `<style>` tag inside the `<head>` section of your HTML document. In the `<body>`, add the following content:
  * A `<ul>` containing three `<li>` tags. Inside each `<li>`, put an `<a>` tag (e.g., "Products", "Solutions", "Pricing") to act as our site navigation.
  * An `<img>` with `src="logo.svg"` and `width="500"`.
  * An `<h1>` for the page title (e.g., "Build the Future with Us").
  * A `<p>` for a welcome message. Inside this paragraph, wrap a key phrase (like "innovative platform") in a `<strong>` tag with `class="highlight"`.
  * At the bottom, add a standalone `<a>` tag with `class="action-btn"` that says "Get Started for Free".
  * Finally, add one more `<p>` with `id="secret"` that says "Special discount code: MYCOUPON".

* Step 2: Create a Horizontal Navigation Menu (Block to Inline-Block)
  By default, `<li>` tags are block elements, which means your navigation links are stacking vertically on top of each other. Let's fix this!
  Inside your `<style>` tag, target the `li` element. Set `display: inline-block`. This forces the list items to sit side-by-side on the same line, creating a classic horizontal menu. To make them look modern and airy, add `line-height: 4` to create generous vertical space.

* Step 3: Transform a Link into a Modern Button (Inline to Inline-Block)
  Look at your "Get Started for Free" link. By default, `<a>` tags are inline elements, meaning they just look like regular text. We want it to look like a massive, clickable button!
  Target the `.action-btn` class selector. Change its behavior by setting `display: inline-block`. Now, you can give it a solid structure: set `background-color` to a sleek dark blue (`#0f172a`), `color` to `white`, and use `line-height: 3` to create vertical space above and below the text. Add `border-radius: 50px;` to give it a modern "pill" shape.

* Step 4: Decorate Text without Breaking the Line (Maintaining Inline)
  Target the `.highlight` class selector. Set `background-color: #dbeafe` (a soft pastel blue) and `color: #1d4ed8`. Notice how the background only covers the specific words and does *not* force the rest of the sentence to a new line. This is the natural power of `display: inline`!

* Step 5: Make Elements Disappear (Any to None)
  Sometimes you want content to exist in the HTML but remain invisible to the user until a specific action occurs.
  Target the unique element with the `#secret` ID selector. Set `display: none`. Refresh your page, and watch the paragraph completely vanish from the layout as if it never existed!

## Checkpoints

* [ ] Build a "Team Member Profile" Section
  Write an HTML webpage containing a `<style>` tag to implement a modern employee or user profile card. Please complete the following requirements:
  * Skill Tags: Use a `<ul>` and `<li>` tags to create three professional skill tags for the member (e.g., "HTML", "CSS", "JavaScript"). Since `<li>` tags are block elements by default and stack vertically, use `display: inline-block;` to force them to sit side-by-side on the same line. Set a fixed width and background color for each tag.
  * Inline Status Highlighting: Within a `<p>` tag containing a short biography, use an `<i>` or `<strong>` tag to wrap the member's current status (e.g., "Open to work" or "Online"). Give this status text a prominent background color, and verify that this inline element does *not* force the rest of the sentence to a new line.
  * Contact Button: Add an `<a>` tag at the bottom of the card to act as a "Send Message" link. Because `<a>` tags are inline elements by default and just look like regular text, use `display: inline-block;` to change its behavior. This will allow you to apply `line-height`, `width`, and a background color to transform it into a solid, clickable button.
