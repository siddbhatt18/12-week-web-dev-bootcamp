### Day 3 – Intro to CSS & The Box Model

**Theme:** Move from plain, unstyled HTML to pages that look intentional. Learn how CSS “hooks into” your HTML and how the browser actually lays things out.

**Estimated time:** 2–3 hours  

---

## 1. Learning Objectives

By the end of Day 3 you should be able to:

1. Explain what CSS is and how it relates to HTML.
2. Use **external stylesheets** and basic **selectors** (element, class, id).
3. Understand and visualize the **CSS box model**: content, padding, border, margin.
4. Use core CSS properties: `color`, `background-color`, `font-family`, `margin`, `padding`, `border`, `width`.
5. Use browser **DevTools** to inspect and tweak styles.
6. See how all this lays the groundwork for React styling and frontend frameworks later.

---

## 2. Conceptual Foundations (Learn)

Spend ~45–60 minutes here with short notes.

### 2.1 What Is CSS?

- **CSS = Cascading Style Sheets**
  - Defines how HTML elements are **presented** (colors, spacing, layout, fonts).
  - Keeps **structure** (HTML) and **presentation** (CSS) separate.

**CSS rule format:**

```css
selector {
  property: value;
  property2: value2;
}
```

Examples:

```css
p {
  color: blue;
}

.my-class {
  background-color: #f0f0f0;
}

#main-title {
  font-size: 32px;
}
```

### 2.2 Ways to Include CSS

You’ll use this one most of the time:

1. **External stylesheet** (recommended for real projects):

```html
<!-- in <head> -->
<link rel="stylesheet" href="styles.css" />
```

2. **Internal** (`<style>` tag):

```html
<style>
  p {
    color: red;
  }
</style>
```

3. **Inline styles** (avoid in most cases):

```html
<p style="color: red;">Hello</p>
```

For maintainability and scalability, **external CSS files** are the standard approach.

### 2.3 Selectors

- **Element selector** – targets all elements of that type:

```css
p {
  color: #333;
}
```

- **Class selector** – targets elements with a given `class` attribute:

```css
.highlight {
  background-color: yellow;
}
```

In HTML:

```html
<p class="highlight">Some text</p>
```

- **ID selector** – targets the element with a specific `id`:

```css
#main-title {
  font-size: 2rem;
}
```

In HTML:

```html
<h1 id="main-title">Title</h1>
```

General rules of thumb:

- Use **classes** for styling groups / reusable styles.
- Reserve **ids** for unique elements or JavaScript hooks, not for general styling.

### 2.4 The Box Model

Every element is a **box** with:

1. **Content** – text or image.
2. **Padding** – space between content and border.
3. **Border** – line around padding and content.
4. **Margin** – space outside the border (space between elements).

Visual:

```text
+---------------------------+
|        margin             |
|  +---------------------+  |
|  |       border        |  |
|  |  +---------------+  |  |
|  |  |   padding     |  |  |
|  |  |  +---------+  |  |  |
|  |  |  | content |  |  |  |
|  |  |  +---------+  |  |  |
|  |  +---------------+  |  |
|  +---------------------+  |
+---------------------------+
```

Key properties:

```css
padding: 16px;       /* inside spacing */
margin: 16px;        /* outside spacing */
border: 1px solid #ccc;
```

Also:

- `display: block` – element takes full width, starts on a new line (e.g., `<div>`, `<p>`, `<h1>`).
- `display: inline` – sits within a line, width = content only (e.g., `<span>`, `<a>`).

---

## 3. Hands-On Work (Do)

Spend 60–90 minutes coding and experimenting.

You’ll add CSS to your **Day 2 about-me page** and visually understand the box model.

### 3.1 Create and Link a Stylesheet

1. In your Week 1 folder, create a new file: `styles.css`.
2. Open `about-me.html` from Day 2.
3. In the `<head>` section, add:

```html
<link rel="stylesheet" href="styles.css" />
```

Check that `about-me.html` and `styles.css` are in the same folder (or adjust the path).

### 3.2 Basic Page Styling

In `styles.css`, add:

