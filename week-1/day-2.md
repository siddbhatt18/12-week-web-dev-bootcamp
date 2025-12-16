Day 2 builds on Day 1 by going deeper into **HTML structure** and introducing **semantic HTML** (tags that describe meaning, not just appearance).

Assume ~2 hours. Keep files inside `week1/day2/`.

---

## High-Level Objectives for Day 2

By the end of today, you should be able to:

- Use core HTML tags: headings, paragraphs, lists, links, images.
- Understand and apply **semantic tags**: `header`, `nav`, `main`, `section`, `article`, `footer`.
- Build a simple “blog article” style page with a clear structure.
- Use the browser’s DevTools to inspect elements and HTML structure.
- Explain why semantic HTML is better than using `<div>` for everything.

---

## Part 1 – Core HTML & Semantic Tags (Concepts) – 30–40 min

### 1. Review basic tags from Day 1 (5–10 min)

From memory, list in a scratch file (or on paper):

- Headings: `h1`, `h2`, `h3`
- Paragraph: `p`
- Link: `a`
- Image: `img`

Then briefly check an online reference (e.g., MDN) to see if you missed anything important about them.

Focus on:

- `<a href="...">Text</a>` for links.
- `<img src="..." alt="...">` for images.

### 2. Learn list tags (10–15 min)

Study these tags:

- Unordered list (bullets):  
  `ul` (container) and `li` (list item)
- Ordered list (numbered):  
  `ol` and `li`

Example:

```html
<h2>Unordered List</h2>
<ul>
  <li>Item one</li>
  <li>Item two</li>
  <li>Item three</li>
</ul>

<h2>Ordered List</h2>
<ol>
  <li>First step</li>
  <li>Second step</li>
  <li>Third step</li>
</ol>
```

Understand: `ul` vs `ol` only change presentation (bullets vs numbers), not meaning.

### 3. Learn semantic structure tags (15–20 min)

Focus on these tags and what they typically represent:

- `header` – Top section of a page or section (logo, title, navigation).
- `nav` – Navigation links (main menu, sidebar menu).
- `main` – Main content of the page (only one `main` per page).
- `section` – A thematic grouping of content (e.g., “Introduction,” “Features”).
- `article` – A self-contained, standalone piece of content (blog post, news article).
- `footer` – Bottom part (copyright, contact info, site links).

Key idea:

- Semantic tags **describe purpose/meaning**.  
  For example:

  ```html
  <header>My blog title and navigation here</header>
  <main>Main article content here</main>
  <footer>Footer info here</footer>
  ```

  is more meaningful than:

  ```html
  <div>My blog title and navigation here</div>
  <div>Main article content here</div>
  <div>Footer info here</div>
  ```

They help with:

- Accessibility (screen readers understand the page better).
- SEO (search engines understand content structure).
- Human readability (other developers instantly see the layout).

Take brief notes in `notes-day2-concepts.txt`:

- Write one sentence per tag (`header`, `nav`, `main`, `section`, `article`, `footer`) summarizing its use.

---

## Part 2 – Build a Simple Article Page with Semantic HTML – 60–70 min

You’ll create a basic blog-style page using semantic tags and lists.

### 1. Create the files (5 min)

In `week1/day2/`, create:

- `day2-article.html`

You can copy the doctype and `<html>`, `<head>`, `<body>` shell from Day 1, or write it from scratch.

### 2. Set up the basic document structure (5–10 min)

Start with:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>My Blog – Day 2 Article</title>
  </head>
  <body>
    <!-- Content will go here -->
  </body>
</html>
```

### 3. Add page layout using semantic tags (15–20 min)

Inside `<body>`, create a basic layout:

```html
<body>
  <header>
    <h1>My Blog</h1>
    <nav>
      <a href="#">Home</a>
      <a href="#">Articles</a>
      <a href="#">About</a>
      <a href="#">Contact</a>
    </nav>
  </header>

  <main>
    <article>
      <h2>My First Article</h2>
      <p><em>Published on: April 1, 2025</em></p>

      <section>
        <h3>Introduction</h3>
        <p>Write a short intro paragraph about any topic you like.</p>
      </section>

      <section>
        <h3>Main Points</h3>
        <p>Explain 2–3 main points about your topic.</p>
        <ul>
          <li>Point one explained briefly.</li>
          <li>Point two explained briefly.</li>
          <li>Point three explained briefly.</li>
        </ul>
      </section>

      <section>
        <h3>Conclusion</h3>
        <p>Summarize your thoughts in a closing paragraph.</p>
      </section>
    </article>
  </main>

  <footer>
    <p>© 2025 My Blog. All rights reserved.</p>
  </footer>
