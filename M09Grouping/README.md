# M09 Grouping

## The "Why?"

As your webpage grows from a simple list of elements to a complex interface, keeping things organized becomes a major challenge. Imagine trying to find a specific shirt in a room where all your clothes are just scattered on the floor. It's difficult to find anything, and even harder to clean up!

Logical grouping is the "closet" for your HTML. By wrapping related elements together, you create a clear structure that is:
1.  **Easier to Style**: You can apply a background color or border to an entire section (like a "Header") rather than styling each individual word or image.
2.  **Semantic**: You tell the browser (and search engines) which parts of your page are navigation, which are main content, and which are supplementary.
3.  **Flexible**: Grouping is the foundation for advanced layouts like Flexbox and Grid, which we will learn soon.

## Goals

Understand how to use container elements to organize your HTML code into logical sections.  
By the end of this module, you should be able to confidently use `<div>` and `<span>` for generic grouping, and use semantic tags like `<header>`, `<main>`, and `<footer>` to give your page a professional, meaningful structure.

## Core Concepts

### Generic Containers: `<div>` and `<span>`

When there isn't a specific tag that fits your needs, you use these "generic" containers.

*   **`<div>` (Division)**: A **block-level** container. It is used to group large sections of content together. Think of it as a big box.
*   **`<span>`**: An **inline-level** container. It is used to group small bits of content, like a few words inside a paragraph, so you can style them differently.

```html
<div class="card">
  <h2>Title</h2>
  <p>Some text with a <span class="highlight">special word</span>.</p>
</div>
```

### Semantic Containers

Modern HTML5 introduced tags that describe the **meaning** of the content they contain. These behave exactly like `<div>` (they are block-level), but they are much better for accessibility and SEO.

*   **`<header>`**: Contains introductory content or navigation links.
*   **`<nav>`**: A section specifically for navigation links.
*   **`<main>`**: The unique, primary content of the page.
*   **`<section>`**: A generic standalone section of a document.
*   **`<article>`**: A self-contained piece of content (like a blog post or news story).
*   **`<aside>`**: Content tangentially related to the main content (like a sidebar).
*   **`<footer>`**: Contains copyright info, contact details, or site maps.

## Guided Practice

Let's build a **"Personal Profile Page"** using logical grouping and semantic tags.

### Step-by-Step Instructions

*   **Step 1: Create the Semantic Shell**
    Use `<header>`, `<main>`, and `<footer>` to define the top, middle, and bottom of your page.
*   **Step 2: Add Navigation**
    Inside the `<header>`, add a `<nav>` tag with a few links (`<a>`).
*   **Step 3: Group the Profile Info**
    Inside `<main>`, create a `<div>` with a class of `profile-card`. Inside this card, put an `<img>`, an `<h2>`, and a `<p>`.
*   **Step 4: Use Inline Grouping**
    Inside the `<p>`, use a `<span>` with a class of `status-dot` to create a small visual indicator.
*   **Step 5: Apply Basic Styles**
    Add some CSS to give the `profile-card` a border and padding, and make the `status-dot` a small green circle.

### Example Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Personal Profile</title>
    <style>
        body { font-family: sans-serif; margin: 0; background-color: #f4f4f4; }
        header { background: #333; color: white; padding: 1rem; text-align: center; }
        nav a { color: white; margin: 0 10px; text-decoration: none; }
        
        .profile-card {
            background: white;
            width: 300px;
            margin: 2rem auto;
            padding: 2rem;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
            text-align: center;
        }

        .status-dot {
            height: 10px;
            width: 10px;
            background-color: #2ecc71;
            border-radius: 50%;
            display: inline-block;
            margin-right: 5px;
        }

        footer { text-align: center; padding: 1rem; font-size: 0.8rem; color: #777; }
    </style>
</head>
<body>

    <header>
        <h1>My Website</h1>
        <nav>
            <a href="#">Home</a>
            <a href="#">About</a>
            <a href="#">Contact</a>
        </nav>
    </header>

    <main>
        <div class="profile-card">
            <img src="https://via.placeholder.com/100" alt="Profile" style="border-radius: 50%;">
            <h2>Jane Doe</h2>
            <p><span class="status-dot"></span> Available for hire</p>
            <p>Frontend Developer & Designer</p>
        </div>
    </main>

    <footer>
        <p>&copy; 2026 Jane Doe. Built with Semantic HTML.</p>
    </footer>

</body>
</html>
```

## Checkpoints

* [ ] Wrap major semantic sections of your page (e.g., header, main content area, footer) inside semantic tags like `<header>`, `<main>`, and `<footer>`.
* [ ] Wrap specific highlight words or phrases within your paragraphs using `<span>` tags.
* [ ] Create a "Content Card" using a `<div>` that groups a heading, an image, and a description.
* [ ] Apply unique CSS classes to these containers and use them to apply layout-wide styles (like `text-align: center` or `background-color`).