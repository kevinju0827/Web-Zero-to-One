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

### Single-Line Inputs: `<input>`

The `<input>` tag is the most versatile element in forms. Like `<img>`, it is an empty tag (it does not have a closing tag). Its behavior completely changes based on its `type` attribute.

Common types include:
* `type="text"`: Standard single-line text (e.g., a username).
* `type="email"`: Text field that expects an email address format.
* `type="password"`: Hides the characters as the user types.
* `type="number"`: Restricts input to numbers (can use `min` and `max`).
* `type="tel"`: Used for phone numbers.
* `type="date"`: Provides a date picker interface.
* `type="file"`: Allows the user to select and upload a file.
* `type="color"`: Provides a color picker interface.
* `type="radio"`: Allows the user to select only one option from a group.
* `type="checkbox"`: Allows the user to select multiple options.

You can also use the `required` attribute to ensure a field is not left empty.
You can also use the `placeholder` attribute to display a temporary hint inside the box before the user types.

Example:

```html
<input type="text" placeholder="e.g. John Doe">
<br>
<input type="password" placeholder="Enter your password">
```

### Describing Inputs: `<label>`

A `<label>` tells the user what information belongs in a specific input field. 
More importantly, labels improve accessibility. When you correctly link a label to an input, clicking the text of the label will automatically focus the input box. You link them by matching the label's `for` attribute with the input's `id` attribute.

Example:

```html
<label for="username">Name:</label>
<input type="text" id="username" placeholder="e.g. John Doe">
<br>
<label for="password">Password:</label>
<input type="password" id="password" placeholder="Enter your password">
```

### Grouping Elements: `<fieldset>` and `<legend>`

When forms get longer, it is helpful to group related pieces of information together. The `<fieldset>` element acts as a container that groups related inputs and labels, often drawing a visual box around them by default. 

To give this grouped section a descriptive title, use the `<legend>` element. The `<legend>` must be the very first element inside the `<fieldset>`. This pairing not only makes your form visually organized but also greatly improves accessibility, especially when grouping things like radio buttons or checkboxes.

Example:

```html
<fieldset>
    <legend>Contact Preferences</legend>
    
    <input type="radio" id="emailPref" name="contact_method">
    <label for="emailPref">Email</label><br>
    
    <input type="radio" id="smsPref" name="contact_method">
    <label for="smsPref">Text Message</label>
</fieldset>
```

### Dropdown Lists: `<select>` and `<option>`

When you want users to choose from a list of options without taking up much space, use a dropdown menu.

* `<select>`: The container for the dropdown.
* `<option>`: The individual choices inside the dropdown.

Example:

```html
<label for="city">Choose a city:</label>
<select id="city">
  <option value="tokyo">Tokyo</option>
  <option value="paris">Paris</option>
  <option value="newyork">New York</option>
</select>
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
> Note: Clicking this button will usually refresh the page by default. Because we are only building the visual interface in this course, we won't be writing the code to actually send the data!

## Guided Practice

* Step 1: Set up your file
  Create a new HTML file named booking.html with the standard document skeleton. Add an `<h1>` heading like `<h1>Flight Booking Form</h1>`.

* Step 2: Create the form container
  Below your heading, add the opening and closing `<form>` tags. All following steps will go inside these tags.

* Step 3: Add personal information fields
  Use a `<fieldset>` and a `<legend>` (e.g., "Personal Information") to create a section for the passenger's basic details. 
  Add `<label>` and `<input>` elements for Full Name (`type="text"`), Email (`type="email"`), Phone Number (`type="tel"`), Date of Birth (`type="date"`), and a Passport Photo upload (`type="file"`). 
  Remember to link them using the for and id attributes. Use required and placeholder attributes where appropriate.

* Step 4: Add flight and cabin selection
  Create a section for the flight details. 
  Add a `<select>` dropdown menu for the Destination (e.g., Tokyo, Paris, New York). 
  Add an `<input type="number">` for the Number of Passengers, restricting it with `min="1"` and `max="10"`. 
  Then, add a group of radio buttons (`type="radio"`) for Cabin Class (Economy, Business, First Class). 
  Ensure all three radio buttons share the exact same name attribute so the user can only select one.

* Step 5: Add custom services and requests
  Create a section for extra services. 
  Add multiple checkboxes (`type="checkbox"`) for add-ons like "In-flight Meal", "Lounge Access", or "Extra Baggage".
  Add an `<input type="color">` so the user can choose a preferred color for their printable luggage tags. 
  Below that, add a `<label>` and a `<textarea>` so the user can type out any special requests or dietary restrictions.

* Step 6: Add confirmation and submit buttons
  At the bottom of the form, add a final checkbox (`type="checkbox"`) requiring the user to agree to the Terms and Conditions (make this one required). 
  Finally, add two buttons: `<button type="submit">` labeled "Confirm Booking," and `<button type="reset">` labeled "Clear Form."

* Step 7: Preview in the browser
  Open booking.html in your browser. Click on your labels to ensure your cursor automatically jumps into the corresponding input boxes. 
  Try typing text, picking a date, selecting a color, and clicking the "Confirm Booking" button to see how the HTML5 built-in validation behaves!

## Checkpoints

* [ ] Create an HTML event registration form that includes fields for personal contact details, a dropdown for ticket type selection, 
      checkboxes for optional workshops, a text area for special accommodations, and a mandatory terms of service agreement before submission. 
      Use `<fieldset>` and `<legend>` to group related sections logically.