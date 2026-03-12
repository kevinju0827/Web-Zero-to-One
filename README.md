# Web Zero to One

> From absolute beginner to building modern, aesthetic websites—amplified by AI.

Welcome to **Web Zero to One**.

This course is designed to take you from knowing nothing about code (Zero) to building and shipping your first website (One).  
(The name is inspired by the phrase "Zero to Hero.")

We'll learn how to use AI to generate rapid prototypes, then refine those outputs into more concise and reliable code by learning basic syntax and concepts.

The total estimated time required to complete this course is approximately 30 hours.

## Getting Started

Before you begin this course, please set up the following environment.
> The following tools are not mandatory; you can use any alternative.

### Windows

### MacOS

* Step 1: Install a browser

  Browsers are used to view web pages and come with developer tools that make inspection and debugging easier.  
  Google Chrome is the most popular browser in the world.  
  Download and install [Google Chrome](https://www.google.com/intl/en/chrome/)

* Step 2: Prepare at least one AI Assistant

  AI assistants can generate suitable examples and help solve many of your learning-related problems.  
  Gemini was launched by Google and is offered free of charge.  
  We will use Gemini as our AI assistant throughout the course.  
  Open [Gemini](https://gemini.google.com/) in your browser.  
  If you encounter any problems, you can first ask Gemini to confirm whether it can be resolved.

* Step 3: Install a code editor / IDE

  Code editors and IDEs make it easy to write and debug code.  
  Even if you can use a text editor, code editors and IDEs often offer more features and can significantly improve efficiency.
  JetBrains is a leading provider of IDEs and tools.  
  Download and install [JetBrains WebStorm](https://www.jetbrains.com/webstorm/).  

* Step 4: Clone this repository

  Git is a version control system that allows you to easily update the course materials.  
  Download and install [Git](https://git-scm.com/).  
  Open your WebStorm and click the `Clone Repository` button.  
  Copy the URL of this repository: `https://github.com/kevinju0827/Web-Zero-to-One.git` and paste the URL into the field.  
  Click the `Clone` button to download the repository to your local machine.  
  Next time you want to update the course materials, you can simply click the `Update Project` button to pull the latest changes.

* Step 5: Open the `README.md` file

  `README.md` is the first file you should see when you open the repository.
  Open the `Web-Zero-to-One` repository in your WebStorm and click the `README.md` file to open it.  
  Switch to the `Preview` tab at the top right to view the content.
  
  > `.md` stands for Markdown, which is a lightweight markup language that allows you to write formatted text using a simple syntax.  
  > It is not necessary to understand Markdown to follow along with this course.  
  > You can refer to the [Markdown Guide](https://www.markdownguide.org/basic-syntax/) for a quick introduction.
  
  In every module, we will also provide a `README.md` file as a learning guide.

## Philosophy

**AI is best suited for handling common requirements, boilerplate code, or building rapid prototypes.**

In the age of AI, coding has changed. You don't need to hand-code every single line anymore.

However, because AI works with limited context, it can struggle to account for the full details of large-scale projects or handle highly specific, complex business logic.

**To use AI effectively, you cannot rely on it blindly.**

The core focus of this course is to equip you with the **understanding of programming concepts, control flow, and basic syntax**.

This fundamental knowledge is the minimum requirement for you to review, modify, and fix the AI-generated content when it occasionally hallucinates or makes logical errors.

## Curriculum Structure

The repository is organized into modules. Each module in this course is designed as a self-contained learning journey, moving from conceptual understanding to practical mastery.

To ensure a consistent and effective learning experience, each module includes the following:

1. **The "Why?"**  
   Before diving into the code, we answer the most important question: Why are we learning this?  
   You will explore how these concepts are applied in real-world situations.
2. **Goals**  
   The goals serve as your learning objectives for this module.   
   Written in plain, accessible language, these goals define what you should understand and be able to articulate by the end of the module.
3. **Core Concepts**  
   This is the heart of the module. Core Concepts provides a deep-dive explanation of programming syntax and technical concepts.  
   It includes detailed explanations and code demonstrations for each topic.
4. **Guided Practice**  
   To make each module easier to follow, we also provide a step-by-step walkthrough.  
   This section is designed to guide you through a small but complete practice sequence, allowing you to apply what you just learned in a concrete way.  
   By following the execution flow, you will:
   - know exactly where to start
   - produce a small example that demonstrates the core concepts of the module
5. **Checkpoints**  
   Checkpoints are designed to verify your learning through practical scripting.  
   Successfully completing these checkpoints serves as proof of your technical competency and readiness for the next module.  
   > **There is no single "correct" answer for the checkpoints.**  
   > Programming is about problem-solving. Since we embrace AI tools for code generation, success is defined by your ability to **explain** your logic, handle errors, and **modify** your code confidently.  
   > Please do not consider a checkpoint "done" just because AI produced an output.

## Tech Stack

### Languages

- **HTML5**  
  The standard markup language for structuring web content with semantic elements (headings, sections, forms, and media).
- **CSS3**  
  The styling language for designing layouts, typography, and responsive, modern-looking web pages across devices.

#### A Note on JavaScript

This course intentionally excludes in-depth JavaScript instruction.

The JavaScript ecosystem is vast and introduces a higher layer of complexity.

While it is essential for building fully dynamic websites, we recommend mastering the foundational skills in this course before diving in.

You may encounter small amounts of JavaScript in this course (often generated by AI), but **proficiency is not required**.

If you are interested in learning more, please refer to the external links in the **Recommended Resources** section.

### Frameworks

- **[Bootstrap 5](https://getbootstrap.com/)**  
  One of the most popular frontend frameworks. It provides pre-built CSS components (like buttons, navbars, and grids) to help you build responsive, mobile-first sites quickly.

### Tools

#### Browser

- **[Google Chrome](https://www.google.com/intl/en/chrome/)**  
  The browser of choice for web developers. Its built-in **Developer Tools** are essential for inspecting code, debugging, and testing responsive designs.

#### Integrated Development Environment(IDE)

- **[JetBrains WebStorm](https://www.jetbrains.com/webstorm/)**  
  A powerful IDE designed specifically for web development. It has a strong understanding of your project structure right out of the box.
  - **[JetBrains AI](https://www.jetbrains.com/ai-ides/)**  
    An integrated AI assistant that provides code generation, explanations, and refactoring tools seamlessly in WebStorm.
  - **[Junie](https://www.jetbrains.com/junie/)**  
    An AI coding assistant for JetBrains IDEs, focusing on advanced code completion and predictive assistance.
- **[Visual Studio Code](https://code.visualstudio.com/)**  
  The industry-standard code editor. It is lightweight, free, and supports a massive ecosystem of extensions.
  - **[GitHub Copilot Chat](https://github.com/microsoft/vscode-copilot-chat)**  
    The AI pair programmer for VS Code. You can chat with it to generate code, explain concepts, or fix bugs directly in your editor.

#### AI

- **[Gemini](https://gemini.google.com/)**  
    Google’s AI assistant for brainstorming, explaining concepts, and generating code or content from prompts.

#### Assets

- **[Pixabay](https://pixabay.com/)**  
  A huge collection of royalty-free stock photos, illustrations, and vectors. Perfect for finding specific visuals without copyright hassles.
- **[unDraw](https://undraw.co/)**  
  Open-source illustrations that you can customize to match your brand color. Perfect for giving your project a modern, tech-savvy look.
- **[Animista](https://animista.net/)**  
  An on-demand CSS animation library. Visually tweak animations and generate the code instantly—perfect for adding "vibe" to your site.

## Recommended Resources

(Optional) In addition to the resources provided within this repository, we highly recommend learning from and utilizing the following:

- **[roadmap.sh Frontend Developer](https://roadmap.sh/frontend)**  
  A visual guide to the developer landscape. Use this to track your progress and understand how different technologies fit together in the frontend ecosystem.
- **[W3Schools](https://www.w3schools.com)**  
  The "dictionary" of web development. It provides simple, isolated examples. Great for quick syntax lookups or when you need to check if a specific HTML tag or CSS property actually exists.
- **[MDN Web Docs](https://developer.mozilla.org)**  
  The gold standard documentation by Mozilla. If you need a deeper, more technical explanation of how the browser works, look here.
- **[Atguigu HTML5+CSS3](https://youtu.be/E-DErp0IcA0?list=PLmOn9nNkQxJGGuwYhQzTmRGFwF9cHYS-x)**  
  Comprehensive and free video tutorials in Chinese. An excellent choice if you prefer learning complex concepts through video content in Mandarin.
- **[Flexbox Froggy](https://flexboxfroggy.com)**  
  A game where you help Froggy and friends by writing CSS code. The most fun and intuitive way to master Flexbox layouts.
- **[CSS Grid Garden](https://cssgridgarden.com)**  
  Similar to Flexbox Froggy, but for CSS Grid. Essential for practicing modern grid-based web layouts.

## License

Distributed under the MIT License. See `LICENSE` for more information.