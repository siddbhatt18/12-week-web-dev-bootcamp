Here’s a **Day 1–Day 7 plan for Week 2**, still focused on HTML/CSS but going deeper into layout, Flexbox, and responsive design.  
Assume ~1.5–3 hours/day. Adjust as needed.

This week’s theme:  
- Take your Week 1 knowledge and **tighten it**.  
- Learn reusable layout patterns.  
- Practice by **rebuilding real components** from reference designs.

You’ll see the same structure: **Learn → Do → Reflect → Stretch**.

---

## Day 1 – Review & Clean Up Week 1 Work

**Goals:**
- Revisit your Week 1 pages with a critical eye.
- Clean up your HTML/CSS structure.
- Start thinking in “components” (reusable patterns).

### 1. Learn (30–45 minutes)

1. Skim-revisit:
   - MDN: “HTML best practices” (search that exact phrase).
   - MDN: “CSS selectors” (skim to confirm you understand element/class/id).

2. Concepts to focus on:
   - Clean, readable HTML:
     - Proper indentation.
     - Semantic tags instead of random `<div>`.
   - CSS organization:
     - Group related rules.
     - Avoid overly specific or repeated selectors.

Write down:
- 3 HTML best practices you want to adopt.
- 2 CSS patterns you’ve seen yourself repeat (e.g. `.card`, `.btn`).

### 2. Do (60–90 minutes)

1. **Open your Week 1 files** (`about-me.html`, `landing.html`, `styles.css`).

2. **HTML cleanup:**
   - Re-indent everything properly (2 spaces or 4 spaces consistently).
   - Check:
     - No orphaned tags (every `<div>` has a closing `</div>`).
     - Headings are hierarchical (no jumping from `<h1>` to `<h4>`).
   - Replace any unnecessary `<div>`s with semantic tags where appropriate.

3. **CSS cleanup:**
   - Group typography rules together, layout rules together, etc.
   - Extract reusable styles:
     - Example: create `.btn` class used for all buttons.
     - Example: create `.container` class used for main width & centering.

   Example:

   ```css
   .container {
     max-width: 960px;
     margin: 0 auto;
     padding: 0 16px;
   }

   .btn {
     display: inline-block;
     padding: 10px 16px;
     background-color: #0070f3;
     color: #fff;
     border-radius: 4px;
     text-decoration: none;
   }

   .btn:hover {
     background-color: #0059c1;
   }
   ```

   - Apply `.container` to main content wrappers.

### 3. Reflect (10–15 minutes)

- In your notes:
  - What repeated CSS patterns did you find?
  - Was your HTML easy or hard to read? Why?

### 4. Stretch (optional, 20–30 minutes)

- Add comments in your CSS, e.g.:

  ```css
  /* Layout */
  /* Typography */
  /* Components */
  ```

- Try to reduce your CSS by removing duplicated rules and using reusable classes.

---

## Day 2 – Deeper Flexbox: Common Layout Patterns

**Goals:**
- Get comfortable with using Flexbox for real UI patterns.
- Create a **navbar** and a **three-column section** with Flexbox.

### 1. Learn (40–60 minutes)

1. Revisit Flexbox:
   - MDN “Basic concepts of flexbox” — scroll through and focus on:
     - `flex-wrap`
     - `flex-basis`
     - `flex-grow`
     - using `gap`.

2. Concepts:
   - Typical patterns:
     - Horizontal navbar: logo + nav links.
     - Card row: 3 cards that wrap on small screens.

Write down:
- What does `flex-wrap: wrap;` do?
- What does `flex: 1;` roughly mean in the context of sibling flex items?

### 2. Do (60–90 minutes)

Create a new file: `flexbox-practice.html` and link to a new `flexbox.css` or reuse your main CSS.

1. **Navbar with Flexbox:**
   - HTML structure:

     ```html
     <header class="site-header">
       <div class="logo">MySite</div>
       <nav class="site-nav">
         <a href="#">Home</a>
         <a href="#">Features</a>
         <a href="#">Pricing</a>
         <a href="#">Contact</a>
       </nav>
     </header>
     ```

   - CSS:

     ```css
     .site-header {
       display: flex;
       justify-content: space-between;
       align-items: center;
       padding: 16px 24px;
       background-color: #111;
       color: #fff;
     }

     .site-nav a {
       color: #fff;
       text-decoration: none;
       margin-left: 16px;
     }
     ```

   - Experiment with `justify-content` and `align-items`.

