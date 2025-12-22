Below is a **Day 1–Day 7 plan for Week 1**, focused on HTML/CSS foundations and how the web works.  
Assume ~1.5–3 hours/day (adjust up/down as needed).  
You’ll see four recurring blocks:

- **Learn** – watch/read, take short notes  
- **Do** – build something or write code  
- **Reflect** – quick written review  
- **Stretch** – optional challenge if you have extra time

Use any browser + VS Code. When in doubt, **try first, then Google, then docs**.

---

## Day 1 – How the Web Works + Your First Page

**Goals:**
- Understand client/server, HTTP, and what HTML is.
- Set up your tools.
- Create a minimal web page.

### 1. Learn (40–60 minutes)

1. **Concepts to understand (not memorize):**
   - What happens when you type `https://example.com` into a browser:
     - Browser → sends HTTP request → server → sends response (HTML/CSS/JS).
   - Definitions:
     - Client (browser), server, URL, HTTP, HTML, CSS, JavaScript.
   - What HTML is: a structured document with tags.

2. **Read/watch (pick one set):**
   - MDN (Mozilla Developer Network):
     - “How the web works” (skim the main idea).
     - “HTML basics”.
   - OR a short YouTube crash course on:
     - “How the web works (client/server)”
     - “HTML for absolute beginners” (first ~20 min).

Take simple notes:
- 3–5 bullet points about “how the web works”
- 3–5 HTML tags you saw.

### 2. Do (60–90 minutes)

1. **Set up:**
   - Install VS Code (if not already).
   - Create a folder: `week1-website/`.
   - Inside, create `index.html`.

2. **Build a barebones page:**
   - Add this minimal structure by typing it yourself (don’t copy-paste):

     ```html
     <!DOCTYPE html>
     <html lang="en">
       <head>
         <meta charset="UTF-8" />
         <title>My First Web Page</title>
       </head>
       <body>
         <h1>Hello, world!</h1>
         <p>This is my first web page.</p>
       </body>
     </html>
     ```

   - Open the file in your browser (double-click or right-click → “Open with”).

3. **Experiment:**
   - Add:
     - 2 more headings: `<h2>`, `<h3>`
     - A paragraph with **bold** `<strong>` and *italic* `<em>` words.
     - A list of 3 favorite foods using `<ul>` + `<li>`.
   - Refresh the browser each time you change the file.

### 3. Reflect (10 minutes)

- In a text file called `notes-day1.md` (or a notebook), answer:
  - What is a client? What is a server?
  - What surprised you about how the web works?
  - What 3 HTML tags do you remember, and what do they do?

### 4. Stretch (optional, 20–30 minutes)

- Add an **image** to the page using `<img>` (Google: “HTML img tag MDN”).
- Add a link to your favorite website using `<a>` with `href`.  
- Without looking, recreate the entire HTML file from scratch in a new file.

---

## Day 2 – HTML Structure & Semantic Tags

**Goals:**
- Learn the common HTML tags used to structure a page.
- Create a simple, well-structured multi-section page.

### 1. Learn (40–60 minutes)

1. **Concepts:**
   - What “semantic HTML” means: tags that describe meaning, not just appearance.
   - Common semantic tags:
     - `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`.
   - Attributes: `id`, `class`, `href`, `src`, `alt`.

2. **Read:**
   - MDN “HTML elements reference” (skim top-level categories).
   - MDN “HTML semantics” (focus on understanding, not memorizing every tag).

