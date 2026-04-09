# M06 Color and Font

## The "Why?"

Up to this point, you've learned how to build the skeleton of a website—text, lists, tables, and forms. But plain HTML is visually quite dull, usually defaulting to black text on a white background. If every website looked like this, the internet would be a very boring place!

To make a website engaging, guide the user's attention, and establish a unique brand identity, we need to add "Styles".

By adjusting colors and fonts, you can transform a basic layout into a professional interface or make an important warning message stand out.

This module will take you through your first steps in web design, teaching you how to beautify your content directly within your HTML.

## Goals

Understand the concept of **Inline Styles** and how to use the HTML `style` attribute.  
By the end of this module, you should be able to apply different text colors (using keywords, Hex codes, and RGBA values) to your elements, and freely adjust font sizes and font families to create a polished look.

## Core Concepts

To change the appearance of an HTML element, the most direct method is using the `style` attribute. This allows us to write style rules directly inside our HTML tags.

The syntax for the `style` attribute looks like this: `style="property: value;"`. Pay close attention to the colon (`:`) in the middle and the semicolon (`;`) at the end.

### The `style` Attribute

You can add the `style` attribute to almost any HTML tag (such as `<p>`, `<h1>`, `<span>`, `<div>`, etc.).

```html
<p style="color: blue;">This is a blue paragraph.</p>
```

### Text Color: `color`

The `color` property is specifically used to change the color of the text. In modern web development, there are a few common ways to define colors:

1. Color Keywords  
   HTML supports over 140 named colors. This is the simplest and most intuitive way to set a color, often used for quick prototyping.
   * Common keywords: `red`, `blue`, `green`, `black`, `white`, `crimson` (a deep red), etc.  
   
   ```html
   <p style="color: crimson;">System Warning: Connection Failed!</p>
   ```

2. Hex Codes (Industry Standard)  
   In real-world development, designers most frequently provide colors in Hex format. It starts with a `#` followed by 6 alphanumeric characters representing the mix of red, green, and blue.
   * For example: `#000000` is pure black, `#FFFFFF` is pure white, and `#3B82F6` is a modern tech blue.  
   
   ```html
   <h1 style="color: #3B82F6;">Main Heading</h1>
   ```

3. RGBA Values  
   When you need a more precise color or want to add "transparency," RGBA is an incredibly powerful tool. In modern UI design, we often use transparency to establish a visual hierarchy between "primary" and "secondary" text.  
   RGBA stands for Red, Green, Blue, and Alpha (transparency).
   * The values for **R, G, and B** range from `0` to `255`.
   * The value for **A (Alpha)** ranges from `0.0` (completely transparent) to `1.0` (completely opaque).  
   
   ```html
   <p style="color: rgba(15, 23, 42, 0.6);">Published on April 9, 2026</p>
   ```

### Text Alignment: `text-align`

This controls the horizontal alignment of the text inside an element. It is one of the most frequently used styling properties!

* Common values: `center`, `right`, `left` (default), `justify`.

```html
<h1 style="text-align: center;">A Perfectly Centered Title</h1>
```

### Text Decoration: `text-decoration`

This property adds or removes lines attached to the text. It's often used to highlight links or strike through old prices.

* Common values: `underline`, `line-through` (strikethrough), `none`.

```html
<p>Original price <span style="text-decoration: line-through; color: gray;">$99</span>, now $49!</p>
```

### Font Size: `font-size`

To adjust the size of your text, we use the `font-size` property.  
The most basic unit of measurement is pixels (abbreviated as `px`).  
This gives you precise control over how large the text appears on the screen.  
In modern web design, body text is usually set around `16px`, while headings are significantly larger.

Example:
```html
<p style="font-size: 24px;">This is 24px medium-large text.</p>
<p style="font-size: 14px;">This is 14px annotation text.</p>
```

### Font Family: `font-family`

By default, browsers usually display text in a serif font (like Times New Roman), which can sometimes be harder to read on screens. Using `font-family`, you can change the typeface to a more modern sans-serif font.  
In practice, we provide a "stack" of font names as fallbacks. Modern developers frequently use the "System Font Stack" to ensure optimal performance and a native, beautiful look on any operating system.

Example:
```html
<p style="font-family: system-ui, -apple-system, sans-serif;">This is a highly modern sans-serif font.</p>
```

## Guided Practice

Now, let's combine these techniques to build a highly refined, dark-themed **"Digital Business Card"**! By setting a contrast between the page background and the card container, and applying some targeted text styling, we can create a professional and modern visual experience.

* Step 1: Set the Page Background
  Create a new HTML file. To set the dark mode mood, first apply a deep slate-blue background to the `<body>` tag (`background-color: #0F172A`). Make sure all text uses a clean sans-serif font (`font-family: Arial, sans-serif;`) and center everything on the page using `text-align: center;`.
* Step 2: Create the Card Container (`<div>`)
  Inside the body, add a `<div>` tag to act as our physical card. Give it a slightly lighter background to make it stand out (`background-color: #1E293B;`). Set its width to `350px` and use `display: inline-block;` so the body's centering works perfectly on it. Finally, add a subtle border (`border: 1px solid #334155;`) and rounded corners (`border-radius: 8px;`).
* Step 3: Craft the Name and Job Title
  Add an `<h1>` inside the `<div>` for the name, using a crisp, icy white color (`color: #F8FAFC;`). Below it, add an `<h3>` for the job title, using an accent amber color to draw the eye (`color: #F59E0B;`).
* Step 4: Add a Tagline
  Use an `<i>` tag to italicize a short tagline ("Building seamless web experiences."). Set its color to a muted slate (`color: #94A3B8;`) so it doesn't distract from the main headings.
* Step 5: Format the Contact Details
  Add two `<p>` tags for your email and mobile number. Set the main paragraph color to white (`color: #F8FAFC;`), but wrap the labels ("Email: " and "Mobile: ") inside `<span>` tags. Apply the muted slate color (`color: #94A3B8;`) to these spans to create a clear visual hierarchy.
* Step 6: Add a Call-to-Action Link
  Finally, add an `<a>` tag to link to your website. Make it pop by using the accent amber color again (`color: #F59E0B;`), removing the default underline (`text-decoration: none;`), and making it bold and slightly larger (`font-weight: bold; font-size: 18px;`). Add two `<br>` tags at the end to give the bottom of the card some breathing room.

## Checkpoints

* [ ] Create an HTML promotional product card for a "Holiday Sale" using inline styles. 
      Apply a modern sans-serif `font-family` and use `text-align` to center all the content. 
      Use a Hex code `color` to make the product name stand out, apply `text-decoration: line-through` to the original price, and emphasize the new discounted price with a larger `font-size`. 
      Finally, use an RGBA `color` to make the promotional fine print (e.g., "Offer valid while supplies last") appear semi-transparent and muted.
