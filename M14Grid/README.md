# M14 CSS Grid

## The "Why?"

If Flexbox is for one-dimensional layouts (a single row or column), then **CSS Grid** is the master of two-dimensional layouts. Grid allows you to align items in both rows **and** columns at the same time.

Before Grid, building complex magazine-style layouts or photo galleries with different sized boxes was incredibly difficult and required messy CSS. Grid allows you to define a blueprint (a "grid") for your page and then drop elements into specific "cells." It is the most powerful layout system available in CSS today.

## Goals

Understand the core concepts of Grid containers and items, and learn how to create multi-column and multi-row layouts.  
By the end of this module, you should be able to use `display: grid` and properties like `grid-template-columns`, `grid-template-rows`, and `gap` to build sophisticated, structured interfaces.

## Core Concepts

### 1. The Grid Container

Just like Flexbox, you start by applying `display: grid;` to a parent element.

### 2. Defining Columns and Rows

You define the "tracks" of your grid using these properties:

*   **`grid-template-columns`**: Defines the number and width of columns. You can use pixels (`px`), percentages (`%`), or the `fr` (fractional) unit.
    *   Example: `grid-template-columns: 1fr 2fr 1fr;` creates three columns where the middle one is twice as wide as the others.
*   **`grid-template-rows`**: Defines the height of rows.
*   **`repeat()` function**: A shortcut for repeating tracks.
    *   Example: `grid-template-columns: repeat(3, 1fr);` creates three equal columns.

### 3. Gap

The `gap` property (or `grid-gap`) allows you to easily add spacing between your grid cells without using margins.

## Guided Practice

Let's build a **"Modern Photo Gallery"** with a header that spans multiple columns.

### Step-by-Step Instructions

*   **Step 1: Set up the HTML**
    Create a `<div>` with the class `grid-container`. Inside, add several `<div>` items (e.g., a header and 6 image placeholders).
*   **Step 2: Initialize the Grid**
    Apply `display: grid;` to the container.
*   **Step 3: Define the Columns**
    Set `grid-template-columns: repeat(3, 1fr);` to create a 3-column layout. Add `gap: 20px;` for spacing.
*   **Step 4: Make the Header Span Across**
    Target the first item (the header) and use `grid-column: span 3;`. This tells the header to take up all three columns in the first row.
*   **Step 5: Add Visual Styling**
    Give the items background colors and padding so you can see the grid structure clearly.

### Example Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>CSS Grid Practice</title>
    <style>
        body { font-family: sans-serif; padding: 40px; background-color: #f1f5f9; }

        .gallery {
            display: grid;
            /* Create 3 equal columns */
            grid-template-columns: repeat(3, 1fr);
            gap: 20px;
            max-width: 900px;
            margin: 0 auto;
        }

        .item {
            background-color: white;
            padding: 40px;
            text-align: center;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            color: #475569;
        }

        /* Make the title span all 3 columns */
        .title-item {
            grid-column: span 3;
            background-color: #4f46e5;
            color: white;
            font-size: 1.5rem;
            font-weight: bold;
        }

        /* Make one item take up 2 rows */
        .tall-item {
            grid-row: span 2;
            background-color: #ede9fe;
            display: flex;
            align-items: center;
            justify-content: center;
        }
    </style>
</head>
<body>

    <div class="gallery">
        <div class="item title-item">Featured Gallery</div>
        <div class="item tall-item">Main Feature (2 Rows)</div>
        <div class="item">Photo 1</div>
        <div class="item">Photo 2</div>
        <div class="item">Photo 3</div>
        <div class="item">Photo 4</div>
    </div>

</body>
</html>
```

## Checkpoints

* [ ] Apply `display: grid;` to a container to enable Grid layout.
* [ ] Use `grid-template-columns` with the `fr` unit to create a flexible multi-column layout.
* [ ] Use the `gap` property to add consistent spacing between grid items.
* [ ] Use `grid-column: span X;` or `grid-row: span X;` to make an item occupy multiple cells in the grid.
* [ ] Build a 3-column photo gallery or dashboard where one item (like a header or a featured image) spans the entire width.