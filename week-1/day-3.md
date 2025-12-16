Day 3 is your first **real CSS day**: you’ll learn how to connect a stylesheet, style text, and understand the **box model** (the foundation of all layout).

Assume ~2 hours. Keep everything in `week1/day3/`.

---

## High-Level Objectives for Day 3

By the end of today, you should be able to:

- Link an external CSS file to an HTML page.
- Use basic selectors: element, class, and ID.
- Style text (colors, fonts, sizes, alignment).
- Explain and experiment with the **box model**: content, padding, border, margin.
- Inspect elements with DevTools to see their box model.

---

## Part 1 – CSS Basics (Concepts) – 30–40 min

### 1. What is CSS and how do we include it? (10–15 min)

Core points to understand:

- **CSS** = Cascading Style Sheets.
  - It controls **how** HTML content looks (colors, fonts, layout, spacing).
- Three ways to add CSS (you’ll focus on the best one today):
  1. **External stylesheet** (preferred):
     ```html
     <link rel="stylesheet" href="styles.css">
     ```
  2. Internal `<style>` tag in `<head>`.
  3. Inline styles: `<p style="color: red;">…</p>` (avoid in real projects).

Today you’ll use an **external stylesheet**, which keeps HTML and CSS separate and easier to manage.

### 2. Basic selectors: element, class, and ID (10–15 min)

Learn these three selector types:

1. **Element selector** – targets all elements of that tag:
   ```css
   p {
     color: blue;
   }
   ```

2. **Class selector** – reusable style added via `class=""` in HTML:
   ```html
   <p class="highlight">Some text</p>
   <p class="highlight">Some more highlighted text</p>
   ```
   ```css
   .highlight {
     background-color: yellow;
   }
   ```

3. **ID selector** – unique element via `id=""`:
   ```html
   <h1 id="main-title">Welcome</h1>
   ```
   ```css
   #main-title {
     color: darkgreen;
   }
   ```

Guideline:
- Use **classes** for styles you might reuse.
- Use **IDs** for unique elements (e.g., `#top`, `#main-header`).

### 3. The box model (10–15 min)

Every visible element is a **box** made of:

1. **Content** – the actual text or image.
2. **Padding** – space between content and border.
3. **Border** – the line around padding/content.
4. **Margin** – space outside the border (distance to other elements).

Visual:

```
+------------------------+
|       margin           |
|  +------------------+  |
|  |     border       |  |
|  |  +------------+  |  |
|  |  |  padding   |  |  |
|  |  | +--------+ |  |  |
|  |  | |content | |  |  |
|  |  | +--------+ |  |  |
|  |  +------------+  |  |
|  +------------------+  |
+------------------------+
```

Key properties:

```css
.box {
  padding: 10px;
  border: 2px solid black;
  margin: 20px;
  width: 200px;  /* width of content area (not counting padding, border by default) */
}
```

You’ll make this concrete in practice.

---

## Part 2 – Styling Yesterday’s Article with CSS – 60–70 min

You’ll reuse the structure idea from Day 2, but keep files separate to stay organized.

### 1. Create files (5–10 min)

In `week1/day3/`, create:

- `day3-article.html`
- `styles-day3.css`

Copy your **HTML structure** from `day2-article.html` into `day3-article.html` (just the `<html>...</html>` content). Then:

- Change the `<title>` to something like `Day 3 – Styled Article`.

### 2. Link the external stylesheet (5 min)

In the `<head>` of `day3-article.html`, add:

```html
<link rel="stylesheet" href="styles-day3.css">
```

Full example:

```html
<head>
  <meta charset="UTF-8">
  <title>Day 3 – Styled Article</title>
  <link rel="stylesheet" href="styles-day3.css">
</head>
```

Open `day3-article.html` in your browser. For now it looks unstyled, which is fine.

### 3. Base styles: body, headings, paragraphs (20–25 min)

Open `styles-day3.css` and add:

1. **Reset and base font styles:**

```css
/* Reset some default margins */
body {
  margin: 0;
  padding: 0;
  font-family: Arial, Helvetica, sans-serif; /* pick any simple font */
  line-height: 1.6; /* makes text more readable */
}
```

2. **Constrain width and center content:**

```css
/* Constrain the width and center the page content */
main {
  max-width: 800px;
  margin: 0 auto;     /* centers main horizontally */
  padding: 1rem;      /* some inner spacing */
}
```

3. **Style headings:**

```css
h1 {
  text-align: center;
  margin: 1rem 0;
}

h2 {
  margin-top: 1.5rem;
  color: #333333;
}

h3 {
  margin-top: 1rem;
  color: #555555;
}
```

4. **Style paragraphs and links:**

```css
p {
  margin: 0.5rem 0;
  color: #222222;
}

a {
  color: #0066cc;
  text-decoration: none; /* remove underline */
}

a:hover {
  text-decoration: underline; /* underline on hover for clarity */
}
```

5. **Give header and footer some visual separation:**

```css
header,
footer {
  background-color: #f4f4f4;
  padding: 1rem;
}

footer {
  text-align: center;
  font-size: 0.9rem;
  color: #666666;
}
```

Save and refresh `day3-article.html` to see the change.

### 4. Add classes and experiment with class selectors (15–20 min)

Pick one section or paragraph you want to highlight.

In `day3-article.html`, add a class:

