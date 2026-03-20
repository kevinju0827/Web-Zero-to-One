# M02 Common Elements

## The "Why?"

In the previous module, you learned how to create a valid HTML document with the standard skeleton.  
But a real web page needs more than just headings and paragraphs.  
If every piece of content is written in the same plain format, the page becomes difficult to read and lacks emphasis, structure, and expression.

HTML provides many common elements that let us describe content more precisely.  
For example, we may want to:

- separate lines of text
- highlight important words
- show text in italic style
- write chemical formulas or math expressions
- insert notes for ourselves
- place an interactive button on the page

By learning these common elements, you can write HTML documents that are not only valid, but also clearer, richer, and more expressive.

## Goals

Understand the purpose of several commonly used HTML elements and be able to apply them appropriately in a document.  
By the end of this module, you should be able to enrich a plain HTML page with line breaks, emphasized text, superscript and subscript text, buttons, and comments.

## Core Concepts

In HTML, different tags represent different kinds of meaning or presentation.  
Even when the content is short, choosing the right element helps both the browser and the reader understand your document more clearly.

### Headings: `<h1>` to `<h6>`

Headings are used to create a content hierarchy.

- `<h1>` is the main title of the page
- `<h2>` is a major section heading
- `<h3>` is a subsection heading
- ...
- `<h6>` is the smallest heading level

Example:

`<h1>My Favorite Drinks</h1>`  
`<h2>Coffee</h2>`  
`<h3>Latte</h3>`

A page should usually have exactly one `<h1>` that represents the main topic.  
Lower-level headings should be used in order to keep the document structure logical.

### Line break: `<br>`

The `<br>` element inserts a line break inside text.  
It is useful when you want text to continue in the same paragraph but appear on a new line.

Example:

`Good morning.<br>Welcome to my page.`

Unlike most HTML elements, `<br>` does not wrap content with opening and closing tags.

### Bold text: `<b>`

The `<b>` element makes text visually bold.

Example:

`This is a <b>very important</b> word.`

Use it when you want a visual emphasis.  
Later, as you learn more semantic HTML, you will also encounter tags like `<strong>`, which carry stronger meaning.

### Italic text: `<i>`

The `<i>` element displays text in italic style.

Example:

`I want to say this in <i>a softer tone</i>.`

It is often used for stylistic changes, foreign words, thoughts, or special terms.

### Button: `<button>`

The `<button>` element creates a clickable button.

Example:

`<button>Click Me</button>`

At this stage, you can think of it as an interactive UI element.  
Even without JavaScript, it helps you recognize how HTML can represent parts of a user interface, not just article text.

### Subscript: `<sub>`

The `<sub>` element displays text slightly below the normal text line.

Example:

`H<sub>2</sub>O`

This is commonly used in chemical formulas or annotations.

### Superscript: `<sup>`

The `<sup>` element displays text slightly above the normal text line.

Example:

`x<sup>2</sup>`

This is commonly used in exponents, footnote markers, or mathematical expressions.

### Comments: `<!-- -->`

HTML comments are notes written inside the file that are not displayed on the web page.

Example:

`<!-- This section introduces the topic -->`

Comments are useful for:

- leaving reminders for yourself
- explaining sections of code
- marking unfinished parts

Browsers ignore comments when rendering the page.

## Guided Practice

* Step 1: Open your HTML file from M01  
  Start with the HTML page you created in the previous module, or create a new HTML file with the standard document skeleton.

* Step 2: Add a clearer content structure  
  Write one `<h1>` as the main title of the page.  
  Then add `<h2>` or `<h3>` headings to divide the content into smaller sections.

* Step 3: Add paragraph content  
  Write at least three paragraphs about a topic you like, or ask Gemini to generate a short article for you.  
  Put the article content into `<p>` tags.

* Step 4: Enrich the content with common elements  
  Modify parts of your text by adding:
  - `<br>` for line breaks
  - `<b>` for bold text
  - `<i>` for italic text
  - `<sub>` or `<sup>` where appropriate

  For example, you can write:
  - a chemical formula like `CO<sub>2</sub>`
  - a math expression like `2<sup>3</sup>`

* Step 5: Add a button  
  Insert a simple `<button>` element somewhere in the page, such as:

  ` <button>Learn More</button> `

* Step 6: Add comments to organize your file  
  Add HTML comments above one or two sections to describe what that section does.

* Step 7: Preview the page in the browser  
  Open the HTML file in your browser and observe how each element changes the appearance and structure of the page.

## Checkpoints

* [ ] Use `<h1>`~`<h6>` to separate paragraphs in the content of `notes_sample.txt`, and highlight important points in bold.
