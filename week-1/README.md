**Week 1 Theme:** Web basics – HTML, CSS fundamentals, and understanding how the web works.  
Assume ~2 hours/day (adjust up/down as needed). Keep everything in a single folder like `week1/`.

---

## Day 1 – How the Web Works + First HTML Page

**Objectives:**
- Understand client/server, HTTP, and what HTML/CSS/JS each do.
- Create your first HTML page.

**1. Concept (30–40 min)**  
Read/watch and take short notes on:
- What happens when you type a URL in the browser:
  - Browser → DNS → Server → HTTP request → HTTP response → HTML/CSS/JS → Render.
- Roles of:
  - **HTML:** structure/content
  - **CSS:** presentation/style
  - **JavaScript:** behavior/logic

Focus on terms: client, server, request, response, URL, HTTP.

**2. Practice: your first page (60–70 min)**  
Create `day1.html`:
- Add the basic structure:

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8">
      <title>My First Page</title>
    </head>
    <body>
      <h1>Hello, Web!</h1>
      <p>This is my first web page.</p>
    </body>
  </html>
  ```

- Add more content:
  - At least 3 headings (`h1`–`h3`)
  - 2–3 paragraphs
  - 1 image (`<img src="..." alt="...">`)
  - 2–3 links (`<a href="https://...">`)

Open in your browser by double‑clicking or dragging into the browser.

**3. Reflection (10–15 min)**  
Write a short note (plain text file `notes-day1.txt`):
- In your own words: What is a client? What is a server?
- What does HTML do?

---

## Day 2 – HTML Fundamentals & Semantic Structure

**Objectives:**
- Learn core HTML tags.
- Use semantic tags to structure a page.

**1. Concept (30–40 min)**  
Review/learn:
- Basic tags: `h1–h6`, `p`, `a`, `img`, `ul`, `ol`, `li`
- Semantic tags: `header`, `nav`, `main`, `section`, `article`, `footer`
- Forms (overview only): `form`, `label`, `input`, `button` (we’ll use them later)

Look specifically at how semantic tags group content logically.

**2. Practice: simple article layout (60–70 min)**  
Create `day2-article.html` for a fake blog post:
- Layout using semantic tags:

  ```html
  <body>
    <header>
      <h1>My Blog</h1>
      <nav>
        <a href="#">Home</a>
        <a href="#">About</a>
        <a href="#">Contact</a>
      </nav>
    </header>

    <main>
      <article>
        <h2>Article Title</h2>
        <p>Intro paragraph...</p>
        <section>
          <h3>Subheading 1</h3>
          <p>Content...</p>
        </section>
        <section>
          <h3>Subheading 2</h3>
          <p>Content...</p>
          <ul>
            <li>Important point 1</li>
            <li>Important point 2</li>
          </ul>
        </section>
      </article>
    </main>

    <footer>
      <p>© 2025 My Blog</p>
    </footer>
  </body>
  ```

- Add:
  - A second article or a “Related posts” section with an ordered list.
  - At least 3 links (one external, two internal `#` or dummy).

**3. Browser DevTools intro (10–15 min)**  
- Right‑click page → Inspect.
- Click elements in the DOM tree and see how they map to the page.
- Change some text directly in DevTools and see it update.

**4. Reflection (5–10 min)**  
In `notes-day2.txt`:  
- Why might semantic tags (`header`, `main`, etc.) be better than just `<div>` everywhere?

---

## Day 3 – Intro to CSS: Styling Text & The Box Model

**Objectives:**
- Link a CSS file to your HTML.
- Understand and experiment with the box model.

**1. Concept (30–40 min)**  
Learn:
- How to include CSS:
  - External stylesheet `<link rel="stylesheet" href="styles.css">`
- Basic selectors:
  - Element (`p`), class (`.highlight`), ID (`#main-title`)
- Basic properties:
  - `color`, `background-color`, `font-family`, `font-size`, `text-align`
- Box model:
  - `margin`, `border`, `padding`, `width`, `height`

**2. Practice: styling your article (60–70 min)**  
- Create `styles-day3.css`.
- In `day2-article.html`, add in `<head>`:

  ```html
  <link rel="stylesheet" href="styles-day3.css">
  ```

In `styles-day3.css`:
- Style the body:
  - Set a font family (e.g., `font-family: Arial, sans-serif;`)
  - Set a max width and center content:

    ```css
    body {
      max-width: 800px;
      margin: 0 auto;
      line-height: 1.6;
    }
    ```

- Style headings and links:
  - Different colors for `h1`, `h2`.
  - Remove underline from links, change color, add hover color.

- Experiment with box model:
  - Add padding, margin, and border to `article` or `section`.
  - Use DevTools to inspect and see the outlined box model.

**3. Mini experiment (15–20 min)**  
Create `day3-boxes.html` with 3 `<div>`s, each with different:
- `margin`
- `padding`
- `border`
See how changes affect layout.

**4. Reflection (5–10 min)**  
In `notes-day3.txt`:
- Explain the box model in one short paragraph.

---

## Day 4 – Layout with Flexbox

**Objectives:**
- Learn Flexbox basics for layout.
- Create a simple navigation bar and a 2‑column layout.

**1. Concept (30–40 min)**  
Study:
- Flex container: `display: flex`
- Main properties:
  - `flex-direction`
  - `justify-content`
  - `align-items`
- Simple horizontal navbar with Flexbox.
- Basic 2‑column layout (`flex: 1` for flexible columns).