2. **Three-column features row:**

   ```html
   <section class="features-row">
     <div class="feature-card">Feature 1</div>
     <div class="feature-card">Feature 2</div>
     <div class="feature-card">Feature 3</div>
   </section>
   ```

   ```css
   .features-row {
     display: flex;
     gap: 16px;
     padding: 24px;
   }

   .feature-card {
     flex: 1;
     border: 1px solid #ccc;
     padding: 16px;
     background-color: #fff;
   }
   ```

3. **Experiment:**
   - Add `flex-wrap: wrap;` to `.features-row` and narrow the browser window.
   - Change width of `.feature-card` using `flex-basis` and see how they behave.

### 3. Reflect (10–15 minutes)

- Which feels easier now: manually setting widths or using Flexbox and `flex`?
- Write one real-world layout you think you can now build with Flexbox.

### 4. Stretch (optional, 20–30 minutes)

- Rebuild the header of a website you like (open it, inspect it, copy the structure with your own style).
- Try to align logo left, links center, and a “Sign Up” button right inside the same Flexbox header.

---

## Day 3 – Responsive Nav + Mobile Menu (Simple Version)

**Goals:**
- Enhance your navbar to handle small screens.
- Learn a common pattern: turning a horizontal menu into a vertical stacked menu.

### 1. Learn (30–45 minutes)

1. Concepts:
   - Mobile-first thinking: start with a simple vertical layout, enhance for desktop.
   - Hiding and showing elements with CSS (e.g. `display: none;` at certain widths).

2. Read:
   - MDN “Media queries” (focus on a couple of usage examples).
   - Google: “CSS responsive navbar flexbox” and skim one tutorial (don’t copy blindly; understand the idea).

Write down:
- Which breakpoint you’ll use for your navbar (e.g. `768px`).
- Your chosen behavior: on small screens, nav links stack vertically (no JS yet).

### 2. Do (60–90 minutes)

Continue from `flexbox-practice.html` or integrate into your `landing.html`.

1. **Start mobile-first:**
   - In CSS, assume **mobile by default**:
     - `.site-header` is a column:
       ```css
       .site-header {
         display: flex;
         flex-direction: column;
         align-items: flex-start;
       }

       .site-nav a {
         display: block;
         margin: 4px 0;
       }
       ```

2. **Add desktop enhancement via media query:**

   ```css
   @media (min-width: 768px) {
     .site-header {
       flex-direction: row;
       justify-content: space-between;
       align-items: center;
     }

     .site-nav a {
       display: inline-block;
       margin: 0 0 0 16px;
     }
   }
   ```

   - Test different widths with DevTools device toolbar.

3. **Polish styling:**
   - Add hover effects.
   - Ensure padding and spacing look good both on mobile and desktop.

### 3. Reflect (10–15 minutes)

- Compare your Day 1 navbar to today’s. What’s better now?
- Did mobile-first feel different than starting from desktop?

### 4. Stretch (optional, 20–40 minutes)

Without JavaScript, simulate a “hamburger menu” conceptually:

- For screens below ~600px:
  - Hide nav links.
  - Show a fake “Menu” text or icon (just a `<div>`).
- For now, don’t make it clickable; just set up the CSS so you understand what would be needed to toggle.

---

## Day 4 – Recreating a Real-World Section from a Design

**Goals:**
- Practice turning a visual reference into HTML/CSS.
- Improve attention to detail: spacing, typography, alignment.

### 1. Learn (20–30 minutes)

1. Choose a simple reference:
   - Pick a clean product landing page or section (e.g., a “features” or “pricing” section).
   - You can use Dribbble, Behance, or even a live website.
   - Screenshot or keep it open in a separate window.

2. Concepts:
   - Translating design → structure:
     - Identify sections, headings, subheadings, buttons, cards.
   - Thinking in boxes:
     - Draw rectangles around groups (mentally or on paper).

Write down:
- What obvious sections you see (e.g. title, subtitle, 3 cards in a row).
- Rough HTML structure you’ll use.

### 2. Do (60–90 minutes)

Create `recreate-section.html` and link a CSS file.

1. **HTML first (no CSS yet):**
   - Create semantic structure:
     - A `<section>` with a container.
     - Heading, subheading.
     - A row of cards (use `<div class="card">` or similar).
   - Don’t worry about exact text; approximate from the design.