```css
/* 1. Global base styles */
body {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  margin: 0;
  padding: 0;
  line-height: 1.5;
  color: #333333;
}

/* 2. Layout containers */
.site-header,
.site-footer {
  background-color: #f2f2f2;
  padding: 16px;
}

/* 3. Main content wrapper */
.site-main {
  max-width: 800px;
  margin: 0 auto;
  padding: 16px;
}
```

Make sure your `about-me.html` header/main/footer use these classes:

```html
<header class="site-header">
  ...
</header>

<main class="site-main">
  ...
</main>

<footer class="site-footer">
  ...
</footer>
```

Refresh the page and note:

- No default body margin (content touches browser edges).
- Header and footer have background color and padding.
- Main content is centered and narrower.

### 3.3 Headings, Text, and Links

Add to `styles.css`:

```css
h1,
h2,
h3 {
  color: #222222;
  margin-top: 0;
}

h1 {
  font-size: 2rem;
}

h2 {
  font-size: 1.5rem;
  margin-top: 24px;
}

p {
  margin-bottom: 12px;
}

/* Navigation links */
.site-nav a {
  text-decoration: none;
  color: #333333;
  margin-right: 12px;
}

.site-nav a:hover {
  text-decoration: underline;
}
```

Ensure your nav has `class="site-nav"`:

```html
<nav class="site-nav">
  ...
</nav>
```

Refresh and observe:

- Headings are more consistent.
- Nav links look like part of a styled header.

### 3.4 Explore the Box Model with a “Card”

1. In `styles.css`, create a reusable “card” style:

```css
.card {
  border: 1px solid #dddddd;
  padding: 16px;
  margin: 16px 0;
  background-color: #ffffff;
}
```

2. In `about-me.html`, wrap one of your sections in a card:

```html
<section id="about" class="card">
  <h2>About Me</h2>
  <p>Write a short paragraph about yourself here.</p>
</section>
```

3. Refresh and see how that section stands out.

4. Use **DevTools** (right-click → Inspect):

   - Select the `.card` element.
   - In the Styles/Layout pane, look for the **box model** visualization.
   - Adjust `padding` and `margin` live:
     - Try `padding: 32px;` vs `4px;`
     - Try `margin: 32px 0;` vs `0;`

Notice how:

- Padding affects **inside** spacing (text moves away from border).
- Margin affects **outside** spacing (distance to other elements).

### 3.5 Practice with Margins and Borders

Still in `styles.css`, add styles to differentiate sections:

```css
section {
  margin-bottom: 24px;
}

#projects {
  border-top: 2px solid #cccccc;
  padding-top: 16px;
}
```

Observe:

- Space between sections from `margin-bottom`.
- Visual separation for Projects with a top border.

Try changing:

- `margin-bottom` to `40px` and see the effect.
- `border-top` thickness and color.

---

## 4. Reflection & Consolidation

Spend 10–15 minutes in your notes (e.g. `notes-day3.md`).

1. In your own words:
   - What is the **box model**?
   - What’s the difference between **margin** and **padding**?

2. Selectors:
   - How do you select:
     - All `<p>` tags?
     - An element with `id="contact"`?
     - All elements with `class="card"`?

3. DevTools:
   - What did you learn by inspecting the `.card` element in DevTools?
   - How might DevTools help you later when debugging layout issues in a React app?

4. Self-assessment:
   - Which CSS concepts feel solid?
   - Which ones still feel confusing (e.g., display types, units, etc.)?

---

## 5. Practice Questions (Increasing Difficulty)

Use these after you’ve finished the hands-on exercises.

### 5.1 Basic Concept Check (Level 1 – Recall)

1. What does CSS stand for, and what problem does it solve?
2. Name three ways to apply CSS to HTML. Which is preferred for larger projects?
3. Describe the four main parts of the CSS box model.
4. What is the difference between `display: block` and `display: inline`?
5. What is the difference between `margin` and `padding`?

---

### 5.2 Selector and Rule Writing (Level 2 – Apply)

6. Write CSS rules for the following:

   - Make all paragraphs have text color `#444444`.
   - Make all `h2` elements have a bottom margin of `20px`.
   - Create a class `.highlight` that sets a yellow background.
   - Create an `#main-heading` style that:
     - Makes font size 32px.
     - Centers the text.

