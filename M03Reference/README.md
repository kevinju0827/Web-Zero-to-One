# M03 References and Media

## The "Why?"

In the previous modules, you learned how to structure text using headings, paragraphs, and text-formatting elements. 
However, a website consisting solely of isolated text can feel disconnected and dull.

Real-world web pages need to connect to other pages and display rich media like photos and videos. 
To do this, we need a way to tell the browser *where* to find these external resources. 
By learning how to use tags that reference external URLs or local files, you can transform a simple text document into a fully connected, interactive, and visually engaging multimedia experience.

## Goals

Understand the concept of HTML attributes and how they provide additional instructions to elements. 
By the end of this module, you should be able to insert images, create clickable hyperlinks between multiple web pages, and embed external content like YouTube videos.

## Core Concepts

### HTML Attributes

To link to other files or display media, we use specific tags combined with **attributes**.  
Attributes provide additional information about HTML elements. They are always specified in the **opening tag** and usually come in name/value pairs like: `name="value"`.

Example:
`<tagname attribute="value">Content goes here...</tagname>`

Different tags require different attributes to function correctly.

### Images: `<img>`

The `<img>` element is used to embed an image into a web page. 
Similar to the `<br>` tag you learned in M02, the `<img>` tag is "empty" - it does not have a closing tag.

It requires two essential attributes:
- `src` (Source): Specifies the path or URL to the image file.
- `alt` (Alternative text): Provides a text description of the image for screen readers or if the image fails to load.

Example (using a local `.webp` image in the same folder):
`<img src="island_sample.webp" alt="A small island floating on the sea">`

### Links: `<a>`

The `<a>` (Anchor) element is used to create hyperlinks, which connect one web page to another.
Its most important attribute is `href` (Hypertext Reference), which indicates the destination address.

Example (linking two files in the same folder):
`<a href="about.html">Click here to learn more about me</a>`

When a user clicks the text "Click here to learn more about me", the browser will navigate to `about.html`. You can also put full URLs in the `href` attribute to link to external websites (e.g., `href="https://www.google.com"`).

### Embedding Content: `<iframe>`

The `<iframe>` (Inline Frame) element allows you to embed another HTML document (like a YouTube video or a Google Map) directly into your current page.

To embed a YouTube video, you use the `src` attribute pointing to the video's embed URL.

Example:
`<iframe src="https://youtu.be/dQw4w9WgXcQ"></iframe>`

*(Note: When getting a video from YouTube, you can simply click "Share" -> "Embed" to get the fully generated `<iframe>` code, which often includes extra attributes for width, height, and fullscreen permissions.)*

## Guided Practice

* Step 1: Set up your files
  In your module folder, create two new HTML files with the standard document skeleton: `index.html` and `about.html`.
  Also, place an image file named `sample.webp` into this exact same folder.

* Step 2: Create a hyperlink between pages
  In `index.html`, write a welcome message and add a link pointing to your about page:
  `<p>Welcome to my homepage! <a href="about.html">Go to About Page</a></p>`
  In `about.html`, add a link to go back:
  `<p>This is the About Page. <a href="index.html">Go Back</a></p>`

* Step 3: Insert a local image
  In `index.html`, display the image you prepared by adding the `<img>` tag:
  `<img src="sample.webp" alt="A sample image for practice">`

* Step 4: Embed a YouTube video
  Go to YouTube, find a video you like, click "Share", and select "Embed". 
  Copy the provided `<iframe>` code and paste it into your `index.html` file below your image.

* Step 5: Test the connections
  Open `index.html` in your browser. Verify that the image displays correctly, the YouTube video can play, and clicking the link successfully navigates to `about.html`.

## Checkpoints

* [ ] Successfully link `index.html` and `about.html` so you can navigate back and forth between them.
* [ ] Display a local `.webp` image using the `<img>` tag and ensure the `alt` attribute is correctly filled out.
* [ ] Successfully embed a YouTube video on the page using an `<iframe>`.