Write down:
- A one-line description for each: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`.
- What attributes are, and 2 examples.

### 2. Do (60–90 minutes)

1. **New file:**
   - Inside `week1-website/`, create `about-me.html`.

2. **Build a semantic layout:**
   - Use the following structure:

     ```html
     <header>
       <h1>Your Name</h1>
       <nav>
         <a href="#about">About</a>
         <a href="#hobbies">Hobbies</a>
         <a href="#contact">Contact</a>
       </nav>
     </header>

     <main>
       <section id="about">
         <h2>About Me</h2>
         <p>...</p>
       </section>

       <section id="hobbies">
         <h2>Hobbies</h2>
         <ul>
           <li>...</li>
         </ul>
       </section>

       <section id="contact">
         <h2>Contact</h2>
         <p>Email: ...</p>
       </section>
     </main>

     <footer>
       <p>© 2025 Your Name</p>
     </footer>
     ```

   - Fill in real content about yourself.

3. **Internal links:**
   - Ensure nav links use `href="#about"` etc.  
   - Click them and watch the browser jump to sections.

### 3. Reflect (10 minutes)

- Answer in your notes:
  - Why might semantic tags be better than just `<div>` for everything?
  - How do `id` and `href="#id"` work together?

### 4. Stretch (optional, 20–30 minutes)

- Add an `<article>` section for “Blog Posts” with at least 2 `<article>` entries inside a `<section>`.
- Add a simple table (e.g. a weekly schedule) using `<table>`, `<tr>`, `<th>`, `<td>`.

---

## Day 3 – Intro to CSS + The Box Model

**Goals:**
- Understand how to connect CSS to HTML.
- Learn the box model: margin, border, padding, content.

### 1. Learn (40–60 minutes)

1. **Concepts:**
   - How to apply CSS:
     - Inline styles, `<style>` tag, **external stylesheet** (`.css` file).
   - Selectors: element (`p`), class (`.my-class`), id (`#my-id`).
   - Box model:
     - Content → padding → border → margin.
   - `display: block` vs `inline`.

2. **Read/watch:**
   - MDN “Getting started with CSS” (focus on the idea of CSS rules).
   - MDN “Box model” section.

Write down:
- The syntax of a CSS rule (selector `{ property: value; }`).
- One example each of: element selector, class selector, id selector.
- The 4 parts of the box model.

### 2. Do (60–90 minutes)

1. **Set up CSS:**
   - In your folder, create `styles.css`.
   - In `about-me.html`, add inside `<head>`:

     ```html
     <link rel="stylesheet" href="styles.css" />
     ```

2. **Style basic elements:**
   - In `styles.css`, add:

     ```css
     body {
       font-family: Arial, sans-serif;
       line-height: 1.5;
     }

     header, footer {
       background-color: #f2f2f2;
     }

     h1, h2 {
       color: #333333;
     }
     ```

   - Refresh the page and observe changes.

3. **Experiment with box model:**
   - Create a class `.card`:

     ```css
     .card {
       border: 1px solid #ccc;
       padding: 16px;
       margin: 16px 0;
     }
     ```

   - In `about-me.html`, wrap one section in a `<div class="card">...</div>` and see how it changes.

4. **Use DevTools:**
   - Right-click on an element → “Inspect”.
   - Look at the “box model” visualization.
   - Change `padding` and `margin` live from DevTools and observe.

### 3. Reflect (10 minutes)

- Answer:
  - What’s the difference between padding and margin?
  - How would you select:
    - All `<p>` tags?
    - An element with id `main`?
    - All elements with class `card`?

### 4. Stretch (optional, 20–30 minutes)

- Add `max-width` and `margin: 0 auto;` to a wrapper container to center your content.
- Add a border and background color to the `<nav>` and adjust padding so it looks better.

---

## Day 4 – Typography, Colors, and Simple Layout

**Goals:**
- Control the look and feel (fonts, colors).
- Start arranging elements with basic layout properties.

### 1. Learn (40–60 minutes)

1. **Concepts:**
   - CSS properties for text:
     - `font-family`, `font-size`, `font-weight`, `color`, `line-height`.
   - Colors:
     - Named colors, hex (`#333333`), RGB.
   - Layout basics (without flexbox yet):
     - `width`, `max-width`, `text-align`, `margin`.

2. **Read:**
   - MDN “Styling text”.
   - MDN “CSS values and units” (skim `px`, `%`, `em`, `rem`).

Write down:
- One example of a font stack (e.g. `font-family: "Helvetica", Arial, sans-serif;`).
- When you might prefer `%` or `rem` over `px`.

### 2. Do (60–90 minutes)

1. **Improve `about-me.html` styling:**
   - In `styles.css`:
     - Set a base font-size and line-height on `body`.
     - Choose a color palette (3 colors: primary, secondary, background).

   Example:

   ```css
   body {
     font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
     background-color: #fafafa;
     color: #333;
     margin: 0;
   }

   main {
     max-width: 800px;
     margin: 0 auto;
     padding: 16px;
   }

   header, footer {
     padding: 16px;
     text-align: center;
   }
   ```

