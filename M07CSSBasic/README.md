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

### Spacing and Layout Basics

Since we haven't officially covered the "Box Model" (which includes Margin and Padding) yet, we can use a few clever properties to make our text more readable and organized:

*   **`line-height`**: Controls the vertical space between lines of text. A value like `1.8` makes the text feel more "airy" and much easier to read. For a single line of text (like a banner), a large `line-height` (e.g., `3`) acts like vertical padding!
*   **`margin: 0`**: Although we'll cover the full "Box Model" later, setting `margin: 0` on the `body` tag is a common "reset" that removes the default white gap around the edges of the screen.
*   **`text-align`**: Used to align text to the `left`, `right`, or `center`.
*   **`border-bottom` / `border-left`**: Can be used to create visual separation between sections without needing extra spacing.

Example:
```css
p {
  line-height: 1.8;
  border-left: 4px solid blue;
}

#banner {
  text-align: center;
  line-height: 3; /* Creates vertical space above and below the text */
}
```

## Guided Practice

Now, let's use all three selectors to build a realistic **"Tech Blog Article Page"**! This scenario perfectly illustrates *why* CSS Selectors are so powerful: multiple paragraphs share the same base style, specific sections are individually highlighted, and a reusable "tag" style can be applied to various elements at once.

* Step 1: Set Up the HTML Structure
  Create a new HTML file. Inside `<head>`, add a `<style>` tag. In `<body>`, add the following content blocks:
  * A top banner `<div>` with `id="top-banner"`.
  * A `<div>` with `class="container"` to hold the main content.
  * Inside the container: an `<h1>` for the title, several `<p>` tags for text, and an `<h2>` subheading.
  * Use `<span>` with `class="highlight"` for important keywords.
  * At the bottom, add a `<div>` with `id="author-box"`.

* Step 2: Style the Layout and All Paragraphs
  First, set `body { text-align: center; margin: 0; }`. This removes the default screen border and centers your content without needing complex layout rules. Then, target the `.container` element: set `max-width: 800px`, `display: inline-block`, and `text-align: left`. Finally, target the `p` element: set `font-family` to `sans-serif`, `font-size` to `18px`, `color` to `#374151`, and `line-height` to `1.8`.

* Step 3: Style the Top Banner with an ID Selector
  Use the `#top-banner` selector. Set `background-color` to `#1D4ED8`, `color` to `white`, and `text-align` to `center`. To give it some "breathing room" without using padding, set `line-height` to `3`.

* Step 4: Create a Reusable Highlight Class
  Use the `.highlight` selector. Set `background-color` to `#FEF9C3` and `color` to `#92400E`. This same style can be applied to any element across your page just by adding the class.

* Step 5: Style the Author Box and Headings
  Target `#author-box` and set a light `background-color: #F3F4F6` and a `border-left: 4px solid #1D4ED8`. For the `h1`, add a `border-bottom: 2px solid #E5E7EB`. Finally, style the `h2` with `color: #1D4ED8`. Notice how these simple borders and colors help organize the page visually.

## Checkpoints

* [ ] Build an HTML **"Online Store Product Listing"** page using a `<style>` tag (no inline styles allowed).
      The page should display at least **three product cards**, each built with a `<div>`. Each card must contain: a product name (`<h2>`), a short description (`<p>`), and a price (`<p>`).
      Apply the following requirements:
      * Use an **Element Selector** to give all `<p>` tags on the page a consistent `font-family` and `color`.
      * Use a **Class Selector** (e.g., `.product-card`) to give every card the same `background-color`, `border`, and `border-radius`.
      * Mark exactly one product as a featured deal: give that card's `<div>` a unique `id` (e.g., `id="featured"`). Use an **ID Selector** to make it stand out — change its `background-color` to a different accent color and make its `border` more prominent.
      * Apply a **Class Selector** (e.g., `.sale-price`) to the price `<p>` of the featured product to display it in a bold, eye-catching color (e.g., `color: #DC2626`).

> **💡 Tip:** To make your product cards look better without using `padding`, try using `text-align: center` on your elements! 