**2. Practice: layout page (60–70 min)**  
Create `day4-layout.html` + `styles-day4.css`:
- Structure:

  ```html
  <body>
    <header class="site-header">
      <div class="logo">MySite</div>
      <nav class="main-nav">
        <a href="#">Home</a>
        <a href="#">Blog</a>
        <a href="#">Contact</a>
      </nav>
    </header>

    <main class="content">
      <section class="main-column">
        <h2>Main Content</h2>
        <p>Some text...</p>
      </section>
      <aside class="sidebar">
        <h3>Sidebar</h3>
        <p>Links or info...</p>
      </aside>
    </main>

    <footer class="site-footer">
      <p>Footer text here</p>
    </footer>
  </body>
  ```

In `styles-day4.css`:
- Make header a flex container:

  ```css
  .site-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    border-bottom: 1px solid #ddd;
  }
  ```

- Make main content a 2‑column layout:

  ```css
  .content {
    display: flex;
    gap: 1rem;
    padding: 1rem;
  }

  .main-column {
    flex: 3;
  }

  .sidebar {
    flex: 1;
  }
  ```

- Add basic styles for body, links, etc.

**3. Quick responsive tweak (15–20 min)**  
Add a simple media query to make columns stack on small screens:

```css
@media (max-width: 600px) {
  .content {
    flex-direction: column;
  }
}
```

**4. Reflection (5–10 min)**  
In `notes-day4.txt`:
- What does `justify-content` control?
- What does `align-items` control?

---

## Day 5 – Building Your “About Me” Page (v1)

**Objectives:**
- Start building your Week 1 main deliverable: an “About Me” page.
- Apply HTML + CSS + Flexbox.

**1. Plan structure (20–30 min)**  
On paper or in a text file, outline sections:
- Header with your name and simple nav
- Main:
  - Short bio
  - Skills list
  - Hobbies or interests
- Footer with contact info (email, links)

**2. Build HTML (50–60 min)**  
Create `about-me.html`:
- Use semantic tags:
  ```html
  <header> ... </header>
  <main>
    <section id="about">...</section>
    <section id="skills">...</section>
    <section id="interests">...</section>
  </main>
  <footer>...</footer>
  ```
- Add actual content:
  - A short bio paragraph.
  - Unordered list of skills/hobbies.
  - Links to any online profiles (GitHub, LinkedIn, etc. – even if empty now).

**3. Add base CSS (40–50 min)**  
Create `about-me.css` and link it in the `<head>`.

- Style body, headings, and paragraphs (fonts, colors).
- Create a simple header using Flexbox (logo/name on left, nav links on right).
- Add spacing with padding/margins between sections.
- Make sure text is readable and not too cramped.

**4. Reflection (10 min)**  
In `notes-day5.txt`:
- What are 1–2 things you want to visually improve tomorrow (colors, layout, etc.)?

---

## Day 6 – Polishing the “About Me” Page (v2) + DevTools

**Objectives:**
- Improve the look and responsiveness of your page.
- Use DevTools to debug/inspect CSS.

**1. Visual improvements (60–70 min)**  
In `about-me.css`:
- Add a simple color palette (background color, text color, accent color).
- Add hover effects on nav links (color change, underline).
- Slight border or background for `skills`/`interests` sections.
- Adjust line-height, font sizes for headings vs body text.

**2. Simple responsive tweak (20–30 min)**  
- Use a media query to adjust layout on small screens:
  - Maybe stack header content vertically on small screens.
  - Increase padding or font-size for mobile readability.

Example:

```css
@media (max-width: 600px) {
  header {
    flex-direction: column;
    align-items: flex-start;
  }

  nav a {
    display: inline-block;
    margin-right: 0.5rem;
  }
}
```

**3. DevTools practice (20–30 min)**  
Open `about-me.html`:
- Use Inspect to:
  - Hover elements and see their box model (margin/padding).
  - Edit CSS live (change color, padding) and then copy good changes back to your file.
  - Toggle on/off styles to see their effect.

**4. Reflection (10 min)**  
In `notes-day6.txt`:
- List 2–3 CSS properties you found most useful this week.
- Note one thing that still feels confusing.

---

## Day 7 – Consolidation & Mini Challenge

**Objectives:**
- Review and consolidate Week 1 concepts.
- Build a small page from scratch without looking at old code at first.

**1. Quick review (20–30 min)**  
Skim your notes from Days 1–6.
Write down (from memory) definitions for:
- Client vs server
- HTML vs CSS roles
- Box model
- Flexbox (what problem it solves)

**2. Mini challenge: simple landing page (60–75 min)**  
Create `day7-landing.html` + `day7-landing.css` **without** copy/pasting from old files for the first attempt.

Requirements:
- Structure:
  - `header` with logo and nav (3–4 links)
  - `main` with:
    - Hero section: big heading, subheading, call-to-action button
    - Features section: 3 columns (or cards) describing features
  - `footer` with simple text
- Styling:
  - Use Flexbox for:
    - Header layout (logo + nav)
    - Features section (3 cards side-by-side on desktop)
  - Simple responsive behavior (cards stack on small screens)
  - Consistent colors and fonts

After you finish:
- Compare with earlier files to see improvement/consistency.

**3. Self-assessment & plan for Week 2 (15–20 min)**  
In `notes-day7.txt`, answer:
- What can you comfortably do now without looking things up?
- What still feels slow/hard (e.g., Flexbox alignment, remembering CSS syntax)?
- One specific goal for Week 2 (e.g., “get more comfortable with Flexbox” or “learn CSS Grid basics”).

---

If you’d like, next I can:
- Turn your Week 2 into a similar structured day‑by‑day plan, focused on more layout, responsive design, and introducing Git.