2. **Header/navigation styling:**
   - Remove underline from nav links and add spacing:

     ```css
     nav a {
       text-decoration: none;
       color: #333;
       margin: 0 8px;
     }

     nav a:hover {
       text-decoration: underline;
     }
     ```

3. **Visual hierarchy:**
   - Ensure:
     - `<h1>` is largest, `<h2>` smaller.
     - Section headings are clearly distinct from paragraph text.

### 3. Reflect (10 minutes)

- Look at your page and answer:
  - What looks good? What feels off?
  - If you had to improve readability, what would you change?

### 4. Stretch (optional, 20–30 minutes)

- Try importing a Google Font (search “Google Fonts MDN” or “use Google Fonts CSS”).
- Add a simple “card” style to your hobbies section and adjust padding/margin until it looks clean.

---

## Day 5 – Flexbox Basics (Modern Layout Tool)

**Goals:**
- Start arranging elements in rows/columns using Flexbox.
- Build a simple responsive header with Flexbox.

### 1. Learn (40–60 minutes)

1. **Concepts:**
   - What Flexbox is for: laying out items in one dimension (row or column).
   - Key properties:
     - Container: `display: flex;`, `flex-direction`, `justify-content`, `align-items`.
     - Items: `flex: 1;` (basic idea).
   - Horizontal vs vertical centering with Flexbox.

2. **Read/watch:**
   - MDN “Basic concepts of flexbox” (focus on the diagrams).
   - Optionally a short Flexbox tutorial video (up to ~20 mins).

Write down:
- What `justify-content` controls.
- What `align-items` controls.
- What `flex-direction: row` vs `column` means.

### 2. Do (60–90 minutes)

1. **Flexbox in the header:**
   - In `styles.css`, for the `<header>`:

     ```css
     header {
       display: flex;
       justify-content: space-between;
       align-items: center;
       padding: 16px 24px;
       background-color: #f0f0f0;
     }

     header h1 {
       margin: 0;
     }
     ```

   - Check how the title and nav align.

2. **Create a “features” section:**
   - In `about-me.html`, add:

     ```html
     <section id="features">
       <h2>What I’m Learning</h2>
       <div class="features">
         <div class="feature-card">HTML &amp; CSS</div>
         <div class="feature-card">JavaScript</div>
         <div class="feature-card">React & Node</div>
       </div>
     </section>
     ```

   - Style with Flexbox:

     ```css
     .features {
       display: flex;
       gap: 16px;
       margin-top: 16px;
     }

     .feature-card {
       flex: 1;
       border: 1px solid #ddd;
       padding: 16px;
       background-color: #fff;
     }
     ```

3. **Experiment with different properties:**
   - Change `justify-content` to `center`, `space-around`, `space-evenly`.
   - Change `flex-direction` to `column` and see what happens.

### 3. Reflect (10 minutes)

- Answer:
  - How did changing `justify-content` affect the layout?
  - When would `flex-direction: column` be useful?

### 4. Stretch (optional, 20–30 minutes)

- Try making the header sticky: search “CSS sticky header” and attempt `position: sticky; top: 0;`.
- Add an avatar/profile photo in the header and align it neatly with Flexbox.

---

## Day 6 – Basic Responsive Design (Mobile First)

**Goals:**
- Understand what “responsive” means.
- Use media queries to adapt layout for small screens.

### 1. Learn (40–60 minutes)

1. **Concepts:**
   - Responsive design:
     - Pages that work on mobile, tablet, desktop.
   - Viewport:
     - Why we add `<meta name="viewport" content="width=device-width, initial-scale=1.0" />` in `<head>`.
   - Media queries:
     - `@media (max-width: 768px) { ... }`.

2. **Read:**
   - MDN “Responsive design basics”.
   - MDN “Using media queries” (focus on one or two examples).

Write down:
- What a media query is.
- One breakpoint you’ll use (e.g. `768px` for tablets).

### 2. Do (60–90 minutes)

1. **Add viewport meta:**
   - In all your HTML files inside `<head>`:

     ```html
     <meta name="viewport" content="width=device-width, initial-scale=1.0" />
     ```

