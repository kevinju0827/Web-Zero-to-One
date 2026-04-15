# M11 Position

## The "Why?"

By default, the browser places elements one after another in the "normal document flow." But what if you want a navigation bar to stay at the top while you scroll? Or a "Chat" button that floats in the bottom-right corner? Or a popup that overlaps other content?

The CSS `position` property allows you to break out of the normal flow. It gives you the power to place elements precisely where you want them on the screen, relative to themselves, their containers, or even the entire browser window.

## Goals

Master the different positioning methods in CSS and understand how they interact with each other.  
By the end of this module, you should be able to confidently use `static`, `relative`, `absolute`, `fixed`, and `sticky` to create complex, multi-layered layouts.

## Core Concepts

The `position` property is used in conjunction with the "offset" properties: `top`, `bottom`, `left`, and `right`.

1.  **`static` (Default)**: The element follows the normal flow. Offset properties (`top`, `left`, etc.) have **no effect**.
2.  **`relative`**: The element is positioned relative to its **original position**. It still occupies its original space in the document flow, but you can "nudge" it without affecting its neighbors.
3.  **`absolute`**: The element is removed from the normal flow. It is positioned relative to its **nearest "positioned" ancestor** (an ancestor with any position other than `static`). If no such ancestor exists, it positions itself relative to the entire page (`<body>`).
4.  **`fixed`**: The element is removed from the normal flow and positioned relative to the **browser viewport** (the screen). It stays in the same place even when the page is scrolled.
5.  **`sticky`**: A hybrid of `relative` and `fixed`. The element behaves like `relative` until it reaches a specific scroll point, then it "sticks" like `fixed`.

### The `z-index` Property

When elements start overlapping, `z-index` determines which one stays on top. A higher `z-index` value means the element will appear in front of elements with lower values.

## Guided Practice

Let's build a **"Modern Web Dashboard Fragment"** featuring a sticky header and a floating notification badge.

### Step-by-Step Instructions

*   **Step 1: Create a Sticky Header**
    Create a `<header>` and give it `position: sticky; top: 0;`. Add enough content below it to enable scrolling and verify it stays at the top.
*   **Step 2: Use Relative Positioning for a Container**
    Create a `<div>` with the class `icon-container` and set it to `position: relative;`. This will be the reference point for our badge.
*   **Step 3: Create an Absolute Notification Badge**
    Inside the container, add a `<span>` with the class `badge`. Set it to `position: absolute; top: -5px; right: -5px;`. This places it perfectly on the corner of the icon.
*   **Step 4: Create a Fixed "Help" Button**
    Create a `<button>` at the very bottom of your HTML. Set it to `position: fixed; bottom: 20px; right: 20px;`. It will now float over the content.

### Example Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Positioning Practice</title>
    <style>
        body { font-family: sans-serif; height: 2000px; margin: 0; padding-top: 60px; }
        
        .sticky-nav {
            position: sticky;
            top: 0;
            background: #2563eb;
            color: white;
            padding: 15px;
            z-index: 100;
        }

        .content { padding: 20px; }

        .icon-container {
            position: relative;
            display: inline-block;
            background: #e5e7eb;
            padding: 20px;
            border-radius: 8px;
            margin-top: 50px;
        }

        .badge {
            position: absolute;
            top: -10px;
            right: -10px;
            background: #ef4444;
            color: white;
            padding: 4px 8px;
            border-radius: 50%;
            font-size: 12px;
            font-weight: bold;
        }

        .floating-btn {
            position: fixed;
            bottom: 30px;
            right: 30px;
            background: #10b981;
            color: white;
            border: none;
            padding: 15px 25px;
            border-radius: 50px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.2);
            cursor: pointer;
        }
    </style>
</head>
<body>

    <nav class="sticky-nav">Sticky Navigation Bar</nav>

    <div class="content">
        <h1>Positioning Demo</h1>
        <p>Scroll down to see the header stick and the button stay fixed.</p>

        <div class="icon-container">
            🔔 Notification Icon
            <span class="badge">3</span>
        </div>
    </div>

    <button class="floating-btn">Need Help?</button>

</body>
</html>
```

## Checkpoints

* [ ] Apply `position: sticky;` to create a header that remains visible at the top of the viewport during scrolling.
* [ ] Create a "Parent-Child" positioning relationship: Set the parent to `relative` and the child to `absolute` to place a small element (like a badge or close button) in a specific corner of the parent.
* [ ] Implement a `fixed` element (like a "Back to Top" button) that stays in the same screen position regardless of scrolling.
* [ ] Experiment with `z-index` to ensure that your sticky or fixed elements always stay on top of other page content.