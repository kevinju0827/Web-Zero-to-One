# M16 Deployment

## The "Why?"

Congratulations! You've learned how to structure content with HTML, design beautiful layouts with CSS, use modern tools like Flexbox and Grid, and speed up your workflow with Bootstrap. But so far, your website only lives on your computer.

What's the point of building a masterpiece if no one else can see it? **Deployment** is the process of moving your code from your local machine to a "Web Server"—a computer that is connected to the internet 24/7. Once deployed, anyone in the world with your URL can visit your site!

## Goals

Understand the basic concepts of web hosting and learn how to deploy a static website for free using GitHub Pages.  
By the end of this module, you should be able to push your code to a GitHub repository and enable the Pages feature to make your site live.

## Core Concepts

### 1. Static vs. Dynamic Hosting

*   **Static Hosting**: Used for websites that consist only of HTML, CSS, and JavaScript files (like the ones we built in this course). Examples: GitHub Pages, Netlify, Vercel.
*   **Dynamic Hosting**: Used for sites that require a database and server-side code (like PHP, Python, or Node.js). Examples: AWS, Heroku, DigitalOcean.

### 2. GitHub Pages

GitHub Pages is a free service provided by GitHub that allows you to host static websites directly from your GitHub repository. It is the perfect place for beginners to launch their first portfolio or project.

## Guided Practice

Let's walk through the steps to launch your **"Final Project"** to the world.

### Step-by-Step Instructions

*   **Step 1: Prepare your `index.html`**
    Make sure your main file is named exactly `index.html`. Web servers look for this file by default when someone visits your URL.
*   **Step 2: Commit and Push to GitHub**
    In WebStorm, go to the **Git** menu (or use the terminal). Stage your changes, write a commit message (e.g., "Ready for launch!"), and click **Push**.
*   **Step 3: Enable GitHub Pages**
    Go to your repository on [GitHub.com](https://github.com). Click on **Settings** -> **Pages** (in the left sidebar).
*   **Step 4: Select the Branch**
    Under "Build and deployment", select **Deploy from a branch**. Under "Branch", select `main` and `/ (root)`. Click **Save**.
*   **Step 5: Celebrate!**
    Wait 1-2 minutes. Refresh the page, and you will see a link like `https://username.github.io/repository-name/`. Click it—your site is live!

### Example Code (Deployment Checklist)

```markdown
# Deployment Checklist

1. [ ] Is the main file named `index.html`?
2. [ ] Are all image paths relative? (e.g., `./images/photo.jpg` instead of `C:\Users\Desktop\photo.jpg`)
3. [ ] Did you push the latest changes to the `main` branch?
4. [ ] Did you enable GitHub Pages in the repository settings?
5. [ ] Does the live site look the same as it did on your local machine?
```

## Checkpoints

* [ ] Successfully push your final project code to a new or existing GitHub repository.
* [ ] Enable the GitHub Pages feature in your repository settings.
* [ ] Share your live website URL with at least one friend or family member.
* [ ] Verify that all images and styles load correctly on the live URL.
* [ ] (Optional) Try making a small change to your `index.html`, push it to GitHub, and see it update automatically on the live site after a few minutes!