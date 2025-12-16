**Week 2 Theme:** Layout, responsive design, and Git basics.  
Assume ~2 hours/day (adjust as needed). Continue working in a `week2/` folder.

---

## Day 1 – Review & Deeper CSS Layout

**Objectives:**
- Refresh Week 1 CSS concepts.
- Understand when to use Flexbox vs other layout tools.
- Start planning your improved “About/Portfolio” layout.

### 1. Concept review (25–30 min)
Skim your Week 1 files and notes:
- Box model, Flexbox basics, semantic HTML.
- Identify 1–2 ugly/awkward layout parts you want to fix (e.g., header alignment, spacing).

Read/learn:
- When Flexbox is best:
  - Navbars
  - Centering elements
  - One-dimensional layouts (row OR column)
- The idea of:
  - “Page wrapper” with `max-width` and `margin: 0 auto;`
  - Consistent spacing (using a spacing scale, e.g., 4px/8px/16px etc.)

### 2. Plan improved layout (30–40 min)
Create `week2/notes-day1.txt`:
- Sketch (on paper or text description) your **future portfolio layout**:
  - Header: logo/name + nav
  - Hero section: your name, short tagline, maybe a photo or placeholder image
  - About section: short bio
  - Skills section: maybe 2-column list or cards
  - Projects placeholder section (even if empty for now)
  - Contact/footer

Decide:
- Color palette (3–4 colors)
- Font choices (Heading font vs body font, if you like)

### 3. Practice: layout skeleton (45–60 min)
Create `week2/layout-skeleton.html` + `layout-skeleton.css`:
- Recreate your planned structure using **semantic tags** and **Flexbox** for:
  - Header
  - A simple hero section (centered content)
  - A 2-column “About” section on larger screens

Focus on:
- Using a `.container` class with `max-width` and centered content.
- Clean HTML structure; don’t worry about perfect colors yet.

---

## Day 2 – Responsive Design Basics

**Objectives:**
- Learn simple responsive design patterns.
- Make your layout adjust to small screens.

### 1. Concept (30–40 min)
Learn:
- What “responsive design” means.
- Common responsive techniques:
  - Fluid layouts: `width: 100%`, `max-width`
  - Using `rem`/`em` instead of `px` for font sizes (basic idea)
  - Media queries:

    ```css
    @media (max-width: 768px) {
      /* styles for tablets/phones */
    }
    ```

### 2. Practice: make `layout-skeleton.html` responsive (60–70 min)
In `layout-skeleton.css`:
- Ensure your main container is fluid:
  ```css
  .container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 0 1rem;
  }
  ```

- Add a media query (for ~768px or 600px):
  - Stack columns vertically in the About section.
  - Maybe reduce heading font sizes slightly on very small screens.
  - Adjust header nav to wrap or stack (logo above nav links).

Example:

```css
@media (max-width: 768px) {
  .about-section {
    flex-direction: column;
  }
}
```

### 3. Testing & refinement (20–30 min)
- Resize your browser window manually to see changes.
- Use DevTools device toolbar (toggle device mode) to test on “iPhone” dimensions.

Update `notes-day2.txt`:
- One thing that broke in your layout when you shrank the screen.
- How you fixed it (or plan to fix it).

---

## Day 3 – CSS Details: Colors, Typography, and Reusable Classes

**Objectives:**
- Make your pages look more polished.
- Learn to use classes for consistent design.

### 1. Concept (30–40 min)
Learn:
- Basic color usage:
  - Using hex, rgb, or hsl.
  - Keeping 1–2 main colors + 1 accent color.
- Typography:
  - Setting `font-size`, `line-height`, `font-weight`.
  - Using Google Fonts (optional but nice).
- Reusable utility classes:
  - Example: `.text-center`, `.btn`, `.card`, `.section-title`.

### 2. Practice: style improvements (60–70 min)
On `layout-skeleton.html`/`.css`:
- Define a color palette in comments or CSS variables:

  ```css
  :root {
    --color-bg: #f4f4f4;
    --color-primary: #2c3e50;
    --color-accent: #e67e22;
    --color-text: #333;
  }
  ```

- Apply colors and fonts consistently:
  - Background color for body or hero.
  - Primary color for headings.
  - Accent color for buttons/links.
- Create a `.btn` class:
  ```css
  .btn {
    background-color: var(--color-accent);
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    text-decoration: none;
    display: inline-block;
  }

  .btn:hover {
    opacity: 0.9;
  }
  ```

- Apply `.btn` to a call-to-action in your hero or contact section.

### 3. Reflection (10–15 min)
In `notes-day3.txt`:
- What 1–2 classes did you create that you can reuse later?
- Does your page now have a consistent “style”? If not, what’s missing?

---

## Day 4 – Intro to Git: Version Control Basics

**Objectives:**
- Understand what Git is and why it’s important.
- Initialize a local Git repository for your Week 2 work.

### 1. Concept (30–40 min)
Learn:
- What Git is and what problem it solves (versioning, backup, collaboration).
- Basic Git workflow:
  - `git init`
  - `git status`
  - `git add`
  - `git commit -m "message"`
- The ideas of:
  - Working directory
  - Staging area
  - Repository history

### 2. Practice: initialize Git (45–60 min)
In your `week2/` folder:
1. Open terminal in that folder.
2. Run:
   ```bash
   git init
   git status
   ```
