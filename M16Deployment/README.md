# M16 Deployment

## The "Why?"

Congratulations—you've reached the final module. You can now structure pages with semantic HTML, style them with the CSS box model, build layouts with Flexbox and Grid, make them responsive with media queries, and accelerate everything with Bootstrap.

But so far, your masterpiece only exists on your own computer. The HTML file lives somewhere on your hard drive and no one else in the world can see it. A site that no one can visit is just a clever local document.

**Deployment** is the step that fixes that. It is the process of moving your files from your local machine to a **web server**—a computer that is connected to the internet 24/7 and serves your site to anyone with the URL. The best part: for a static site like the ones we built in this course, deployment is **completely free** thanks to services like GitHub Pages, Netlify, and Vercel. Within five minutes of finishing this module, your site can be live on the public internet with a real URL you can share.

## Goals

Understand the difference between static and dynamic hosting, and learn how to deploy a static website for free using GitHub Pages.  
By the end of this module, you should be able to prepare a project for deployment (correct file naming, relative paths, no broken assets), push it to a GitHub repository, enable GitHub Pages, and verify the live site loads correctly on a public URL you can share.

## Core Concepts

### 1. What Is a "Web Server"?

A web server is just a computer that is **always online**, listening for HTTP requests, and ready to send back HTML, CSS, JavaScript, and image files to anyone who asks. Your home Wi-Fi router could technically do this, but in practice we use cloud-hosted services so we don't have to worry about uptime, security, bandwidth, or the electricity bill.

### 2. Static vs. Dynamic Hosting

This distinction decides which kind of hosting service you can use.

* **Static hosting** — the server simply hands out the exact same HTML, CSS, JS, and image files to every visitor. Nothing is generated on the fly. This is what everything you built in this course needs. Hosts: **GitHub Pages**, **Netlify**, **Vercel**, **Cloudflare Pages**. All are free for personal projects.
* **Dynamic hosting** — the server runs code (PHP, Python, Node.js, Ruby, etc.) and talks to a database to build a different page for every request. Used for things like full-stack apps, blogs with logins, and e-commerce sites. Hosts: **AWS**, **Heroku**, **DigitalOcean**, **Render**. These usually cost money once you exceed a small free tier.

Since every project in this course is HTML + CSS + a sprinkle of JS, **static hosting is exactly what we need**.

### 3. GitHub Pages

GitHub Pages is a free service built into every GitHub account. It takes the contents of one of your repositories and publishes it as a public website at `https://<your-username>.github.io/<repository-name>/`.

You get:

* A public URL you can share.
* Automatic redeployment every time you push a commit to GitHub.
* Free HTTPS (the little padlock icon next to the URL).
* Optional support for a custom domain (e.g. `myportfolio.com`) if you own one.

### 4. The "Final Project" Convention

Every web server has a default file it serves when someone visits the root URL. That file is **`index.html`**. If you visit `https://example.com/`, the server is really sending you `https://example.com/index.html`—you just don't see it in the address bar.

This means your main page **must be named exactly `index.html`** (all lowercase, no spaces, no `.htm`). Anything else and the deployment will show a blank "404 Not Found" page.

### 5. Absolute vs. Relative Paths

This is the single most common cause of "it worked on my machine but the live site is broken." When you reference an image, a stylesheet, or another page, use **relative paths**:

```html
<!-- BAD: absolute path to your hard drive — will never work on the live site -->
<img src="C:\Users\Alex\Desktop\photos\hero.jpg">

<!-- BAD: absolute file URL -->
<img src="file:///D:/projects/site/hero.jpg">

<!-- GOOD: relative path — works locally AND on the live server -->
<img src="./images/hero.jpg">
<img src="images/hero.jpg">
```

Relative paths describe **where the file is in relation to the HTML file**, which stays the same no matter what computer is hosting it.

## Guided Practice

In this practice, we will treat the portfolio site you built at the end of M15 like a **real product launch**. Putting files on GitHub Pages is only the first step — a *production-quality* deployment also makes the site shareable on social media, handles broken URLs gracefully, and passes a basic performance audit. By the end of this walkthrough you will have a live, polished site you can actually put on your résumé.

* Step 1: Audit the Project Locally Before Pushing

  The single fastest way to ship a broken site is to deploy first and audit later. Five minutes of local checks save hours of "why is it 404ing only on the live URL" debugging.
  * Open your portfolio folder in WebStorm. Verify:
    * Your main page is named exactly `index.html` (all lowercase, no spaces, no `.htm`).
    * Every asset lives in a sensible subfolder, e.g. `images/`, `css/`, `js/`.
    * Every `src` and `href` attribute uses a **relative** path (`images/profile.jpg`), never an absolute one (`C:\Users\...` or `file:///D:/...`).
  * In WebStorm's built-in terminal, run:
  ```bash
  ls
  ```
  * **Observation:** Confirm `index.html` is visible at the root of the folder. If it's inside a `src/` or `dist/` subfolder, GitHub Pages won't find it without extra configuration.

