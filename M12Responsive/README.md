# M12 Responsive Design

## The "Why?"

Gone are the days when people only browsed the web on a desktop computer. Today, your website will be viewed on everything from a massive 4K monitor to a tiny smartphone screen. If your layout is "fixed" at 1000px wide, mobile users will have to zoom in and out, creating a frustrating experience.

Responsive design is the practice of building websites that "respond" to the device's screen size. It's like water—it takes the shape of the container it's in. By mastering responsive design, you ensure your content is beautiful and accessible to everyone, no matter what device they are using.

## Goals

Understand the core principles of the mobile-first approach and learn how to use Media Queries to adapt layouts.  
By the end of this module, you should be able to use the Viewport Meta Tag and write CSS `@media` rules to change styling based on the width of the browser.

## Core Concepts

### 1. The Viewport Meta Tag

To tell mobile browsers that your site is mobile-friendly, you **must** include this tag in your `<head>`:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Without this, mobile browsers will try to "mimic" a desktop screen, making everything tiny.

### 2. Media Queries

Media queries are the "If/Then" statements of CSS. They allow you to apply certain styles only when specific conditions are met (like a certain screen width).

```css
/* Standard styles for mobile first */
.container { width: 100%; }

/* "If" the screen is wider than 768px (Tablet/Desktop) */
@media (min-width: 768px) {
    .container { width: 50%; }
}
```

### 3. Mobile-First Approach

It is standard industry practice to write your "base" CSS for small screens (mobile) first, and then use media queries with `min-width` to add complexity as the screen gets larger. This makes your code cleaner and more efficient.

## Guided Practice

Let's build a **"Responsive Hero Section"** that changes its layout from a single column on mobile to two columns on desktop.

### Step-by-Step Instructions

*   **Step 1: Add the Viewport Tag**
    Ensure your HTML `<head>` includes the viewport meta tag.
*   **Step 2: Create a Mobile Layout**
    Create a `<div>` with the class `hero`. Inside, add a `<div>` for `text-content` and an `<img>`. By default, they will stack vertically because they are block elements.
*   **Step 3: Define a Breakpoint**
    In your CSS, add an `@media (min-width: 768px)` rule.
*   **Step 4: Change Layout for Desktop**
    Inside the media query, change the `hero` container to use `display: flex;`. This will make the text and image sit side-by-side on larger screens.
*   **Step 5: Test it Out**
    Open your browser, right-click and select **Inspect**. Use the "Device Toggle" icon to shrink the screen and watch the layout snap between mobile and desktop views.

### Example Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Responsive Design Practice</title>
    <style>
        body { font-family: sans-serif; margin: 0; padding: 20px; }

        .hero {
            background-color: #f3f4f6;
            padding: 40px;
            border-radius: 12px;
            text-align: center; /* Mobile: centered text */
        }

        .hero img {
            width: 100%;
            max-width: 400px;
            border-radius: 8px;
            margin-top: 20px;
        }

        /* Desktop Breakpoint */
        @media (min-width: 768px) {
            .hero {
                display: flex;
                align-items: center;
                justify-content: space-between;
                text-align: left; /* Desktop: left-aligned text */
            }

            .hero-text { flex: 1; padding-right: 40px; }
            .hero img { margin-top: 0; }
        }
    </style>
</head>
<body>

    <div class="hero">
        <div class="hero-text">
            <h1>Building for Everyone</h1>
            <p>Our app works seamlessly on your phone, tablet, and computer. Try resizing this window!</p>
        </div>
        <img src="https://images.unsplash.com/photo-1551650975-87deedd944c3?w=500" alt="Mobile App">
    </div>

</body>
</html>
```

## Checkpoints

* [ ] Include the `<meta name="viewport">` tag in your HTML and explain to someone why it's necessary.
* [ ] Write at least one CSS **Media Query** (`@media`) to change the layout for screens smaller than 768px (mobile devices).
* [ ] Create a layout that displays elements in a single column on mobile but switches to **two or three columns** on a desktop screen.
* [ ] Test the responsiveness of your site using the device toolbar in Chrome's Developer Tools.
* [ ] Ensure text remains readable and images do not overflow their containers on mobile viewports.