```html
<section class="highlight-section">
  <h3>Main Points</h3>
  <p>Explain 2–3 main points about your topic.</p>
  <ul>
    <li>Point one...</li>
    <li>Point two...</li>
    <li>Point three...</li>
  </ul>
</section>
```

In `styles-day3.css`, add:

```css
.highlight-section {
  background-color: #fff8e1;
  border-left: 4px solid #ffb300;
  padding: 0.75rem 1rem;
  margin: 1rem 0;
}
```

Also, add a class to your main article title:

```html
<h2 class="article-title">My First Article</h2>
```

And style it:

```css
.article-title {
  font-size: 1.8rem;
  color: #222222;
}
```

This gives you practice connecting **HTML classes** to **CSS selectors**.

---

## Part 3 – Box Model Practice: Boxes Page – 20–25 min

You’ll build a tiny “boxes” page just to experiment with padding, border, and margin.

### 1. Create files (5 min)

In `week1/day3/`, create:

- `day3-boxes.html`

Basic HTML:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Day 3 – Box Model</title>
    <link rel="stylesheet" href="styles-day3.css">
  </head>
  <body>
    <h1>Box Model Demo</h1>

    <div class="box box-one">Box One</div>
    <div class="box box-two">Box Two</div>
    <div class="box box-three">Box Three</div>
  </body>
</html>
```

You can reuse `styles-day3.css` (it already exists), or you can make a separate CSS file; for simplicity, we’ll keep using `styles-day3.css`.

### 2. Add box styles in CSS (15–20 min)

In `styles-day3.css`, add:

```css
.box {
  width: 200px;
  /* height: 100px;  you can uncomment to see fixed height behavior */
  background-color: #e0e0e0;
  margin: 10px;          /* space outside the box */
  padding: 10px;         /* space inside, around the text */
  border: 2px solid #333;
}
```

Now open `day3-boxes.html` and look at the boxes.

Change values and observe:

- Increase padding:

  ```css
  padding: 30px;
  ```

- Increase margin:

  ```css
  margin: 30px;
  ```

- Change border:

  ```css
  border: 5px dashed red;
  ```

Give each box different values to see the effect:

```css
.box-one {
  background-color: #f8bbd0;
  padding: 10px;
  margin: 5px;
}

.box-two {
  background-color: #bbdefb;
  padding: 20px;
  margin: 20px;
  border-width: 4px;
}

.box-three {
  background-color: #c8e6c9;
  padding: 5px 20px;   /* top/bottom 5px, left/right 20px */
  margin: 10px 40px;   /* top/bottom 10px, left/right 40px */
}
```

Try to answer for yourself:

- When I change **padding**, what visually changes?
- When I change **margin**, what visually changes?
- How does border thickness affect the overall size?

---

## Part 4 – DevTools: Inspecting the Box Model – 10–15 min

Now you’ll use DevTools to **see** the box model.

### 1. Inspect elements on `day3-boxes.html` (5–10 min)

- Open `day3-boxes.html` in your browser.
- Right-click on “Box One” → Inspect.
- In the DevTools **Elements** panel:
  - Ensure `.box.box-one` is selected.
  - Look for the **box model diagram** (usually in a “Layout” or “Computed” or “Styles” section).
    - It should show margin, border, padding, and content sizes.

Play with it:

- Change `padding` or `margin` live in DevTools (in the Styles panel).
- Watch the box model diagram update.
- Notice how total space taken up by the element changes.

### 2. Inspect an element on `day3-article.html` (5 min)

- Open `day3-article.html`.
- Inspect:
  - The `<header>` element.
  - The `<main>` element.
  - One of your `.highlight-section` elements.

For each, observe:

- Margin: Is there space around the element?
- Padding: Is there space inside around its content?
- Border: Is there a visible border?

This links the abstract box model idea with the real page.

---

## Part 5 – Reflection – 5–10 min

In `notes-day3.txt` in `week1/day3/`, answer:

1. In your own words, describe the **box model**.  
   Mention content, padding, border, margin.
2. What is the difference between **margin** and **padding** in terms of:
   - Where the space appears?
3. Which CSS properties did you use today that felt most useful or interesting?

Optional: Write down one or two lines of CSS that you want to remember (e.g., the pattern for margin, padding, basic font settings).

---

## Optional Mini Challenges (if you have extra time)

1. **Add a navigation bar style to your article page:**
   - In HTML, ensure you have:

     ```html
     <header>
       <h1>My Blog</h1>
       <nav>
         <a href="#">Home</a>
         <a href="#">Articles</a>
         <a href="#">About</a>
       </nav>
     </header>
     ```

   - In CSS:

     ```css
     header {
       display: flex;
       justify-content: space-between;
       align-items: center;
     }

     nav a {
       margin-right: 1rem;
     }

     nav a:last-child {
       margin-right: 0;
     }
     ```

   (You’re getting a tiny preview of Flexbox for tomorrow.)

2. **Experiment with text alignment:**
   - Center one of your headings:

     ```css
     h2 {
       text-align: center;
     }
     ```

   - Make one paragraph justified:

     ```css
     .justified {
       text-align: justify;
     }
     ```

   - Add `class="justified"` to a paragraph in HTML and see the effect.

---

If you’d like, next I can create a detailed, structured guide for **Day 4 of Week 1**, where you go deeper into layout with **Flexbox** and start making a more realistic page layout.
