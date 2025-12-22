### Day 2 – HTML Structure & Semantic Tags

**Theme:** Move from “just making things appear” to structuring pages in a way that is meaningful, maintainable, and ready for real apps.

**Estimated time:** 2–3 hours  

---

## 1. Learning Objectives

By the end of Day 2 you should be able to:

1. Explain what **semantic HTML** is and why it matters (accessibility, SEO, maintainability).
2. Use common **layout/structural tags**:  
   `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<footer>`.
3. Use **attributes** like `id`, `class`, `href`, `src`, `alt` correctly.
4. Create a **multi-section page** with internal navigation (links that scroll to sections).
5. See how a well-structured HTML page sets you up for later CSS, JavaScript, React, and backend integration.

---

## 2. Conceptual Foundations (Learn)

Spend ~45–60 minutes here, with brief notes (bullet points, not essays).

### 2.1 Semantic HTML: What and Why

**Non-semantic vs semantic:**

- **Non-semantic** tags:
  - `<div>` – generic block container.
  - `<span>` – generic inline container.
  - They say nothing about what the content *means*.

- **Semantic** tags:
  - `<header>` – introductory content or a set of navigational links.
  - `<nav>` – section with navigation links.
  - `<main>` – the main content unique to that page.
  - `<section>` – thematically grouped content.
  - `<article>` – self-contained, independent piece of content (blog post, news article, card).
  - `<aside>` – tangentially related content (sidebar, related links).
  - `<footer>` – footer for a section or document.

**Why semantic HTML matters:**

- **Accessibility:**  
  Screen readers and assistive devices rely on structure to help users navigate.
- **SEO / Search engines:**  
  Semantic structure helps search engines understand your content.
- **Maintainability / readability:**  
  Other developers (or you, in 3 weeks) can quickly understand the layout.
- **Foundation for styles and JS:**  
  Clean structure makes CSS and JavaScript interactions easier and less fragile.

---

### 2.2 Page Structure Patterns

A very common **high-level layout pattern**:

```html
<body>
  <header>
    <!-- Logo, site title, nav menu -->
  </header>

  <main>
    <!-- Main content: sections, articles, etc. -->
  </main>

  <footer>
    <!-- Footer content -->
  </footer>
</body>
```

Inside `<main>`, we often have:

```html
<main>
  <section id="hero">
    <!-- Big intro/hero section -->
  </section>

  <section id="about">
    <!-- About content -->
  </section>

  <section id="features">
    <!-- Key features, services, etc. -->
  </section>

  <section id="contact">
    <!-- Contact info or form -->
  </section>
</main>
```

For content that stands alone, like a blog post:

```html
<article>
  <header>
    <h2>Article Title</h2>
    <p>Published on ...</p>
  </header>
  <p>Article body...</p>
  <footer>
    <p>Tags: HTML, CSS</p>
  </footer>
</article>
```

---

### 2.3 Attributes: id, class, href, src, alt

- `id` – a unique identifier within a page.
  - Used for:
    - CSS hooks (`#about { ... }`).
    - JS hooks (`document.getElementById('about')`).
    - Internal navigation: `<a href="#about">Go to About</a>`.

- `class` – reusable label for elements.
  - Used for:
    - Styling groups of elements (`.card { ... }`).
    - JS operations on groups.

- `href` (on `<a>`) – target of a link.
  - Example: `<a href="https://example.com">Visit</a>`
  - Internal link: `<a href="#contact">Contact</a>`

- `src` (on `<img>`, `<script>`, etc.) – source of external resource.
  - Example: `<img src="avatar.jpg" alt="My avatar" />`

- `alt` (on `<img>`) – text alternative describing the image.
  - Important for accessibility and when images fail to load.

---

## 3. Hands-On Work (Do)

Spend 60–90 minutes. You’ll build a simple “About Me” page with semantic structure and internal navigation.

### 3.1 Set Up a New File

1. Open your **Week 1** folder (e.g. `fullstack-week1-day1/` or create a `week1/` folder if you prefer).
2. Create a new file: `about-me.html`.

### 3.2 Add Boilerplate + Basic Structure

Type this (from scratch, don’t paste):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>About Me</title>
  </head>
  <body>
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
        <p>Write a short paragraph about yourself here.</p>
      </section>

      <section id="hobbies">
        <h2>Hobbies</h2>
        <ul>
          <li>Hobby one</li>
          <li>Hobby two</li>
          <li>Hobby three</li>
        </ul>
      </section>

      <section id="contact">
        <h2>Contact</h2>
        <p>Email: your-email@example.com</p>
      </section>
    </main>

    <footer>
      <p>© 2025 Your Name</p>
    </footer>
  </body>