* Step 2: Add Open Graph Meta Tags (so the site looks good when shared)

  When someone pastes your portfolio URL into Slack, Twitter, WhatsApp, or LinkedIn, the platform fetches your `<head>` and looks for **Open Graph (OG)** meta tags. Without them, your link shows up as a sad gray rectangle. With them, it shows a polished preview card with your name, tagline, and a hero image — and that is what every recruiter sees first.
  * Inside the `<head>` of `index.html`, add:
  ```html
  <!-- Page metadata -->
  <title>Alex Chen — Frontend Developer Portfolio</title>
  <meta name="description" content="I build fast, accessible web interfaces. Portfolio, projects, and contact.">

  <!-- Open Graph (Facebook, LinkedIn, Slack, WhatsApp) -->
  <meta property="og:title" content="Alex Chen — Frontend Developer">
  <meta property="og:description" content="I build fast, accessible web interfaces.">
  <meta property="og:image" content="https://alexchen.github.io/my-portfolio/images/og-cover.jpg">
  <meta property="og:url" content="https://alexchen.github.io/my-portfolio/">
  <meta property="og:type" content="website">

  <!-- Twitter / X -->
  <meta name="twitter:card" content="summary_large_image">
  <meta name="twitter:title" content="Alex Chen — Frontend Developer">
  <meta name="twitter:description" content="I build fast, accessible web interfaces.">
  <meta name="twitter:image" content="https://alexchen.github.io/my-portfolio/images/og-cover.jpg">

  <!-- Favicon -->
  <link rel="icon" type="image/png" href="favicon.png">
  ```
  * Place a `1200×630px` image at `images/og-cover.jpg` (Pixabay, unDraw, or a screenshot of your hero section all work fine).
  * **Observation:** The `og:image` URL must be **absolute** (start with `https://...`), not relative. Social platforms fetch the image from the open internet — they can't resolve a relative path. This is the one exception to the "relative paths everywhere" rule.

* Step 3: Add a Custom 404 Page

  Sooner or later, someone will visit a broken URL on your site (a stale tweet, a typo, an outdated bookmark). By default they'll see GitHub's generic "404 — File not found" page. A custom `404.html` lets you control that experience — show a witty message, link them back to the homepage, and keep them on your site.
  * Create a new file at the root of your project: `404.html`.
  * Add minimal content:
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>404 — That page wandered off</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
  </head>
  <body class="bg-dark text-light d-flex align-items-center" style="min-height:100vh;">
    <div class="container text-center">
      <div class="display-1 fw-bold text-warning">404</div>
      <h1 class="display-5 mb-3">That page wandered off.</h1>
      <p class="lead opacity-75 mb-4">Either the URL is wrong, or something on the site is broken and I should know about it.</p>
      <a href="/" class="btn btn-warning btn-lg">← Back to the homepage</a>
    </div>
  </body>
  </html>
  ```
  * **Observation:** GitHub Pages has a special rule — if a file named `404.html` exists at the root of your repository, it gets served automatically for any URL that doesn't match an existing file. No configuration needed.

* Step 4: Push to GitHub and Enable Pages

  Now we ship.
  * On [github.com](https://github.com), click the green **New** button and create a public repository named `my-portfolio` (or whatever you like — but lowercase and hyphenated is conventional). Do **not** check "Add a README".
  * In WebStorm's terminal, from inside your project folder, run these commands one at a time, replacing the URL on the third line with the one shown on your new repo's page:
  ```bash
  git init
  git add .
  git commit -m "Initial portfolio launch"
  git branch -M main
  git remote add origin https://github.com/<your-username>/my-portfolio.git
  git push -u origin main
  ```
  * In your repository on GitHub, click **Settings → Pages** in the left sidebar.
  * Under **Build and deployment**, set **Source** to **Deploy from a branch**, then choose `main` and `/ (root)`. Click **Save**.
  * **Observation:** Within 1–2 minutes, the Pages settings page shows a green banner with your live URL: `https://<your-username>.github.io/my-portfolio/`. If you refresh and the link returns 404, wait another minute — the very first deployment can take a while to propagate.

* Step 5: Verify the Live Site With DevTools (the production checklist)

  Local works ≠ production works. Always verify on the actual deployed URL.
  * Open the live URL in Chrome.
  * Press **F12** to open Developer Tools.
  * Switch to the **Network** tab and reload the page (`Ctrl + R`). Scan the request list:
    * Every row should show a green status (200) — **no red 404s**.
    * Especially watch for case-mismatched paths: `Images/Photo.JPG` works on Windows locally but **fails on GitHub Pages**, whose Linux servers are case-sensitive.
  * Switch to the **Console** tab. There should be **no red error messages**.
  * Press `Ctrl + Shift + M` to open the Device Toggle. Test at 375px, 768px, and 1280px — confirm no horizontal overflow, all images load, and the hamburger menu still works.
  * **Observation:** This 60-second pass catches 90% of "but it worked locally" deploy bugs. Get in the habit of doing it after every push.

