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

Example:
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

### Classes and the Class Selector: `.class`

What if you only want to change the style of **some** paragraphs, not all of them? This is when we use the `class` attribute.
Think of a `class` as sticking a label on an HTML element. You can apply the exact same `class` name to multiple different elements. In CSS, we use a **period (`.`)** to select a class.

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

### Identifiers and the ID Selector: `#id`

The `id` attribute is very similar to `class`, but with one strict rule: **An `id` name can only be used once per HTML page**.
It is used to mark a unique and specific element on the page (like a navigation bar, a main title, or a specific container). In CSS, we use a **hashtag (`#`)** to select an id.

Example:
```html
<head>
  <style>
    /* Targets the unique element with id="main-title" */
    #main-title {
      color: blue;
      font-size: 32px;
    }
  </style>
</head>
<body>
  <h1 id="main-title">Welcome to My Website</h1>
  <h1>Another Heading</h1>
</body>
```

## Guided Practice

* Step 1: Set up your file
  Create a new HTML file named `style.html` with the standard document skeleton.
* Step 2: Add the Style Block
  Inside the `<head>` tag, add an opening `<style>` and closing `</style>` tag. All of our CSS rules will go in here.
* Step 3: Use an Element Selector
  Add three `<li>` list items inside the `<body>`. Then, write a rule in your `<style>` block: type `li`, add `{}`, and set the `font-size` to `18px` inside the braces.
* Step 4: Create and Target a Class
  Add two `<p>` paragraphs inside the `<body>`. Add `class="alert"` to the first paragraph. Go back up to the `<style>` block and add `.alert { color: red; }`.
* Step 5: Create and Target an ID
  At the very top of your `<body>`, add an `<h1>` heading and give it `id="hero-text"`. In the `<style>` block, add `#hero-text { color: purple; }`.
* Step 6: Preview in the browser
  Open `style.html` in your browser. Verify that your list items have larger text, your paragraph with the `alert` class is red, and your heading with the `hero-text` id is purple.

## Checkpoints

* [ ] Successfully add a `<style>` tag within the `<head>` section.
* [ ] Use an element selector to change the global styling of a specific HTML tag.
* [ ] Successfully add a `class` attribute to at least one element and style it correctly using `.` in CSS.
* [ ] Successfully add an `id` attribute to a unique element and style it correctly using `#` in CSS.
