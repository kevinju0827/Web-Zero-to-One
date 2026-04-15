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
<div style="background-color: lightblue;">
  I am a block! I take up the whole width, even if my text is short.
</div>
<div style="background-color: lightcoral;">
  I am forced onto a new line!
</div>
```

### Inline-level Elements

An inline element does not start on a new line. It only takes up as much width as absolutely necessary to wrap its content. Think of them as words in a sentence; they simply flow next to each other.

* Common examples: `<a>`, `<strong>`, `<i>`.
* Characteristics: You **cannot** set their `width` or `height` properties. They completely ignore those CSS rules because their dimensions are dictated entirely by the text inside them.

> **Exception: The `<img>` Tag**: While technically an inline element, `<img>` is unique because it is "replaced content." This means it **does** have an intrinsic width and height, and you **can** set its width and height in CSS, unlike other inline elements.

```html
<span style="background-color: yellow;">I am inline.</span>
<span style="background-color: lightgreen;">I sit right next to my neighbor!</span>
```

### The `display` Property

What if you want a link (`<a>`) to look and function like a large, clickable block button? Or what if you want two `<div>` containers to sit side-by-side to create a two-column layout? You can override their default browser behavior using the CSS `display` property.

1. `display: block;` Forces an element to behave like a block (taking up the full row and accepting width/height).
2. `display: inline;` Forces an element to behave like inline text (shrinking to its content and sitting side-by-side).
3. `display: inline-block;` The best of both worlds! The element sits side-by-side with others (like inline), but it respects the `width` and `height` properties you set in CSS (like a block). This is incredibly useful for creating grid-like layouts, image galleries, or navigation buttons.
4. `display: none;` Completely hides the element from the page. It will look and act as if the element doesn't exist in the HTML at all, freeing up the space it previously occupied.

## Guided Practice

Let's build a simple layout to see these display types in action and learn how to manipulate them.

### Step-by-Step Instructions

* **Step 1: Set up the structure**
    Create a new HTML file. In the `<head>`, add your `<style>` block. We will write our CSS rules here.
* **Step 2: Add Block Elements**
    In the `<body>`, add two `<div>` tags and assign them both the class `box`. In your CSS, style `.box` with a background color and a thin border. Open your browser. You will see they stack vertically and span the entire screen.
* **Step 3: Add Inline Elements**
    Below the boxes, add two `<span>` tags and assign them the class `label`. In your CSS, give `.label` a different background color and try setting `width: 200px;`. Check the browser. They sit side-by-side, but the width property is completely ignored!
* **Step 4: Fix with Inline-Block**
    In your CSS, add `display: inline-block;` to your `.label` rule. Refresh the browser. The spans will still sit side-by-side, but now they will successfully expand to 200px wide.
* **Step 5: Transform a Block**
    Let's force a block to act like text. Go to your `.box` CSS rule and add `display: inline;`. Refresh the page. Your large `<div>` boxes will shrink to fit their internal text and snap next to each other on the same line, acting exactly like `<span>` tags.

### Example Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>M08 Display Types Practice</title>
    <style>
        .box {
            background-color: lightblue;
            border: 1px solid blue;
            margin: 10px 0;
            padding: 10px;
            /* Default: display: block; */
        }

        .label {
            background-color: yellow;
            padding: 5px;
            /* Inline elements ignore width/height by default */
            width: 200px; 
            margin: 5px;
        }

        /* Try uncommenting these to see the behavior change */
        /*
        .label {
            display: inline-block;
        }

        .box {
            display: inline;
        }
        */
    </style>
</head>
<body>

    <h1>Display Types Practice</h1>

    <!-- Block elements stack vertically -->
    <div class="box">Box 1 (Block Level)</div>
    <div class="box">Box 2 (Block Level)</div>

    <hr>

    <!-- Inline elements sit side-by-side -->
    <span class="label">Label 1 (Inline)</span>
    <span class="label">Label 2 (Inline)</span>

</body>
</html>
```

## Checkpoints

* [ ] Create an HTML file containing at least two default block-level elements and two default inline-level elements.
* [ ] Use CSS to change one of your block-level elements into an `inline` element, demonstrating that it now sits on the same line as surrounding elements.
* [ ] Apply the `display: inline-block;` property to an inline-level element (like a `<span>` or `<a>`) and successfully give it a specific `width` and `height`.