2. **Add CSS:**
   - Use Flexbox for the row.
   - Use your existing `.container` class if you have one.
   - Adjust:
     - Heading font size, weight.
     - Colors (approximately).
     - Padding and margins between elements.

3. **Compare with reference:**
   - Toggle between your prototype and the reference screenshot.
   - Try to get:
     - Similar spacing between heading and cards.
     - Rough card dimensions and alignment.

### 3. Reflect (10–15 minutes)

- What did you find hardest to match: spacing, fonts, or layout?
- List 3 small differences you notice between your version and the reference.

### 4. Stretch (optional, 20–30 minutes)

- Add a responsive version:
  - At small widths, stack cards vertically.
- Tweak your CSS until the **visual rhythm** (spacing between items) feels clean and balanced.

---

## Day 5 – Forms & Basic Form Styling

**Goals:**
- Build an accessible HTML form.
- Make forms visually clean with CSS.

### 1. Learn (40–60 minutes)

1. Concepts:
   - Basic form elements:
     - `<form>`, `<label>`, `<input>`, `<textarea>`, `<select>`, `<option>`, `<button>`.
   - Why labels matter (accessibility).
   - Input types: `text`, `email`, `password`, `number`.
   - Basic validation attributes: `required`, `min`, `max`.

2. Read:
   - MDN “Your first form”.
   - MDN pages for `<label>` and `<input>` (skim examples).

Write down:
- The correct way to associate a label with an input (`for` + `id`).
- 3 different `type` values for `<input>` and what they’re for.

### 2. Do (60–90 minutes)

Create `contact-form.html` with a linked CSS file.

1. **Build a contact/signup form:**
   - Fields:
     - Name (text)
     - Email (email)
     - Subject (text)
     - Message (textarea)
   - Use `<label>` properly:

     ```html
     <label for="name">Name</label>
     <input id="name" type="text" name="name" required />
     ```

2. **Style the form:**

   ```css
   form {
     max-width: 400px;
     margin: 40px auto;
   }

   label {
     display: block;
     margin-bottom: 4px;
     font-weight: 600;
   }

   input, textarea {
     width: 100%;
     padding: 8px;
     margin-bottom: 16px;
     border: 1px solid #ccc;
     border-radius: 4px;
     font: inherit;
   }

   button {
     padding: 10px 16px;
     background-color: #0070f3;
     border: none;
     border-radius: 4px;
     color: #fff;
     cursor: pointer;
   }

   button:hover {
     background-color: #0059c1;
   }
   ```

3. **Experiment:**
   - Change border colors on `:focus` so the user can see where they’re typing.
   - Add `placeholder` text to inputs and consider: does it add or reduce clarity?

### 3. Reflect (10–15 minutes)

- How does using `<label>` improve usability (especially for screen readers)?
- What part of the form styling felt most confusing?

### 4. Stretch (optional, 20–30 minutes)

- Add a simple two-column layout on wider screens:
  - Name + Email side by side using Flexbox.
  - Subject + Message full width below.
- Add basic HTML validation attributes (e.g. `required`, `minlength`).

---

## Day 6 – Mini Project: “Profile Card Grid” (Component Thinking)

**Goals:**
- Think in “components” (reusable card layout).
- Use Flexbox + responsive design to create a grid of profile cards.

### 1. Learn (20–30 minutes)

1. Concepts:
   - Component thinking:
     - A “card” with image, name, description, and button is a reusable pattern.
   - Reuse: one `.card` style, many instances.

2. Look at examples:
   - Google “CSS card layout examples” and pick one design to loosely follow.

Write down:
- What elements every card will have (e.g. image, name, role, short bio, button).
- How many cards you’ll display (e.g. 4–6).

### 2. Do (60–90 minutes)

Create `profile-grid.html`.

1. **HTML:**

   ```html
   <main class="container">
     <h1>Meet the Team</h1>
     <section class="card-grid">
       <article class="card">
         <img src="..." alt="Person 1" />
         <h2>Person Name</h2>
         <p>Short description about this person.</p>
         <a href="#" class="btn">View Profile</a>
       </article>
       <!-- Repeat for 3–5 more cards -->
     </section>
   </main>
   ```

   (You can use placeholder images from `https://via.placeholder.com/150`.)

