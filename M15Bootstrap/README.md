# M15 Bootstrap

## The "Why?"

By now, you've learned how to build everything from scratch—containers, grids, flexboxes, and responsive layouts. But in the professional world, time is money. Building every single button, navigation bar, and card from zero for every project is slow and repetitive.

**Bootstrap** is a powerful, "batteries-included" frontend framework that provides pre-built CSS components and a robust responsive grid system. It allows you to build professional-looking, mobile-first websites in a fraction of the time. Instead of writing 50 lines of CSS for a button, you just add a class like `btn btn-primary`.

## Goals

Learn how to integrate Bootstrap into your project and utilize its pre-built components and utility classes to speed up development.  
By the end of this module, you should be able to include Bootstrap via CDN, build layouts using the Bootstrap grid, and customize Bootstrap components to suit your needs.

## Core Concepts

### 1. Including Bootstrap

The easiest way to start is by adding the **CDN link** (Content Delivery Network) to your HTML `<head>`. This tells the browser to download the Bootstrap CSS file from a fast, global server.

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
```

### 2. The Bootstrap Grid

Bootstrap's grid is based on Flexbox and uses a 12-column system:
*   **`.container`**: Centers your content and adds padding.
*   **`.row`**: A horizontal wrapper for columns.
*   **`.col-X`**: A column that spans `X` out of 12 slots.
*   **Responsive columns**: Use classes like `.col-md-6` (takes 6 slots on medium screens and above, but stacks to 12 slots on mobile).

### 3. Components and Utilities

Bootstrap provides hundreds of pre-styled items:
*   **Components**: `.navbar`, `.card`, `.btn`, `.modal`, `.carousel`.
*   **Utilities**: Quick classes for spacing (`m-3`, `p-2`), colors (`text-primary`, `bg-light`), and alignment (`text-center`).

## Guided Practice

Let's build a **"Rapid Landing Page"** using Bootstrap to create a hero section and a feature grid.

### Step-by-Step Instructions

*   **Step 1: Link Bootstrap**
    Add the Bootstrap CSS and JS CDN links to your HTML file.
*   **Step 2: Create a Navbar**
    Copy a basic Navbar component from the Bootstrap documentation and paste it at the top of your `<body>`.
*   **Step 3: Build the Hero Section**
    Use a `div` with classes `bg-light p-5 rounded-lg m-3` to create a prominent hero area (previously called a Jumbotron).
*   **Step 4: Create a Responsive Grid**
    Use `.container`, `.row`, and `.col-md-4` to create a 3-column feature section that automatically stacks on mobile.
*   **Step 5: Use Bootstrap Cards**
    Inside each column, add a `.card` component with an image, title, and a `.btn-primary`.

### Example Code

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bootstrap Practice</title>
    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>

    <!-- Navbar Component -->
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
      <div class="container">
        <a class="navbar-brand" href="#">FastSite</a>
        <div class="navbar-nav ms-auto">
          <a class="nav-link active" href="#">Home</a>
          <a class="nav-link" href="#">Features</a>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <div class="container my-5">
      <div class="p-5 text-center bg-light rounded-3">
        <h1 class="text-primary">Built with Bootstrap</h1>
        <p class="lead">Beautiful, responsive sites in half the time.</p>
        <button class="btn btn-primary btn-lg">Get Started</button>
      </div>
    </div>

    <!-- Feature Grid -->
    <div class="container">
      <div class="row g-4">
        <div class="col-md-4">
          <div class="card h-100">
            <div class="card-body">
              <h5 class="card-title">Responsive</h5>
              <p class="card-text">Works on any device automatically.</p>
            </div>
          </div>
        </div>
        <div class="col-md-4">
          <div class="card h-100">
            <div class="card-body">
              <h5 class="card-title">Pre-built</h5>
              <p class="card-text">Dozens of components ready to go.</p>
            </div>
          </div>
        </div>
        <div class="col-md-4">
          <div class="card h-100">
            <div class="card-body">
              <h5 class="card-title">Customizable</h5>
              <p class="card-text">Easily tweak colors and spacing.</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Bootstrap Bundle with Popper JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
```

## Checkpoints

* [ ] Successfully include Bootstrap 5 in your project via a CDN link in the `<head>` section.
* [ ] Implement Bootstrap's grid system classes (`.container`, `.row`, `.col`) to build a responsive layout that changes based on screen size.
* [ ] Replace custom-built UI components with at least two different pre-built Bootstrap components (e.g., a Navbar and Buttons).
* [ ] Use Bootstrap Utility classes (like `m-5`, `p-2`, `text-center`, `bg-dark`) to modify spacing and appearance without writing custom CSS.
* [ ] Create a "Product Card" using the Bootstrap `.card` component, including an image, title, text, and a button.