</body>
```

Then customize:

- Replace placeholder text with your own:
  - Choose any topic: why you’re learning to code, a hobby, a movie you like.
- Add at least one more paragraph in one of the sections.

### 4. Add a second article or related posts section (15–20 min)

Choose one of the two options below.

#### Option A: A second `<article>`

Inside `<main>`, **after the first `article`**, add:

```html
<article>
  <h2>My Second Article</h2>
  <p><em>Published on: April 2, 2025</em></p>

  <section>
    <h3>Another Topic</h3>
    <p>Write a short paragraph on a different topic.</p>
  </section>
</article>
```

#### Option B: A “Related Posts” `section` with an ordered list

Inside `<main>`, after the first `article`, add:

```html
<section>
  <h2>Related Posts</h2>
  <ol>
    <li><a href="#">How I Started Learning to Code</a></li>
    <li><a href="#">My Favorite Learning Resources</a></li>
    <li><a href="#">Things I Want to Build</a></li>
  </ol>
</section>
```

You can also:

- Mix in **both**: a second article and a related posts section.

### 5. Add some links (5–10 min)

Ensure your page includes:

- At least 1 external link (e.g., to MDN, Google, or any relevant site).
- Some internal-style links with `href="#"` as placeholders.

Example modifications:

```html
<nav>
  <a href="#">Home</a>
  <a href="#">Articles</a>
  <a href="https://developer.mozilla.org/en-US/docs/Web/HTML">HTML Docs</a>
  <a href="#">Contact</a>
</nav>
```

Or in “Related Posts”, ensure each list item contains an `<a>`.

### 6. Open and review in browser (5–10 min)

- Open `day2-article.html` in your browser.
- Check:
  - Does the header look like a clear top section?
  - Are your articles and sections logically separated?
  - Do the headings (`h1` vs `h2` vs `h3`) feel like a proper outline?

Think of it like this:

- `h1`: Site title.
- `h2`: Article title or main section.
- `h3`: Subsections of the article.

---

## Part 3 – DevTools: Inspecting Your Structure – 10–15 min

Introduce yourself to DevTools again, this time focusing on semantic structure.

### 1. Open DevTools and inspect (5–10 min)

- Right-click anywhere on `day2-article.html` in the browser → **Inspect**.
- In the **Elements** panel:
  - Click on `<header>`, `<nav>`, `<main>`, `<article>`, each `<section>`, and `<footer>`.
  - Watch the highlighted area on the page as you select each element.

Questions to answer (mentally or in notes):

- Where does the `<header>` start and end?
- What exactly is inside `<main>`?
- How are `section`s nested inside `article`?

### 2. Make a small live edit in DevTools (optional but useful) (5 min)

In DevTools:

- Double-click a heading (`<h2>` text) and change the text.
- Press Enter and see it update on the page.

Remember: changes in DevTools are temporary. They disappear when you refresh.

---

## Part 4 – Reflection: Why Semantic HTML? – 5–10 min

Create `notes-day2.txt` in `week1/day2/` and answer:

1. In your own words:  
   **Why might semantic tags (`header`, `main`, `section`, etc.) be better than just using `<div>` everywhere?**
2. Which tags did you use today that you did **not** use on Day 1?
3. Does the structure of your `day2-article.html` feel similar to an outline you might write for a document? How?

These reflections help lock in the idea that HTML is about **structure and meaning**, not just text on a page.

---

## Optional Mini Challenges (if you have extra 15–20 min)

Choose one or more:

1. **Add an image to your article**
   - Inside one of your sections, add:

     ```html
     <img src="https://via.placeholder.com/400x200" alt="Description of the image">
     ```

2. **Add an internal “Back to top” link**
   - Give your `<header>` an `id`:

     ```html
     <header id="top">
       ...
     </header>
     ```

   - At the end of the page (maybe in the footer), add:

     ```html
     <p><a href="#top">Back to top</a></p>
     ```

   Clicking it should scroll back to the top of the page.

3. **Outline your page like a document**
   - In `notes-day2.txt`, write a simple bullet list outline:
     - `h1`: My Blog
       - `h2`: My First Article
         - `h3`: Introduction
         - `h3`: Main Points
         - `h3`: Conclusion
       - `h2`: Related Posts
   - Compare it to your actual HTML structure.

---

If you’d like, next I can create a detailed, structured guide for **Day 3 of Week 1** (linking a CSS file, styling text, and understanding the box model).
