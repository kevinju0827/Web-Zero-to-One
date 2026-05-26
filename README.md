# Web: Zero to One

![16 Modules](https://img.shields.io/badge/Modules-16-6366f1?style=flat-square)
![~35 Hours](https://img.shields.io/badge/Time-~35_hours-60a5fa?style=flat-square)
![Beginner Friendly](https://img.shields.io/badge/Level-Beginner_Friendly-4ade80?style=flat-square)
![HTML + CSS](https://img.shields.io/badge/Stack-HTML_%2B_CSS-f97316?style=flat-square)
![License: MIT](https://img.shields.io/badge/License-MIT-94a3b8?style=flat-square)

> From absolute beginner to building and shipping your first modern website — amplified by AI.

This course takes you from knowing nothing about web development (**Zero**) to building and deploying a real website (**One**). Each module is a self-contained step, introducing new HTML and CSS concepts through guided examples and practical challenges — with AI tools woven in throughout.

No prior coding experience required. No build tools, no package managers, no JavaScript framework. Every file in this course opens directly in a browser.

---

## Philosophy

**AI is best at handling common patterns, boilerplate, and rapid prototypes.**

In the age of AI, you do not need to hand-write every line. But AI works with limited context — it can miss project-specific requirements, generate outdated patterns, or confidently produce wrong code.

**To use AI effectively, you cannot rely on it blindly.**

This course builds the foundational knowledge you need to *review*, *modify*, and *fix* what AI produces. You will learn to spot when code is incorrect, understand why, and know how to correct it. That skill — not the ability to write HTML from memory — is what this course is actually developing.

---

## Getting Started

Complete these steps before opening any module.

### Step 1: Install a browser

Chrome is the recommended browser for this course. Its built-in **DevTools** (opened with `F12`) are essential for inspecting, debugging, and experimenting with your HTML and CSS in real time.

[Download Google Chrome](https://www.google.com/intl/en/chrome/)

> **Opening HTML files:** Every file in this course can be viewed by simply opening it in Chrome — drag the `.html` file onto the browser window, or right-click → Open with → Chrome. No local server or command line needed.

---

### Step 2: Install a code editor

A code editor provides syntax highlighting, auto-completion, and live file previews that make writing HTML and CSS significantly faster.

**Option A — WebStorm (recommended)**  
A full-featured IDE designed specifically for web development. Strong built-in understanding of HTML/CSS structure with zero configuration.  
[Download JetBrains WebStorm](https://www.jetbrains.com/webstorm/)

**Option B — Visual Studio Code**  
Lightweight, free, and backed by a massive extension ecosystem. Install the [Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server) extension to see your HTML update in real time as you type.  
[Download Visual Studio Code](https://code.visualstudio.com/)

---

### Step 3: Set up an AI assistant

AI assistants are used throughout this course to generate styled examples, explain concepts, and help debug your work. A free account is sufficient for all course exercises.

| Assistant | Provider | Free tier | Best for |
|-----------|----------|-----------|----------|
| [Gemini](https://gemini.google.com/) | Google | Yes | Generating HTML/CSS, quick explanations |
| [Claude](https://claude.ai/) | Anthropic | Yes | Detailed explanations, code review |
| [ChatGPT](https://chat.openai.com/) | OpenAI | Yes | General coding help |

> Choose any one to start. You can use multiple assistants side-by-side to compare outputs.

---

### Step 4: Install Git and clone this repository

Git lets you download the course materials and pull updates whenever new content is added.

**Download Git:** [git-scm.com](https://git-scm.com/)

> **macOS users:** Install [Homebrew](https://brew.sh/) first, then run `brew install git` in Terminal. Homebrew simplifies installing all developer tools on macOS.

**Clone with WebStorm:**
1. Open WebStorm → click **Clone Repository**
2. Paste the repository URL: `https://github.com/kevinju0827/Web-Zero-to-One.git`
3. Choose a local folder and click **Clone**

**Clone with command line:**
```bash
git clone https://github.com/kevinju0827/Web-Zero-to-One.git
cd Web-Zero-to-One
```

To pull future updates: **Git → Update Project** in WebStorm, or run `git pull` in the terminal.

---

### Step 5: Read this file in preview mode

Markdown files (`.md`) are displayed as formatted text in your editor's preview mode.

- **WebStorm:** Click the **Preview** button (split-pane icon) at the top right of the editor
- **VS Code:** Press `Ctrl+Shift+V` (Windows/Linux) or `Cmd+Shift+V` (macOS)
- **GitHub:** Rendered automatically in the browser

> Each module also contains its own `README.md` — open it in preview mode before starting that module.

---

## Module Structure

Every module follows the same structure so you always know where to look.

| Section | Purpose |
|---------|---------|
| **The Why?** | Motivation and real-world context. Answers "why does this matter?" before writing any code. Learning objectives are embedded here. |
| **Core Concepts** | Technical explanations with code examples, diagrams, and tables. This is the reference material you will return to. |
| **Going Further** | Optional deep dives into advanced topics, accessibility, performance, and AI usage patterns. Collapsible — skip freely. |
| **Guided Practice** | A step-by-step walkthrough building a small real-world example from scratch. Follow along in your own editor. |
| **Checkpoints** | Independent tasks that verify your understanding. Complete these before moving to the next module. |

Each module also contains one or more `*_example.html` files — these are the finished results for the Guided Practice steps. Use them as a reference if you get stuck, but build the practice file yourself first.

---

## Curriculum Overview

| Module | Topic | Key Concepts | Time |
|--------|-------|--------------|------|
| [M01](M01HTMLFoundations/README.md) | HTML Foundations | Document skeleton · headings · paragraphs · text elements · DevTools | 1–2 hrs |
| [M02](M02LinksAndMedia/README.md) | Links & Media | Attributes · `<a>` · relative vs absolute paths · `<img>` · `<figure>` · `<iframe>` | 1–2 hrs |
| [M03](M03ListsAndTables/README.md) | Lists & Tables | `<ul>` `<ol>` `<dl>` · `<table>` · `thead/tbody/tfoot` · `colspan` / `rowspan` | 1–2 hrs |
| [M04](M04Forms/README.md) | Forms | `<input>` types · `<label>` · `<fieldset>` · `<select>` / `<optgroup>` · HTML5 validation | 1.5–2 hrs |
| [M05](M05CSSBasics/README.md) | CSS Basics | Selectors · cascade · specificity · `<link>` · the box model intro | 1.5–2 hrs |
| [M06](M06TypographyAndColor/README.md) | Typography & Color | Font properties · color values · `px` / `em` / `rem` / `%` · Google Fonts | 1–2 hrs |
| [M07](M07StructureAndDisplay/README.md) | Structure & Display | Semantic HTML · `<div>` / `<span>` · `display` property · block vs inline | 1–2 hrs |
| [M08](M08BoxModel/README.md) | Box Model | `padding` · `border` · `margin` · `box-sizing` · DevTools box model panel | 1.5–2 hrs |
| [M09](M09Position/README.md) | Position | `static` · `relative` · `absolute` · `fixed` · `sticky` · `z-index` | 1.5–2 hrs |
| [M10](M10Flexbox/README.md) | Flexbox | Flex container · flex items · alignment · `gap` · wrapping | 2 hrs |
| [M11](M11CSSGrid/README.md) | CSS Grid | Grid tracks · `grid-template` · `grid-area` · responsive grid | 2 hrs |
| [M12](M12ResponsiveDesign/README.md) | Responsive Design | Media queries · mobile-first · `vw/vh` · fluid typography · `clamp()` | 2 hrs |
| [M13](M13Transitions/README.md) | Transitions & Animation | `transition` · `@keyframes` · `animation` · timing functions · `transform` | 1.5–2 hrs |
| [M14](M14Bootstrap/README.md) | Bootstrap Basics | CDN setup · container · 12-col grid · responsive breakpoints · utility classes | 2 hrs |
| [M15](M15BootstrapComponents/README.md) | Bootstrap Components | Navbar · card · button · form · badge · alert · modal · accordion | 2 hrs |
| [M16](M16Deployment/README.md) | Deployment | GitHub Pages · production checklist · custom domains · DNS basics | 1–2 hrs |

**Total estimated time: 30–35 hours** (including Guided Practice and Checkpoints)

---

## Tech Stack & Tools

| Category       | Tool                                                           | Notes                                                                                                                                                                                                                                    |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Language**   | HTML5                                                          | Markup language — defines what every element *is*. The structure of every page in this course.                                                                                                                                           |
| **Language**   | CSS3                                                           | Styling language — controls colours, fonts, layout, spacing, and animation.                                                                                                                                                              |
| **Framework**  | [Bootstrap 5](https://getbootstrap.com/)                       | M14 — pre-built components, responsive grid, utility classes loaded via CDN.                                                                                                                                                             |
| **Browser**    | [Google Chrome](https://www.google.com/intl/en/chrome/)        | Recommended browser. DevTools (`F12`) used throughout for inspection and debugging.                                                                                                                                                      |
| **IDE**        | [JetBrains WebStorm](https://www.jetbrains.com/webstorm/)      | Recommended for beginners. Built-in HTML/CSS intelligence, Git integration, live preview.                                                                                                                                                |
| **IDE**        | [Visual Studio Code](https://code.visualstudio.com/)           | Industry standard. Free, lightweight. Add [Live Preview](https://marketplace.visualstudio.com/items?itemName=ms-vscode.live-server) and [GitHub Copilot](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) extensions. |
| **IDE Plugin** | [JetBrains AI](https://www.jetbrains.com/ai-ides/)             | AI completions and chat built into WebStorm.                                                                                                                                                                                             |
| **IDE Plugin** | [Mermaid](https://plugins.jetbrains.com/plugin/20146-mermaid)  | Mermaid syntax support.                                                                                                                                                                                                                  |
| **AI**         | [Gemini](https://gemini.google.com/)                           | Google. Free. Generating HTML/CSS examples, quick explanations.                                                                                                                                                                          |
| **AI**         | [Claude](https://claude.ai/)                                   | Anthropic. Free tier. Detailed code explanations, reviewing HTML for errors.                                                                                                                                                             |
| **AI**         | [ChatGPT](https://chat.openai.com/)                            | OpenAI. Free tier. General-purpose coding help.                                                                                                                                                                                          |
| **Assets**     | [Unsplash](https://unsplash.com/)                              | Free high-resolution photos, no attribution required.                                                                                                                                                                                    |
| **Assets**     | [Pixabay](https://pixabay.com/)                                | Royalty-free photos, illustrations, and vectors.                                                                                                                                                                                         |
| **Assets**     | [unDraw](https://undraw.co/)                                   | Open-source SVG illustrations with customisable accent colour.                                                                                                                                                                           |
| **Assets**     | [Google Fonts](https://fonts.google.com/)                      | Free web fonts, loaded via a single `<link>` tag.                                                                                                                                                                                        |
| **Assets**     | [Animista](https://animista.net/)                              | Visual CSS animation builder — tweak and copy the generated code.                                                                                                                                                                        |
| **Assets**     | [Shields.io](https://shields.io/)                              | Generate SVG badges for README files.                                                                                                                                                                                                    |

> **JavaScript** — this course intentionally excludes in-depth JavaScript. The JS ecosystem adds significant complexity. Master the foundations here first; a dedicated JS course is the natural next step.

> Each module's Guided Practice ends with a step asking you to use an AI to style your work. Experiencing AI-assisted development early — while you still understand every line — is the core skill this course builds.

---

## Recommended Resources

These are optional but high-value references to use alongside this course.

| Resource | What it is |
|----------|-----------|
| [MDN Web Docs](https://developer.mozilla.org) | The authoritative HTML/CSS reference. Maintained by Mozilla. Use it to look up any element, attribute, or property in depth. |
| [W3Schools](https://www.w3schools.com) | Quick, isolated examples for syntax lookups. Ideal when you want to check if a tag or property exists without reading full spec pages. |
| [roadmap.sh — Frontend](https://roadmap.sh/frontend) | Visual map of the entire frontend landscape. Use it to see where this course fits and plan what to learn next. |
| [Flexbox Froggy](https://flexboxfroggy.com) | Interactive game for learning Flexbox. Complements M10. |
| [CSS Grid Garden](https://cssgridgarden.com) | Interactive game for learning CSS Grid. Complements M11. |
| [CSS Tricks — Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/) | The most referenced Flexbox visual guide on the web. |
| [CSS Tricks — Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/) | Comprehensive CSS Grid reference with visual diagrams. |
| [CSS Diner](https://flukeout.github.io/) | Interactive game for learning CSS selectors — 32 levels. Complements M05. |
| [Atguigu HTML5+CSS3 (Chinese)](https://youtu.be/E-DErp0IcA0?list=PLmOn9nNkQxJGGuwYhQzTmRGFwF9cHYS-x) | Free video course in Mandarin. Excellent if you prefer video explanations in Chinese. |

---

## License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for details.
