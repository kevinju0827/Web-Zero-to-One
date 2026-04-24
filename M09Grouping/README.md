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

Modern HTML5 introduced tags that describe the **meaning** of the content they contain. These behave exactly like `<div>` (they are block-level), but they are much better for accessibility and **SEO** (Search Engine Optimization). 

**SEO** is the practice of optimizing your website to increase its visibility and ranking in search engine results. 
By using semantic tags instead of generic `<div>` containers, you provide search engines with a clear map of your page's structure. 
This helps crawlers understand which parts of your site are the most important (like `<main>` or `<article>`), leading to better indexing and improved discoverability for your content.

* **`<header>`**: Contains introductory content or navigation links.
* **`<nav>`**: A section specifically for navigation links.
* **`<main>`**: The unique, primary content of the page.
* **`<section>`**: A generic standalone section of a document.
* **`<article>`**: A self-contained piece of content (like a blog post or news story).
* **`<aside>`**: Content tangentially related to the main content (like a sidebar).
* **`<footer>`**: Contains copyright info, contact details, or site maps.

## Guided Practice

In this practice, you will use logical grouping to organize a professional developer portfolio. You'll learn how to wrap related elements into containers to create distinct sections like a navigation header and a featured content card.

### Step 1: Establish the Semantic Shell
Before adding content, define the high-level structure of your page using semantic grouping tags. These tags tell the browser exactly what role each section plays.
* Create an HTML file and add a `<style>` tag in the `<head>`.
* Inside the `<body>`, add a `<header>` for your branding and navigation.
* Below the header, add a `<main>` tag to hold the primary content of your portfolio.
* At the very bottom, add a `<footer>` for copyright information.

### Step 2: Group the Header Content
The header often contains both a title and a navigation menu. We group them to style the top bar of the site as one unit.
* Inside your `<header>`, add an `<h1>` with the text "DevPortfolio".
* Next to the heading, add a `<nav>` container.
* Inside the `<nav>`, add three `<a>` tags for "Projects", "Blog", and "About".
* **CSS Tip:** Target the `header` in your styles and add `border-bottom: 2px solid #e5e7eb;` and `padding: 20px;` to create a clean separator from the rest of the page.

### Step 3: Create a Featured Card (The `<div>` Container)
A "card" is a classic web design pattern where a group of elements (heading, text, links) are treated as a single visual object.
* Inside the `<main>` tag, add a `<section>`.
* Inside that section, create a `<div>` and give it a class: `<div class="feature-card">`.
* Inside this `div`, add an `<h2>` for a project title and a few `<p>` tags for descriptions.
* **CSS Tip:** Target `.feature-card` in your CSS. Give it `background: white;`, `border: 1px solid #e5e7eb;`, and `box-shadow: 0 1px 3px rgba(0,0,0,0.1);`. Notice how the border and shadow surround the entire group of elements.

### Step 4: Use Inline Grouping for Emphasis
Sometimes you need to group just a few words within a sentence without breaking the flow of the text.
* Find a sentence inside your card's paragraph.
* Wrap a specific phrase (like "semantic tags") in a `<span>` tag with the class `highlight`: `<span class="highlight">...</span>`.
* **CSS Tip:** Target `.highlight` and set `background-color: #fef9c3;`. This allows you to style specific words within the block-level paragraph.

### Step 5: Finalize the Footer
The footer acts as the final group at the bottom of the document.
* Inside your `<footer>`, add a `<p>` tag with your copyright notice.
* **CSS Tip:** Set the `footer` to have a dark `background-color: #1f2937;` and `color: white;`. Use `text-align: center;` and `line-height: 5;` to give the footer height and center the text.

## Checkpoints

* [ ] Build a "Tech Blog Article" Layout
  Write an HTML webpage containing a `<style>` tag to implement a structured, modern blog post layout. Please complete the following requirements:
  * **Semantic Page Structure**: Use semantic containers to define the high-level structure of your page. Create a `<header>` for the blog's introductory content or navigation links, a `<main>` tag to house the unique, primary content of the page, and a `<footer>` at the bottom for copyright information.
  * **Grouping Content and Sidebars**: Inside your `<main>` element, group the actual blog post content within an `<article>` tag to represent a self-contained piece of content. Below or alongside the article, add an `<aside>` tag to contain tangentially related content, such as a "Related Posts" sidebar. 
  * **Author Bio Card (Generic Block Grouping)**: At the end of your `<article>`, use a `<div>` tag as a block-level container to group large sections of content together. Place an author's name, profile picture, and short biography inside this `<div>`. Apply CSS to this container (such as a border and background color) to style the grouped elements as a single visual card.
  * **Keyword Highlighting (Generic Inline Grouping)**: Pick a sentence within your blog post. Use a `<span>` tag as an inline-level container to wrap a specific phrase or keyword, which allows you to group small bits of content. Apply a special text color or background highlight to this `<span>` to emphasize the text, ensuring it does not break the natural flow of the paragraph.