* Step 6: Verify the Social Preview Card

  Now confirm the OG tags you wrote in Step 2 actually render the way you intended on other platforms.
  * Visit Meta's [Sharing Debugger](https://developers.facebook.com/tools/debug/) (it works for any OG tags, not just Facebook).
  * Paste your live URL into the input field and click **Debug**.
  * Inspect the preview card it generates. Verify the title, description, and image are all correct.
  * If anything looks wrong, click **Scrape Again** after fixing it on your site — social platforms aggressively cache OG data, so this button is essential.
  * **Observation:** Many platforms (LinkedIn especially) cache OG previews for *days*. The Sharing Debugger is the way to force a re-scrape so your changes show up immediately when you share.

* Step 7: Run a Lighthouse Performance Audit

  Lighthouse is a free, built-in Chrome tool that rates your site on Performance, Accessibility, Best Practices, and SEO — the same scores Google uses when ranking pages.
  * On your live URL, open DevTools (F12) and click the **Lighthouse** tab.
  * Select **Mobile**, check all four categories, and click **Analyze page load**.
  * **Observation:** Aim for **90+ in every category**. Anything red (Performance under 50, Accessibility under 90) is worth fixing before you put the URL on your résumé. Common quick wins:
    * Add `alt` text to every `<img>` (huge Accessibility bump).
    * Specify `width` and `height` attributes on images (Performance — prevents layout shift).
    * Convert oversized hero images from JPG to WebP.
    * Add a `lang` attribute on `<html>`.

* Step 8: Ship an Update and Watch It Redeploy

  GitHub Pages auto-redeploys on every push to `main`. Get one cycle under your belt so the workflow feels routine.
  * Change a piece of text in `index.html` — a tagline, a section heading, anything visible.
  * In the terminal, run:
  ```bash
  git add .
  git commit -m "Update homepage tagline"
  git push
  ```
  * **Observation:** Wait ~30 seconds, refresh your live URL, and see the change appear. This — `edit → commit → push → live` — is the deployment workflow you'll use for the rest of your career, from your portfolio to a billion-dollar product.

## Checkpoints

* [ ] Production-Launch Your Portfolio Site  
      Take the portfolio you built at the end of M15 and deploy it to the public internet at a quality you'd be comfortable putting on a résumé or LinkedIn. Every requirement below must be verified on the **live URL** — not on your local machine:
      * **Correct File Layout**: Your main page is named exactly `index.html` at the root of the repository. Every asset path is **relative** and **case-correct** (verify on the deployed URL, not just locally — GitHub Pages servers are case-sensitive even if your laptop is not).
      * **Live on GitHub Pages**: The site is publicly reachable at `https://<your-username>.github.io/<repo-name>/`. Open it from a different browser or from your phone over mobile data to confirm it really is public.
      * **Clean Network Panel**: Open the live site in Chrome, press F12, and reload with the Network tab open. There must be **zero 404 (red) entries** and **zero red Console errors**.
      * **OG / Social Preview Card**: Add Open Graph + Twitter Card meta tags to your `<head>`, including a `1200×630` cover image stored in the repository. Paste your live URL into Meta's [Sharing Debugger](https://developers.facebook.com/tools/debug/) and screenshot the rendered preview card — the title, description, and image must all be the ones you wrote.
      * **Custom 404 Page**: Create a `404.html` file at the root of the repository. Visit any non-existent URL on your live site (e.g. `https://<your-user>.github.io/<repo>/this-does-not-exist`) and confirm your custom 404 page renders, with a link back to the homepage.
      * **Lighthouse Score**: Run a Chrome DevTools Lighthouse audit on the live URL in **Mobile** mode. Score **at least 90** in **Accessibility**, **Best Practices**, and **SEO**. (Performance can be harder if you use a lot of large images — aim for at least 75 there.) Fix any easy wins Lighthouse flags before considering the checkpoint complete.
      * **Continuous Deployment Drill**: Make one visible change locally (a color, a tagline, a project description), commit it with a clear message, and push to `main`. Refresh the live URL one minute later and confirm the change is live. This proves your auto-deploy pipeline works end-to-end.
      * **Share It (this is the actual point of deployment)**: Send the live URL to **at least two** other people — a friend, a classmate, a recruiter, a community Discord. The whole reason we deploy is to give the work an audience. A site that no one visits is just a folder on a hard drive with a fancier address.