2. **Make the features section responsive:**
   - In `styles.css`, add:

     ```css
     @media (max-width: 768px) {
       .features {
         flex-direction: column;
       }

       header {
         flex-direction: column;
         align-items: flex-start;
       }

       nav a {
         display: inline-block;
         margin: 4px 4px 0 0;
       }
     }
     ```

   - Test:
     - Make the browser window narrow.
     - Use DevTools “toggle device toolbar” (mobile view).

3. **Adjust font sizes for small screens:**
   - Inside the same media query, slightly decrease heading sizes or padding if needed.

### 3. Reflect (10 minutes)

- Answer:
  - What changed when you resized the browser window?
  - What’s one improvement you’d like to make for small screens?

### 4. Stretch (optional, 20–30 minutes)

- Add another breakpoint, e.g.:

  ```css
  @media (max-width: 480px) {
    body {
      font-size: 14px;
    }
  }
  ```

- Try hiding some non-essential elements on very small screens (e.g. hide an image).

---

## Day 7 – Mini “Landing Page” Project & Review

**Goals:**
- Consolidate everything from the week into a small project.
- Practice building from scratch with minimal step-by-step guidance.

### 1. Plan (15–20 minutes)

On paper or in a note, sketch a simple **landing page** (single screen) for:

- A fictional product (e.g. “FocusNote – a note taking app”), or
- Your personal “Developer in Training” profile.

Your page should include:
- Header with title + nav (links that scroll to sections).
- Hero section:
  - Big heading, subheading, a call-to-action button.
- Features section (3 columns/cards on desktop, stacked on mobile).
- About section or “Why this exists”.
- Footer.

Don’t start coding until you have a rough mental or paper layout.

### 2. Do – Build the Landing Page (90–120 minutes)

1. **Set up:**
   - Create a new file: `landing.html`.
   - Link `styles.css` or create a new stylesheet (your choice).
   - Add boilerplate HTML: `<!DOCTYPE html>`, `<html>`, `<head>`, etc.
   - Include the viewport meta tag.

2. **Structure HTML first (no CSS yet):**
   - Use semantic tags:
     - `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`.
   - Give `id`s to sections for navigation.
   - Add realistic text (don’t worry about perfect wording, just write something).

3. **Then add CSS:**
   - Re-use styles from previous days when possible.
   - Use:
     - A max-width container for main content.
     - Flexbox for:
       - Header (logo/title + nav).
       - Features section (3 feature cards).
   - Add a hero section with:
     - Large heading.
     - Button styled (background color, padding, border-radius).

4. **Make it responsive:**
   - At least one media query (`max-width: 768px`):
     - Stack nav vertically or make it more compact.
     - Features become a column.
   - Check in browser at multiple widths.

### 3. Self-Review Checklist (20–30 minutes)

Use this checklist against your `landing.html`:

- Structure:
  - [ ] Do I use `<header>`, `<main>`, `<section>`, `<footer>` appropriately?
  - [ ] Do nav links scroll to their sections using `href="#..."`?
- CSS:
  - [ ] Does the page have consistent spacing (padding/margin)?
  - [ ] Are headings clearly larger than body text?
  - [ ] Are feature cards visually separated (border/background/padding)?
- Responsiveness:
  - [ ] On a narrow screen, is the content still readable without horizontal scrolling?
  - [ ] Does my layout change at the breakpoint?

Note 2–3 weaknesses you notice.

### 4. Reflect (10–15 minutes)

- In your notes, answer:
  - What were the hardest parts of this week?
  - What CSS concept do you still feel shaky about?
  - If you had 1 more hour to improve the landing page, what would you do?

### 5. Stretch (optional, 20–40 minutes)

- Add a simple **contact form** to the landing page:
  - Use `<form>`, `<label>`, `<input>`, `<textarea>`, `<button>`.
  - Style it to match the rest of the page.
- Validate HTML/CSS:
  - Use an online HTML validator and see if any errors come up.
  - Fix as many as you can.

---

If you’d like next, I can:
- Turn Week 2 into a daily plan (focusing more on Flexbox, layout patterns, and refinement), or
- Review a description or screenshot of your Day 7 landing page and suggest concrete improvements.