2. **CSS:**
   - Use Flexbox or CSS Grid for `.card-grid`:
     - If using Flexbox:

       ```css
       .card-grid {
         display: flex;
         flex-wrap: wrap;
         gap: 16px;
         margin-top: 24px;
       }

       .card {
         flex: 1 1 calc(33.333% - 16px);
         border: 1px solid #ddd;
         border-radius: 8px;
         padding: 16px;
         background-color: #fff;
       }
       ```

   - Make cards look consistent:
     - Ensure images are same size.
     - Align text.
     - Use consistent margins.

3. **Responsive behavior:**
   - At small widths, stack cards:

     ```css
     @media (max-width: 768px) {
       .card {
         flex: 1 1 100%;
       }
     }
     ```

### 3. Reflect (10–15 minutes)

- Did you define styles once and reuse them, or did you repeat yourself?
- Could you plug this card grid into another website easily?

### 4. Stretch (optional, 20–30 minutes)

- Add hover effects on cards (e.g. slight shadow, scale up).
- Try refining typography (e.g. name larger, role italic, etc.).

---

## Day 7 – Week 2 Mini Project: Refined Landing Page v2

**Goals:**
- Rebuild or significantly improve your Week 1 landing page using everything from Week 2.
- Practice designing and implementing a more polished layout.

### 1. Plan (20–30 minutes)

Decide:  
- Either rebuild your original landing page from scratch as “v2”,  
- Or create a new landing page for a different product/service.

Sketch or outline:
- Header: responsive nav using Flexbox.
- Hero: heading, subheading, call-to-action button, maybe an image.
- Features: 3 cards in a row on desktop, stacked on mobile.
- Testimonials or team section (card grid).
- Contact form at the bottom.
- Footer.

Write down:
- Which breakpoints you’ll use (e.g. 768px and maybe 480px).
- Which reusable components you’ll have (e.g. `.container`, `.card`, `.btn`).

### 2. Do – Build / Rebuild (90–120 minutes)

Create `landing-v2.html` and a corresponding CSS file, or reuse your main one but clearly separate sections with comments.

1. **HTML structure (15–30 minutes):**
   - Use semantic layout tags.
   - Add all sections with placeholder text first.
   - Double-check heading levels (`h1` only once; `h2` for main sections).

2. **Desktop styling (45–60 minutes):**
   - Implement:
     - Flexbox header (logo + nav).
     - Hero with text on left and image on right (Flexbox).
     - Features row using Flexbox.
     - Team/testimonial grid (like Day 6).
     - Contact form (Day 5 patterns).
   - Focus on:
     - Consistent spacing.
     - Clean typography hierarchy.
     - Reuse classes like `.container`, `.card`, `.btn`.

3. **Responsive adjustments (30–40 minutes):**
   - Add at least one media query (e.g. max-width: 768px):
     - Stack hero content.
     - Stack features cards.
     - Make nav vertical if needed.
   - Test on multiple viewport sizes in DevTools.

### 3. Self-Review Checklist (20–30 minutes)

Go through:

- Structure:
  - [ ] Semantic tags used where appropriate?
  - [ ] Only one `<h1>`?
  - [ ] Navigation links scroll to sections (`href="#section-id"`)?  

- CSS:
  - [ ] Typography feels consistent: base font size, heading hierarchy.
  - [ ] Reuse `.card`, `.btn`, `.container` or similar, not copy-paste everywhere.
  - [ ] Reasonable use of colors (no random clashing colors).

- Responsiveness:
  - [ ] No horizontal scrolling at mobile widths.
  - [ ] Sections still readable and visually separated on small screens.
  - [ ] Navbar usable on small screens.

Note 3 things you are proud of and 3 things you’d like to improve.

### 4. Reflect (10–15 minutes)

In your notes:
- How does this v2 landing page compare to your Week 1 attempt?
- Which CSS concept “clicked” for you this week?
- What still feels confusing or magic?

### 5. Stretch (optional, 30–45 minutes)

- Add simple transitions:
  - Button hover transitions:
    ```css
    .btn {
      transition: background-color 0.2s ease, transform 0.1s ease;
    }

    .btn:hover {
      transform: translateY(-1px);
    }
    ```
- Add smooth scrolling for nav links (`scroll-behavior: smooth;` on `html` or `body`).
- Validate your HTML and CSS with online validators and fix warnings.

---

If you’d like, next I can give you:
- A detailed **Week 3** daily plan (JavaScript fundamentals), or  
- A “code review checklist” you can use every time you finish a small project.
