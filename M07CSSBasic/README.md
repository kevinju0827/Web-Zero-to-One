# M07 CSS Basic

## The "Why?"

In the previous section, you learned how to modify colors and fonts directly inside HTML tags using the `style` attribute (this is called Inline Styles). However, imagine you have a webpage with 50 paragraphs, and you want all of them to be blue. If you use the `style` attribute, you'd have to copy and paste the exact same code 50 times! Not only does this bloat your HTML code, but if you later decide to change that blue to green, you will face a maintenance nightmare of updating every single line.

This is where CSS (Cascading Style Sheets) and "Selectors" come into play. By separating the design (CSS) from the content structure (HTML), we can achieve the principle of "write once, apply everywhere." By adding `class` or `id` attributes to our HTML tags, we can precisely tell CSS which designs should be applied to which elements.

## Goals

Understand the concept of separating HTML structure from CSS styling, and grasp basic CSS syntax.  
By the end of this module, you should be able to use the `<style>` tag within an HTML document, and know how to use Element Selectors, Class Selectors, and ID Selectors to change the appearance of your webpage.

## Core Concepts

To separate CSS rules from HTML, we typically add a `<style>` tag inside the `<head>` section of our HTML document. Inside this tag, we use **Selectors** to target elements, and then declare our styling rules within a pair of curly braces `{}`.

### Element Selector

The most basic selector uses the HTML tag name directly. This applies the styling to **all** instances of that specific tag on the page.

```html
<head>
  <style>
    /* This will turn "all" <p> paragraphs on the page gray */
    p {
      color: gray;
      font-size: 16px;
    }
  </style>
</head>
<body>
  <p>First paragraph.</p>
  <p>Second paragraph.</p>
</body>
```

### Identifiers and the ID Selector: `#id`

The id attribute is used to mark a single, unique element on the page.
One important rule is that an id value should only be used once per HTML page.  
This makes it ideal for elements like a navigation bar, a main title, or a specific container.  
In CSS, we use a hashtag (#) to select an id.

```html
<head>
  <style>
    /* Targets the unique element with id="top-banner" */
    #top-banner {
      background-color: lightblue;
      text-align: center;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <p id="top-banner">Summer Sale: 50% Off Everything!</p>
  <p>Check out our latest products below.</p>
</body>
```
### Classes and the Class Selector: `.class`

The `class` attribute is used when you want to apply the same style to **multiple elements**.
Think of a `class` as sticking a label on HTML elements. You can apply the exact same `class` name to many different elements. In CSS, we use a **period (`.`)** to select a class.

Example:
```html
<head>
  <style>
    /* Targets all elements with class="highlight" */
    .highlight {
      color: red;
      font-family: sans-serif;
    }
  </style>
</head>
<body>
  <p class="highlight">This paragraph is important.</p>
  <p>This is a normal paragraph.</p>
  <h2 class="highlight">This heading is also important!</h2>
</body>
```

## Guided Practice

Now, let's use all three selectors to build a realistic **"Tech Blog Article Page"**! This scenario perfectly illustrates *why* CSS Selectors are so powerful: multiple paragraphs share the same base style, specific sections are individually highlighted, and a reusable "tag" style can be applied to various elements at once.

* Step 1: Set Up the HTML Structure
  Create a new HTML file. Inside `<head>`, add a `<style>` tag — this is where all your CSS rules will live. In `<body>`, add the following content blocks in order:
  * A top banner `<div>` with `id="top-banner"`.
  * An `<h1>` for the article title.
  * Three `<p>` tags for article body text.
  * An `<h2>` subheading before the third paragraph.
  * Inside the second and third `<p>`, wrap one keyword each with a `<span>` and give them both `class="highlight"`.
  * Below the article, add a `<div>` with `id="author-box"` containing a small `<p>` describing the author.

* Step 2: Style All Paragraphs with an Element Selector
  Inside `<style>`, write a rule targeting the `p` element. Set `font-family` to `system-ui, sans-serif`, `font-size` to `16px`, `color` to `#374151` (a dark gray), and `line-height` to `1.8`. Notice how this single rule instantly styles **all** your paragraphs — no repetitive `style=""` needed!

* Step 3: Style the Top Banner with an ID Selector
  Use the `#top-banner` selector to style the announcement bar. Set `background-color` to `#1D4ED8` (a strong blue), `color` to `white`, `text-align` to `center`, and `font-weight` to `bold`. Because IDs are unique, this exact style will only ever apply to this one element.

* Step 4: Create a Reusable Highlight Class
  Use the `.highlight` selector to create a reusable inline highlight style. Set `background-color` to `#FEF9C3` (a soft yellow), `color` to `#92400E` (a dark amber), and `font-weight` to `bold`. Apply `class="highlight"` to the `<span>` elements inside your paragraphs. Notice how the same class styles elements in completely different paragraphs consistently.

* Step 5: Style the Author Box with an ID Selector
  Use the `#author-box` selector to make the author section distinct from the main content. Set `background-color` to `#F3F4F6`, add a left border accent with `border-left: 4px solid #1D4ED8`, and give it some breathing room with `padding: 12px 16px`. Because the `p` Element Selector already applies `color: #374151`, the author text inherits that style automatically — showing how Element and ID selectors work *together*.

* Step 6: Style the Subheading
  Target the `h2` element with an Element Selector. Set `color` to `#1D4ED8` to match the banner's blue, creating a cohesive color theme across the page.

## Checkpoints

* [ ] Build an HTML **"Online Store Product Listing"** page using a `<style>` tag (no inline styles allowed).
      The page should display at least **three product cards**, each built with a `<div>`. Each card must contain: a product name (`<h2>`), a short description (`<p>`), and a price (`<p>`).
      Apply the following requirements:
      * Use an **Element Selector** to give all `<p>` tags on the page a consistent `font-family` and `color`.
      * Use a **Class Selector** (e.g., `.product-card`) to give every card the same `background-color`, `border`, and `border-radius`.
      * Mark exactly one product as a featured deal: give that card's `<div>` a unique `id` (e.g., `id="featured"`). Use an **ID Selector** to make it stand out — change its `background-color` to a different accent color and make its `border` more prominent.
      * Apply a **Class Selector** (e.g., `.sale-price`) to the price `<p>` of the featured product to display it in a bold, eye-catching color (e.g., `color: #DC2626`).