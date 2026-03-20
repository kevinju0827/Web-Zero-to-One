# M05 Form

## The "Why?"

Up until now, the websites you've built have been a one-way street: you display information, and the user consumes it. But what if you want to hear back from your users? 

Think about logging into your favorite app, typing a query into a search engine, or filling out shipping details for an online order. All of these interactions rely on forms. Forms are the primary way users submit data to a website. 

While making a form actually *process* data requires a backend server or JavaScript, every functional form starts with a solid, well-structured visual interface. In this module, we will focus purely on building the frontend UI of a form—creating the text boxes, buttons, and options that users will eventually interact with.

## Goals

Understand the structure of user input elements and how to group them.  
By the end of this module, you should be able to build a complete visual interface for a contact form or login page using various input types, labels, and buttons.

## Core Concepts

Forms are built using a container element that holds various input controls. To make the interface user-friendly and accessible, we also pair these inputs with descriptive labels.

### The Container: `<form>`

The `<form>` element acts as a wrapper for all your input fields. While it doesn't change the visual appearance on its own, it tells the browser that all the inputs inside it belong together.

### Describing Inputs: `<label>`

A `<label>` tells the user what information belongs in a specific input field. 
More importantly, labels improve accessibility. When you correctly link a label to an input, clicking the text of the label will automatically focus the input box. You link them by matching the label's `for` attribute with the input's `id` attribute.

### Single-Line Inputs: `<input>`

The `<input>` tag is the most versatile element in forms. Like `<img>`, it is an empty tag (it does not have a closing tag). Its behavior completely changes based on its `type` attribute.

Common types include:
* `type="text"`: Standard single-line text (e.g., a username).
* `type="email"`: Text field that expects an email address format.
* `type="password"`: Hides the characters as the user types.
* `type="radio"`: Allows the user to select only one option from a group.
* `type="checkbox"`: Allows the user to select multiple options.

You can also use the `placeholder` attribute to display a temporary hint inside the box before the user types.

Example:

```html
<label for="username">Your Name:</label>
<input type="text" id="username" placeholder="e.g. John Doe">
```

### Multi-Line Inputs: `<textarea>`

If you need the user to type a long message, like a comment or feedback, use the `<textarea>` element. Unlike `<input>`, it requires both an opening and closing tag.

Example:

```html
<label for="message">Leave a message:</label>
<textarea id="message" placeholder="Type your thoughts here..."></textarea>
```

### Submitting: `<button>`

Every form needs a way to be submitted. The `<button>` element provides a clickable interface for the user to finish their task.

Example:

```html
<button type="submit">Send Message</button>
```

*(Note: Clicking this button will usually refresh the page by default. Because we are only building the visual interface in this course, we won't be writing the code to actually send the data!)*

## Guided Practice

* Step 1: Set up your file
  Create a new HTML file named `contact.html` with the standard document skeleton. Add an `<h1>` heading like `<h1>Contact Us</h1>`.
* Step 2: Create the form container
  Below your heading, add the opening and closing `<form>` tags. All following steps will go *inside* these tags.
* Step 3: Add basic text inputs
  Create a `<label>` and an `<input>` for the user's Name. Remember to link them using the `for` and `id` attributes. Do the same for their Email address, using `type="email"`.
* Step 4: Add a message area
  Below the text inputs, add a `<label>` and a `<textarea>` so the user can write a detailed message.
* Step 5: Add a submit button
  At the bottom of the form, add a `<button type="submit">`. Give it a clear label like "Submit" or "Send".
* Step 6: Preview in the browser
  Open `contact.html` in your browser. Try clicking on your labels to see if your cursor automatically jumps into the corresponding input boxes. Type some text to see how the inputs behave!

## Checkpoints

* [ ] Create a `<form>` container to hold all user input elements.
* [ ] Add at least two different `<input>` elements (e.g., text and email) and use the `placeholder` attribute.
* [ ] Successfully link a `<label>` to an input using the `for` and `id` attributes.
* [ ] Add a `<button>` at the bottom to visually complete the form interface.
