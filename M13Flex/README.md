# M13 Flexbox

## The "Why?"

Before Flexbox, creating layouts in CSS was notoriously difficult. Developers had to use hacks like `float` or `table` to align elements side-by-side, which often led to buggy and frustrating code. Something as simple as centering an item vertically was a major headache.

Flexbox (the Flexible Box Module) changed everything. It was designed specifically to handle one-dimensional layouts—either a row or a column. It makes it incredibly easy to align items, distribute space, and handle different screen sizes with just a few lines of code. If you want to build a modern navigation bar, a list of items, or a centered login form, Flexbox is your best friend.

## Goals

Master the fundamentals of Flexbox and learn how to align items along the main and cross axes.  
By the end of this module, you should be able to use `display: flex` and properties like `justify-content`, `align-items`, and `flex-direction` to create dynamic and organized layouts.

## Core Concepts

Flexbox works with a **Container** (the parent) and **Items** (the children).

### 1. The Flex Container

To start using Flexbox, you apply `display: flex;` to the parent element. This instantly turns all its direct children into "flex items."

### 2. Main Axis Properties

These properties control how items are distributed along the "Main Axis" (usually horizontal).

*   **`flex-direction`**: Defines the direction (e.g., `row`, `column`).
*   **`justify-content`**: Controls horizontal alignment (e.g., `flex-start`, `center`, `flex-end`, `space-between`, `space-around`).
*   **`flex-wrap`**: Allows items to wrap to a new line if they run out of space.

### 3. Cross Axis Properties

These properties control how items are distributed along the "Cross Axis" (usually vertical).

*   **`align-items`**: Controls vertical alignment of items within a row (e.g., `stretch`, `center`, `flex-start`, `flex-end`).

## Guided Practice

Let's build a **"Professional Navigation Bar"** using Flexbox to align a logo and some links.

### Step-by-Step Instructions

*   **Step 1: Set up the Navbar**
    Create a `<nav>` element with a logo `<div>` and a `<ul>` for links.
*   **Step 2: Enable Flexbox**
    Apply `display: flex;` to the `<nav>`. Notice how the logo and the list now sit side-by-side.
*   **Step 3: Distribute Space**
    Use `justify-content: space-between;` on the `<nav>`. This pushes the logo to the left and the links to the right.
*   **Step 4: Align Vertically**
    Use `align-items: center;` on the `<nav>` to ensure the logo and links are perfectly centered vertically.
*   **Step 5: Style the Links**
    Apply `display: flex;` to the `<ul>` as well to make the list items sit in a horizontal row. Use `gap: 20px;` to add spacing between them.

### Example Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flexbox Navbar Practice</title>
    <style>
        body { font-family: sans-serif; margin: 0; background-color: #f8fafc; }

        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: #1e293b;
            color: white;
            padding: 1rem 5%;
        }

        .logo { font-size: 1.5rem; font-weight: bold; }

        .nav-links {
            display: flex;
            list-style: none;
            margin: 0;
            padding: 0;
            gap: 24px; /* Space between flex items */
        }

        .nav-links a {
            color: white;
            text-decoration: none;
            font-weight: 500;
        }

        .nav-links a:hover { color: #38bdf8; }
    </style>
</head>
<body>

    <nav class="navbar">
        <div class="logo">FlexBrand</div>
        <ul class="nav-links">
            <li><a href="#">Home</a></li>
            <li><a href="#">Features</a></li>
            <li><a href="#">Pricing</a></li>
            <li><a href="#">About</a></li>
        </ul>
    </nav>

    <div style="padding: 50px; text-align: center;">
        <h2>Flexbox makes alignment easy!</h2>
        <p>The navbar above uses Flexbox for horizontal layout, spacing, and vertical centering.</p>
    </div>

</body>
</html>
```

## Checkpoints

* [ ] Apply `display: flex;` to a parent container to enable Flexbox for its children.
* [ ] Use `justify-content` to distribute items along the main axis (e.g., centering items or pushing them to opposite ends).
* [ ] Use `align-items` to center elements vertically within a container.
* [ ] Use `flex-direction: column;` to stack elements vertically, and understand how the main and cross axes swap.
* [ ] Implement a navigation bar or a horizontal list where items are spaced evenly using the `gap` property.