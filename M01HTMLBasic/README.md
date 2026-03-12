# M01 HTML Basic

## The "Why?"

Imagine you’re writing a note on your computer. Unlike writing on paper, you can’t naturally organize your content just by switching pens, changing handwriting style, or adjusting font size on the fly.  
To support richer structure - like headings, lists, and images. We need a format that tells the computer which parts of the text are *special elements*, not just plain words.  
That’s what HTML is: a standardized markup language designed to describe the structure of content so browsers can display it correctly.

## Goals

Understand the basic syntax and standard skeleton of an HTML document and be able to write valid HTML files on your own.  
By the end of this module, you should be able to turn plain text into a structured web page using semantic elements like headings and paragraphs. 

## Core Concepts

**HTML (HyperText Markup Language)** is used to **describe the structure and meaning** of content.  
The **HyperText** means that the content is not just text, but also links to other pages, images, and other multimedia elements.  
The **Markup** is the syntax used to describe the structure of the content.  

### Element tags

HTML is made of **elements**. Most elements are written with an opening and closing tag:

- Opening tag: `<p>`
- Closing tag: `</p>`
- Content: the text inside

Example: 
`<h1>My first HTML</h1>`
`<p>This is my first HTML</p>`

By grouping content together with tags, the browser can determine the specific element type of the content.  
Each element has a specific purpose and meaning, which helps the browser understand how to display the content correctly.

### The HTML document skeleton

A typical HTML file is not just random tags — it follows a standard structure.  
Please open the `standard.html` file in your editor and browser to see the structure.

Key parts:

- `<!DOCTYPE html>`  
  Declares that this document uses modern HTML5.

- `<html>`  
  The root element of the page.

- `<head>`  
  **Metadata** that is not the main visible content:
  - `<meta charset="utf-8">` for character encoding
  - `<meta name="viewport" content="width=device-width,initial-scale=1" />` for responsive behavior on mobile
  - `<title>` for the browser tab title

- `<body>`  
  The actual visible content of your page.

## Guided Practice

* Step 1: Create a new `.txt` file
  Use Gemini to generate a short article (or write it yourself).
  Save it in the `M01HTMLBasic` folder as `my_article.txt`.
* Step 2: Convert the `.txt` file into a `.html` file
  Ask Gemini to convert the `.txt` content into a valid HTML document with the basic skeleton, including `<!DOCTYPE html>`, `<html>`, `<head>`, and `<body>`.
  Open the `.html` file in a browser (by right-clicking and selecting `Open In | Browser | Chrome`) to see the result.
* Step 3: Improve the page presentation by asking Gemini
  Ask Gemini to add tags, styles, and attributes to make the HTML document look better.

## Checkpoints

* [ ] Convert `sample_latte.txt` into a proper HTML document.
* [ ] Modify the `<title>` element of the HTML document to append `(Course Practice)` to the end.