3. Create a `.gitignore` file (even if empty or with something simple like `node_modules/` for future).
4. Stage and commit:
   ```bash
   git add .
   git commit -m "Initial week2 layout and styles"
   ```
5. Make a small change (e.g., change a heading), then:
   ```bash
   git status
   git diff
   git add .
   git commit -m "Tweak heading text"
   ```

### 3. Reflection (10–15 min)
In `notes-day4.txt`:
- In your own words, what are “staging” and “committing”?
- Why is a `.gitignore` file useful?

---

## Day 5 – GitHub: Remote Repositories & Publishing Code

**Objectives:**
- Create a GitHub account (if you don’t have one).
- Push your local repo to GitHub.

### 1. Concept (20–30 min)
Learn:
- What GitHub is (remote hosting for Git repos).
- Difference between Git (local) and GitHub (remote).
- SSH vs HTTPS cloning (you can start with HTTPS for simplicity).
- Basic remote commands:
  - `git remote add origin ...`
  - `git push -u origin main` (or `master`, depending on default branch).

### 2. Practice: push to GitHub (60–70 min)
1. On GitHub:
   - Create a new repository: `week2-layout` (no README or .gitignore, to avoid conflict).
2. In your local `week2/`:
   ```bash
   git branch -M main
   git remote add origin https://github.com/<your-username>/week2-layout.git
   git push -u origin main
   ```
3. Refresh GitHub and verify your files show up.
4. Make a small local change (e.g., add a comment or minor CSS tweak), then:
   ```bash
   git add .
   git commit -m "Small style adjustment"
   git push
   ```

### 3. Optional: GitHub Pages quick publish (15–25 min)
- In the GitHub repo settings, look for **Pages**.
- Set the source to the `main` branch (and root, if needed).
- After a few minutes, visit the provided URL to see your page live.

### 4. Reflection (10 min)
In `notes-day5.txt`:
- Summarize the steps to go from local changes to live on GitHub:
  - local → commit → push → (optional) GitHub Pages.

---

## Day 6 – Building Your Portfolio (v2) Using Everything So Far

**Objectives:**
- Start turning your earlier “About Me” into a more complete portfolio.
- Combine semantic HTML, clean CSS, responsive layout, and Git.

### 1. Planning (20–30 min)
Decide on the sections of your **Portfolio v2**:
- Header: name + nav links (e.g., About, Skills, Projects, Contact).
- Hero: your name, role (e.g., “Aspiring Full Stack Developer”), short intro, call-to-action button.
- Skills: grouped into categories (e.g., Frontend, Backend, Tools).
- Projects: placeholder cards (you’ll fill later with real projects).
- Contact: simple text or a mock form (no backend yet).

Create `week2/portfolio.html` + `portfolio.css`.

### 2. Build structure (60–70 min)
- Use semantic tags and re-usable classes from earlier:
  - `.container` for width.
  - `.section-title`, `.btn`, etc.
- Create a hero section:
  ```html
  <section class="hero">
    <div class="container">
      <h1>Your Name</h1>
      <p>Aspiring Full Stack Web Developer</p>
      <a href="#projects" class="btn">View My Work</a>
    </div>
  </section>
  ```
- Layout:
  - Use Flexbox for header.
  - For skills, maybe use a simple grid-like layout using Flexbox (cards).

### 3. Commit your work (10–15 min)
- In terminal (inside `week2/`):
  ```bash
  git add portfolio.html portfolio.css
  git commit -m "Add initial portfolio structure"
  git push
  ```

### 4. Reflection (5–10 min)
In `notes-day6.txt`:
- List which parts of the portfolio you’ll refine visually tomorrow (e.g., project cards, spacing, colors).

---

## Day 7 – Portfolio (v2) Polish + Responsive Check + Git Workflow

**Objectives:**
- Polish your portfolio page visually.
- Ensure it works well on mobile.
- Practice a full Git workflow.

### 1. Visual polish (45–60 min)
In `portfolio.css`:
- Improve hero section:
  - Background color or gradient.
  - Larger, bold heading.
  - Centered content vertically (using Flexbox or padding).
- Polish skills/projects:
  - Use cards with borders or subtle shadows.
  - Consistent spacing (margin-bottom between sections).
  - Distinguish section titles with font-size/weight.

### 2. Responsive testing (30–40 min)
- Use DevTools Device Mode to simulate phone/tablet.
- Check:
  - Is text readable (not too small)?
  - Does the nav wrap/stack nicely?
  - Are cards stacking properly on small widths?

Adjust with media queries as needed, similar to earlier days.

### 3. Full Git cycle (15–20 min)
- After finishing your changes:
  ```bash
  git status
  git add .
  git commit -m "Polish portfolio styles and responsive behavior"
  git push
  ```
- If using GitHub Pages (for this repo or another), confirm your latest version shows online.

### 4. Weekly reflection (10–15 min)
In `notes-week2-summary.txt`:
- Answer:
  - What parts of CSS/layout do you now feel **comfortable** with?
  - What parts still confuse you (e.g., Flexbox alignment, media queries)?
  - Are you comfortable with:
    - `git init`, `git add`, `git commit`, `git push`?
  - One concrete goal for Week 3 (e.g., “start JavaScript basics confidently”).

---

Next step:  
If you’d like, I can create a **Week 3 day-by-day plan** focused on JavaScript fundamentals (variables, functions, arrays, DOM basics) and adding interactivity to your portfolio.
