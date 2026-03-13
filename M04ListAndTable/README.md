# M04 List and Table

## The "Why?"

Up to this point, you've learned how to write text, format it, and link out to other resources. But what happens when you need to display structured information? 

Imagine reading a recipe where the ingredients are written in one massive paragraph, or trying to compare the pricing of three different software plans without a grid to separate the features. It would be incredibly difficult to read. 

HTML provides specific elements for grouping related items (Lists) and displaying data in a grid of rows and columns (Tables). By mastering these, you can present structured data—like step-by-step instructions, navigation menus, or schedules—in a clean, readable, and organized way.

## Goals

Understand the concept of nested HTML elements and how to use them to structure groups of data.  
By the end of this module, you should be able to create bulleted lists, numbered lists, and build a structured data table using rows and columns.

## Core Concepts

Unlike simple elements like `<p>` or `<h1>`, lists and tables require **nested elements** (elements placed inside other elements) to work properly. You need a "parent" element to define the container, and "child" elements to define the individual items inside it.

### Unordered Lists: `<ul>` and `<li>`

An unordered list is used when the order of the items does not matter. By default, browsers display these items with bullet points.

- `<ul>` (Unordered List): The parent container.
- `<li>` (List Item): The individual item inside the list.

Example:
```html
<ul>
  <li>Apples</li>
  <li>Bananas</li>
  <li>Oranges</li>
</ul>

```

### Ordered Lists: `<ol>` and `<li>`

An ordered list is used when the sequence of the items is important, such as a top 3 ranking or a recipe's instructions. Browsers automatically number these items.

* `<ol>` (Ordered List): The parent container.
* `<li>` (List Item): The individual item, just like in the unordered list.

Example:

```html
<ol>
  <li>Preheat the oven to 180°C.</li>
  <li>Mix the ingredients.</li>
  <li>Bake for 20 minutes.</li>
</ol>

```

### Tables: `<table>`, `<tr>`, `<th>`, and `<td>`

A table is used to display data in a two-dimensional grid of rows and columns. Building a table requires a few different tags working together:

* `<table>`: The main parent container for the entire table.
* `<tr>` (Table Row): Defines a single horizontal row.
* `<th>` (Table Header): Defines a header cell, usually bold and centered by default. Used for column or row titles.
* `<td>` (Table Data): Defines a standard data cell.

To build a table, you create a `<table>`, then add rows (`<tr>`), and inside those rows, you add your cells (`<th>` or `<td>`).

Example:

```html
<table>
  <tr>
    <th>Name</th>
    <th>Age</th>
  </tr>
  <tr>
    <td>Alice</td>
    <td>25</td>
  </tr>
  <tr>
    <td>Bob</td>
    <td>30</td>
  </tr>
</table>

```

*(Note: Without CSS styling, standard HTML tables will not have visible borders by default, but the data will still be aligned in a grid.)*

## Guided Practice

* Step 1: Set up your file
  Create a new HTML file named `data.html` with the standard document skeleton. Add an `<h1>` heading at the top, like `<h1>My Favorite Recipes and Schedule</h1>`.
* Step 2: Create an Unordered List
  Think of a meal you like. Add an `<h2>` heading for "Ingredients", and below it, create a `<ul>` containing at least three `<li>` elements for the ingredients.
* Step 3: Create an Ordered List
  Below your ingredients, add an `<h2>` for "Instructions". Create an `<ol>` with at least three `<li>` steps explaining how to make the meal.
* Step 4: Build a Table
  Let's create a simple weekly schedule. Add an `<h2>` for "My Schedule".
  Create a `<table>`.
  Add a first row (`<tr>`) and put three headers (`<th>`) inside it: "Day", "Morning", and "Afternoon".
  Add two more rows (`<tr>`), and fill them with data (`<td>`) matching those columns (e.g., "Monday", "Work", "Gym").
* Step 5: Preview in the browser
  Open `data.html` in your browser. Verify that your ingredients have bullet points, your instructions have numbers, and your schedule is aligned in columns.

## Checkpoints

* [ ] Successfully create an unordered list (`<ul>`) with at least three list items (`<li>`).
* [ ] Successfully create an ordered list (`<ol>`) with at least three list items (`<li>`).
* [ ] Build a table (`<table>`) containing at least one header row (using `<th>`) and two data rows (using `<td>`).