7. Given this HTML:

   ```html
   <h1 id="site-title">My Site</h1>
   <p class="intro">Welcome to my website.</p>
   <p class="intro">Here you'll find my projects and blog posts.</p>
   ```

   Write CSS to:

   - Color the `h1` text dark blue.
   - Make all `.intro` paragraphs italic.

8. You want three specific sections (`#about`, `#projects`, `#contact`) to share the same card style.  
   How do you do that using a **class** instead of repeating styles for each `id`?

---

### 5.3 Box Model & Layout Reasoning (Level 3 – Understand & Debug)

9. Suppose an element has this CSS:

   ```css
   .box {
     width: 200px;
     padding: 20px;
     border: 5px solid #000;
     margin: 10px;
   }
   ```

   - What is the total horizontal space this element takes up (excluding margin)?
   - What is the total horizontal space including left and right margin?

10. You have two `<div>` elements stacked vertically. They seem “stuck together” with no space between them.  
    Name at least two different CSS approaches to add space between them.

11. You change `padding: 10px;` to `padding: 50px;` on a card.  
    - What visual changes do you expect?
    - How does this affect the card’s content vs its position relative to neighboring elements?

---

### 5.4 Full-Stack Connections (Level 4 – Conceptual Bridge)

12. In a future React frontend, you’ll often have components like:

    ```jsx
    function Card({ title, children }) {
      return (
        <div className="card">
          <h3>{title}</h3>
          <div>{children}</div>
        </div>
      );
    }
    ```

    Today, you created a `.card` style in plain CSS.  
    How does understanding the box model help you reason about the visual appearance of this React `Card` component?

13. When building a full-stack app, you might fetch a list of tasks from a backend and display them as items in a list.  
    If the list looks cramped or misaligned, what steps would you take using:
    - CSS box model knowledge.
    - Browser DevTools.
    - Understanding of HTML structure.

14. Imagine your backend (Express + MongoDB) returns a JSON array of products. On the frontend, you generate a grid of product cards.  
    Why is it important to:
    - Use consistent **classes** for these cards?
    - Understand `margin` and `padding` when laying them out side by side?

---

### 5.5 Stretch Coding Exercises (Level 5 – Small Builds)

If you have extra time and want more practice:

15. **Style your `index.html` from Day 1**:

    - Link to `styles.css` (or create a new CSS file).
    - Give the page:
      - A distinct header style (background color, padding).
      - A main content area with max-width and centered.
      - At least one `.card` for a section.

16. Create a new file `layout-demo.html` with:

    - A header
    - A main area with three sections (`.card`)
    - A footer

    Then in `styles.css`:

    - Give each `.card` a different background color.
    - Apply different margin and padding values to each.
    - Use DevTools to observe each box’s model and note down differences.

17. Experiment with borders:

    - Add `border-radius` to your `.card` to round corners.
    - Try different `border` styles (`dashed`, `dotted`, etc.).
    - Add `box-shadow` (Google: “CSS box-shadow MDN”) to make cards pop.

---

## 6. How Day 3 Supports Full-Stack Skills

Today’s CSS and box model knowledge will show up repeatedly later:

- **Frontend frameworks (React, etc.):**  
  You’ll still use CSS (or CSS-in-JS) to style components. Knowing selectors, classes, and the box model is fundamental.

- **Reusable components:**  
  Concepts like `.card`, `.site-header`, and `.site-main` are direct precursors to React components and design systems.

- **Debugging complex UIs:**  
  As your full-stack apps grow (forms, dashboards, lists from APIs), layout bugs are inevitable. DevTools + box model understanding are your primary debugging tools.

- **Professional quality:**  
  Even simple apps look significantly more professional with good spacing, typography, and layout—this matters for portfolio projects and interviews.

---

If you’d like next, I can:

- Create a **Day 4** guide focusing on typography, colors, and simple layout patterns, or  
- Look at (or have you describe) your current `about-me.html` + `styles.css` and suggest concrete improvements to structure and styling.
