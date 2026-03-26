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

* Step 1: Set Up Your Recipe Page  
  Create a new HTML file named `recipe.html` and add the standard HTML document structure.  
  At the top of the page, include an `<h1>` heading such as `<h1>Homemade Pancakes</h1>`.  
  You may also add a short introduction below the title to briefly describe the recipe.

* Step 2: Create a Shopping List  
  Add an `<h2>` heading such as `<h2>Shopping List</h2>`.  
  Then build a `<table>` to display the ingredients you need to buy.  
  Include the item name, quantity, and unit price, and add a final row that shows the total price.  
  Example columns:
  - Item
  - Quantity
  - Unit Price
  - Total

* Step 3: Write the Cooking Instructions with an Ordered List  
  Below the shopping list, add another `<h2>` heading such as `<h2>Cooking Instructions</h2>`.  
  Use an `<ol>` to write the recipe steps in the correct order.  
  Place each step inside an `<li>` so the instructions are easy to follow from start to finish.  
  Make sure the steps flow naturally, such as preparing the ingredients, mixing the batter, cooking, and serving.

* Step 4: Preview and Review  
  Open `recipe.html` in your browser and check that the shopping list appears as a clear table and the cooking instructions are displayed as a numbered list.  
  If needed, refine the wording so the recipe feels complete, smooth, and easy to read.

## Checkpoints

* [ ] Create an HTML travel planner page that includes a packing list, trip dates, a simple itinerary, and a few general travel tips or recommendations.