</html>
```

Now:

- Open `about-me.html` in your browser.
- Click the nav links and see the page jump to each section.

---

### 3.3 Add More Semantic Detail

1. **Add an “Experience” or “Projects” section**

Inside `<main>`, before the contact section, add:

```html
<section id="projects">
  <h2>Projects</h2>

  <article>
    <h3>Project 1: Portfolio Website</h3>
    <p>A simple personal portfolio built with HTML and CSS.</p>
  </article>

  <article>
    <h3>Project 2: To-Do App</h3>
    <p>
      A basic task manager built with JavaScript that lets you add and remove
      tasks.
    </p>
  </article>
</section>
```

Update your nav:

```html
<nav>
  <a href="#about">About</a>
  <a href="#hobbies">Hobbies</a>
  <a href="#projects">Projects</a>
  <a href="#contact">Contact</a>
</nav>
```

2. **Use `id` and `class` attributes**

Add some classes for future styling (even though you won’t style much today):

```html
<header class="site-header">
  <h1 class="site-title">Your Name</h1>
  <nav class="site-nav">
    <!-- links -->
  </nav>
</header>

<main class="site-main">
  <!-- sections -->
</main>

<footer class="site-footer">
  <p>© 2025 Your Name</p>
</footer>
```

You don’t need to create CSS yet, but setting up classes prepares your HTML for styling and JS.

---

### 3.4 Internal vs External Navigation

Practice both:

1. **Internal link (to a section on the same page)**

Already done with `href="#about"`, `href="#projects"`, etc.

2. **External link**

Add a small section or paragraph somewhere:

```html
<section id="learning">
  <h2>What I'm Learning</h2>
  <p>
    I am following a full-stack web development roadmap that includes
    <a href="https://developer.mozilla.org/">MDN Web Docs</a>
    and other resources.
  </p>
</section>
```

Note the difference:
- `href="#about"` → scrolls to a location on the current page.
- `href="https://developer.mozilla.org/"` → goes to another website.

---

### 3.5 Mini-Experiment: Misusing vs Using Semantics

Create a small snippet in a **separate file** called `semantic-test.html`:

**Version A (non-semantic):**

```html
<div>
  <div>My Blog</div>
  <div>
    <div>First Post</div>
    <div>This is my first blog post.</div>
  </div>
</div>
```

**Version B (semantic):**

```html
<header>
  <h1>My Blog</h1>
</header>
<main>
  <article>
    <h2>First Post</h2>
    <p>This is my first blog post.</p>
  </article>
