# M01 HTML Basic

## The "Why?"

Imagine you’re writing a note on your computer. Unlike writing on paper, you can’t naturally organize your content just by switching pens, changing handwriting style, or adjusting font size on the fly.

To support richer structure—like headings, lists, and images—we need a format that tells the computer which parts of the text are *special elements*, not just plain words.

That’s what HTML is: a standardized markup language designed to describe the structure of content so browsers can display it correctly.

## Goals

Understand the basic syntax and common skeleton of an HTML document.

## Core Concepts

**HTML (HyperText Markup Language)** is used to **describe the structure and meaning** of content.

### Element tags

HTML is made of **elements**. Most elements are written with an opening and closing tag:

- Opening tag: `<p>`
- Closing tag: `</p>`
- Content: the text inside

Example: 
`<h1>My first HTMl</h1>`
`<p>This is my first HTML</p>`

### The HTML document skeleton

A typical HTML file is not just random tags—it follows a standard structure.

Key parts:

- `<!DOCTYPE html>`  
  Declares this document uses modern HTML.

- `<html>`  
  The root element of the page.

- `<head>`  
  “Metadata” that is not the main visible content:
  - `<meta charset="utf-8">` for character encoding
  - `<meta name="viewport" ...>` for responsive behavior on mobile
  - `<title>` for the browser tab title

- `<body>`  
  The actual visible content of your page.

## Checkpoints

* [ ] Manually write (or use AI to generate) a short article, then convert it into an HTML document.
* [ ] Modify the `<title>` element of the HTML document to append `(Course Practice)` to the end.
