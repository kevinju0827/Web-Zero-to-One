# M06 Color and Font

## The "Why?"

Up to this point, you've learned how to build the skeleton of a website—text, lists, tables, and forms. But plain HTML is visually quite dull, usually defaulting to black text on a white background. If every website looked like this, the internet would be a very boring place!

To make a website engaging, guide the user's attention, and establish a unique brand identity, we need to add "Styles." By adjusting colors and fonts, you can transform a basic form into a professional interface or make an important warning message stand out. This module will take you through your first steps in web design, teaching you how to beautify your content directly within your HTML.

## Goals

Understand the concept of Inline Styles and how to use the HTML `style` attribute.  
By the end of this module, you should be able to apply different text colors (using keywords and RGBA values) to your elements, and freely adjust font sizes and font families.

## Core Concepts

To change the appearance of an HTML element, the most direct method is using the `style` attribute. This allows us to write Style rules directly inside our HTML tags.

The syntax for the `style` attribute looks like this: `style="property: value;"`. Pay close attention to the colon (`:`) in the middle and the semicolon (`;`) at the end.

### The `style` Attribute

You can add the `style` attribute to almost any HTML tag (such as `<p>`, `<h1>`, `<span>`, etc.).

Example:
```html
<p style="color: blue;">This is a blue paragraph.</p>
```

### Text Color: `color`

The `color` property is specifically used to change the color of the text. There are a few common ways to define colors on the web:

**1. Color Keywords** 

HTML supports over 140 named colors. This is the simplest and most intuitive way to set a color.
* Common keywords: `red`, `blue`, `green`, `black`, `white`, `orange`, etc.

Example:
```html
<h1 style="color: tomato;">Warning!</h1>
```

**2. RGBA Values** 

When you need a more precise color or want to add "transparency," RGBA is an incredibly powerful tool.  
RGBA stands for Red, Green, Blue, and Alpha (transparency).
* The values for **R, G, and B** range from `0` to `255`.
* The value for **A (Alpha)** ranges from `0.0` (completely transparent) to `1.0` (completely opaque).

Example:
```html
<p style="color: rgba(128, 0, 128, 0.5);">This text is semi-transparent purple.</p>
```

### Font Size: `font-size`

To adjust the size of your text, we use the `font-size` property. The most basic unit of measurement is pixels (abbreviated as `px`). This gives you precise control over how large the text appears on the screen.

Example:
```html
<p style="font-size: 24px;">This text is 24 pixels large.</p>
<p style="font-size: 12px;">This text is quite small.</p>
```

### Font Family: `font-family`

By default, browsers usually display text in a serif font similar to Times New Roman. Using `font-family`, you can change the typeface to make your web page look more modern.  
Usually, we provide multiple font names as "fallbacks" just in case the user's computer doesn't have our first choice installed. We typically end the list with a generic font family (like `sans-serif`).

Example:
```html
<p style="font-family: Arial, Helvetica, sans-serif;">This is a modern sans-serif font.</p>
```

## Guided Practice

* Step 1: Set up your file  
  Create a new HTML file named `design.html` with the standard document skeleton. Add an `<h1>` heading at the top, like `<h1>My Styling Playground</h1>`.
* Step 2: Apply a Color Keyword  
  Add the `style` attribute to your `<h1>` tag and use `color` to make the heading your favorite color (e.g., `color: teal;`).
* Step 3: Experiment with RGBA  
  Add a `<p>` paragraph below the heading. Type some text and use an RGBA value to give it a color with some transparency.
* Step 4: Change the Font Size  
  Add an `<h2>` heading. Use the `font-size` property to set its size to `36px`.
* Step 5: Mix and Match Multiple Styles  
  You can have multiple styles inside a single tag! Add one final `<p>` paragraph. Inside its `style` attribute, set the `color`, `font-size`, and `font-family` all at once. Remember to separate each rule with a semicolon `;`!  
  *(Example: `style="color: red; font-size: 18px; font-family: Arial;"`)*
* Step 6: Preview in the browser  
  Open `design.html` in your browser. Verify that your heading is colored, your paragraph has a transparency effect, and your mixed-style paragraph displays correctly.

## Checkpoints

* [ ] Successfully change text color using the `style` attribute and a color keyword (like `blue` or `red`).
* [ ] Successfully set a text color with transparency using an `rgba()` value.
* [ ] Successfully change text size using the `font-size` property (with the `px` unit).
* [ ] Successfully combine two or more CSS properties inside a single HTML element (separated by semicolons).