</main>
```

Just look at them side by side and ask yourself:  
If you came back in 1 month, which would you rather read and maintain?

This is the *feel* you want for all your HTML.

---

## 4. Reflection & Consolidation

Spend ~10–15 minutes writing answers in your notes file (e.g. `notes-day2.md`).

1. In your own words:
   - What is **semantic HTML**?
   - Why use `<section>` or `<article>` instead of `<div>` for everything?

2. Describe:
   - The role of `<header>`, `<main>`, and `<footer>`.
   - When you might use `<article>` instead of `<section>`.

3. Attributes:
   - What is the difference between `id` and `class`?
   - Give one example where you’d use `id` and one where you’d use `class`.

4. Navigation:
   - How do `id` and `href="#something"` work together to create internal navigation?

5. Self-assessment:
   - Which tags do you feel comfortable with now?
   - Which tags or concepts still feel a bit fuzzy?

---

## 5. Practice Questions (Increasing Difficulty)

Use these after you’ve done the hands-on work. Attempt from memory first; then verify with docs if needed.

### 5.1 Basic Concept Check (Level 1 – Recall)

1. What does **“semantic HTML”** mean?
2. Name three semantic tags used for page layout and say what they’re generally used for.
3. What’s the difference between `<section>` and `<article>` at a high level?
4. What is the purpose of the `alt` attribute on an image?
5. What is the difference between the `id` and `class` attributes in HTML?

---

### 5.2 Applied HTML Structure (Level 2 – Apply)

6. Write the HTML structure for a simple page that includes:

   - A header with the title “My App”.
   - A navigation with links to sections: Home, Features, Contact.
   - A main area with three sections (home, features, contact).
   - A footer with a copyright notice.

   Don’t worry about content beyond simple headings/paragraphs.

7. You want to create two blog posts on a page. Each post should be:

   - An `article`.
   - Contain a heading, a publish date, and a paragraph of text.

   Write the HTML for one post and then duplicate it for the second, changing the title/date.

8. You want a navigation bar where clicking “Contact” scrolls to the contact section.  
   Which attributes and values do you use in:
   - The `a` tag?
   - The section tag?

   Write the minimal HTML for both pieces.

---

### 5.3 Structuring Realistic Content (Level 3 – Design & Reason)

9. You’re building a **product landing page** with:

   - A big hero section (headline, short description).
   - A “Features” section with three core features.
   - A “Testimonials” section with quotes from users.
   - A “Pricing” section.
   - A “FAQ” section.

   - Which tags would you use to structure this page at the top level (`header`, `main`, etc.)?
   - Within `main`, how would you group the different sections? Which ones could reasonably use `<article>`?

10. You have a layout with a main content area and a sidebar containing:
    - Related articles
    - Newsletter signup
    - Small profile bio

    - Which semantic tag might you use for the **sidebar**?
    - Why is that preferable to a `<div>`?

11. Consider this HTML:

    ```html
    <div>
      <h1>My Site</h1>
      <a href="#section1">Go to section 1</a>
      <a href="#section2">Go to section 2</a>
    </div>

    <div id="section1">
      <h2>Section 1</h2>
      <p>Some info.</p>
    </div>

    <div id="section2">
      <h2>Section 2</h2>
      <p>Some other info.</p>
    </div>
    ```

    Rewrite this using more semantic tags, without changing the visible content.

---

### 5.4 Full-Stack Connections (Level 4 – Conceptual Bridge)

These link today’s HTML structure to your future backend and full-stack work.

12. In a future full-stack app, you might have:

    - A React frontend that renders a layout with `<header>`, `<main>`, `<footer>`.
    - A Node.js/Express backend that sends JSON data.

    Even though React and Express are different layers, how does a clear HTML structure help when:
    - You fetch data and render it into components?
    - You set up client-side routing (e.g., `/about`, `/projects`)?

13. Imagine a blog platform:
    - The backend (Node + MongoDB) stores posts and returns them as JSON:  
      `{ title: "My First Post", date: "...", body: "..." }`

    When this data reaches your frontend, why does mapping each post into an `<article>` make sense semantically and for accessibility?

14. Think about URLs and internal links:
    - Today you used anchors like `href="#contact"` to move within a page.
    - Later you’ll have URLs like `/posts/:id` in an Express app.

    Conceptually, how is “linking to a part of the same page” similar to and different from “linking to another route handled by the backend”?

---

### 5.5 Stretch Coding Exercises (Level 5 – Small Builds)

If you have extra time and want more practice:

15. Create a new file `mini-resume.html` with:

    - `<header>`: Your name and a short tagline.
    - `<main>`:
      - `<section id="summary">` – short bio.
      - `<section id="experience">` – at least 2 job/role entries; each as an `<article>` with a role title, company, and short description.
      - `<section id="skills">` – list of skills.
    - `<footer>`: Contact info and a link to your `about-me.html`.

16. Add an internal table of contents:

    - At the top of `mini-resume.html`, add a `nav` with links to `#summary`, `#experience`, and `#skills`.
    - Clicking each link should scroll to the appropriate section.

17. Challenge yourself to build `about-me.html` again from scratch in a new file `about-me-v2.html`:
    - Same general sections (about, hobbies, projects, contact).
    - But try to improve:
      - Use of `<article>` for projects.
      - Better section ordering.
      - Clearer headings.

Compare the two versions and see if the second one feels more structured.

---

## 6. How Day 2 Supports Full-Stack Skills

Today’s work directly supports later parts of the 12-week roadmap:

- **React components**:  
  JSX uses semantic tags just like HTML. A well-structured HTML mindset makes it easier to design React component trees (e.g., `<Header>`, `<Main>`, `<Footer>`, `<ArticleCard>`).

- **Backend rendering / APIs**:  
  When your Express backend sends HTML or JSON, you’ll map data structures into semantic HTML. For example, each row from a “posts” collection becomes an `<article>`. This alignment makes your app clearer and more maintainable.

- **Accessibility & Professionalism**:  
  Good semantic HTML is a hallmark of a competent developer. It’s often what distinguishes “I copied a tutorial” from “I understand how to structure a real app”.

---

If you’d like next, I can:

- Create a **Day 3** guide focusing on introductory CSS and the box model, or  
- Review (by description or pasted code) your `about-me.html` structure and suggest concrete improvements.
