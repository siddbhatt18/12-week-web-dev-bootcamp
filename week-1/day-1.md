Day 1 is about two things:  
1) understanding the big picture of how the web works, and  
2) creating and exploring your very first HTML page.

Assume ~2 hours total. Keep everything in a folder like `week1/day1/`.

---

## High-Level Objectives for Day 1

By the end of today, you should be able to:

- Explain, in simple terms, what happens when you type a URL into a browser.
- Define “client,” “server,” “request,” and “response.”
- Describe what HTML, CSS, and JavaScript each do.
- Create and open a basic HTML file in your browser.
- Use a few core HTML tags: `html`, `head`, `body`, `h1–h3`, `p`, `a`, `img`.

---

## Part 1 – Concepts: How the Web Works (30–40 min)

### 1. Core ideas to learn

Use any beginner-friendly resource (short article or video) and take brief notes. As you read/watch, focus on these questions:

1. **What is a client?**
   - Typically: your browser (Chrome, Firefox, etc.) on your device.
   - It requests web pages and displays them.

2. **What is a server?**
   - A computer on the internet that “serves” web pages/data when requested.

3. **What happens when you type `https://example.com` and press Enter?**
   - Browser checks DNS → finds the server’s IP address.
   - Browser sends an **HTTP request** to that server.
   - Server processes the request and sends back an **HTTP response** (often HTML).
   - Browser parses the HTML, then loads linked CSS and JavaScript, then displays the page.

4. **What are HTML, CSS, and JavaScript each responsible for?**
   - **HTML** – structure and content (headings, text, images, forms).
   - **CSS** – presentation and styling (colors, layout, fonts, spacing).
   - **JavaScript** – behavior and logic (interactivity, dynamic content).

### 2. Note-taking (5–10 min)

Create a text file `notes-concepts-day1.txt` in `week1/day1/` and write short, clear answers in your own words:

- What is a client?
- What is a server?
- What is an HTTP request?
- What is an HTTP response?
- One–two sentences each on HTML, CSS, and JavaScript.

Keep it simple; you’re building understanding, not writing an essay.

---

## Part 2 – Your First HTML Page (60–70 min)

You’ll create `day1.html`, open it in the browser, and then expand it.

### 1. Set up your folder and file (5–10 min)

- Create folder: `week1/day1/` (if not already).
- Inside it, create a file: `day1.html`.

### 2. Basic HTML structure (copy, then understand) (10–15 min)

Paste this into `day1.html`:

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

Then, line by line, add a comment after each major part (just for today) so you remember what it does:

```html
<!DOCTYPE html> <!-- Tells the browser this is an HTML5 document -->
<html lang="en"> <!-- Root element of the page, language is English -->
  <head> <!-- Contains metadata and the title, not visible content -->
    <meta charset="UTF-8"> <!-- Character encoding, supports most characters -->
    <title>My First Page</title> <!-- Title shown in browser tab -->
  </head>
  <body> <!-- Visible page content goes here -->
    <h1>Hello, Web!</h1> <!-- Main heading -->
    <p>This is my first web page.</p> <!-- Paragraph of text -->
  </body>
</html>
```

### 3. Open it in the browser (5 min)

- On your computer, open `day1.html` in a browser:
  - Either double-click the file, or
  - Right-click → “Open with” → choose browser, or
  - Drag the file into a browser window.

You should see “Hello, Web!” and your paragraph.

### 4. Add more content using core HTML tags (30–40 min)

Now expand `day1.html` so it has:

- At least **3 headings** (`h1`, `h2`, `h3`).
- 2–3 **paragraphs**.
- 1 **image**.
- 2–3 **links**.

Example structure (adjust content to be about you or anything you like):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>My First Page</title>
  </head>
  <body>
    <h1>Welcome to My First Web Page</h1>

    <h2>About Me</h2>
    <p>My name is [Your Name]. I'm starting to learn web development.</p>
    <p>I created this page on my first day of studying HTML.</p>

    <h3>My Goals</h3>
    <p>Some of my learning goals are:</p>
    <p>1) Understand how the web works. 2) Build real projects. 3) Become comfortable with HTML, CSS, and JavaScript.</p>

    <h2>My Favorite Picture</h2>
    <img src="https://via.placeholder.com/300x200" alt="Placeholder image">

    <h2>Useful Links</h2>
    <p>
      <a href="https://developer.mozilla.org/en-US/docs/Web/HTML">HTML Guide on MDN</a><br>
      <a href="https://www.google.com">Google</a><br>
      <a href="https://www.wikipedia.org">Wikipedia</a>
    </p>
  </body>
</html>
```

Key points while you edit:

- **Headings:** use them logically: `h1` for main title, `h2` for sections, `h3` for subsections.
- **Paragraphs (`<p>`):** wrap your text; don’t leave bare text in the `<body>` when you can structure it.
- **Image (`<img>`):**
  - `src` can be any image URL for now.
  - `alt` should be a short text description.
- **Links (`<a>`):**
  - `href="https://..."` for external sites.
  - Clicking should navigate to the page.

After each small change, **save** the file and **refresh** the browser tab to see the effect.

---

## Part 3 – Quick Exploration & Reflection (15–20 min)

### 1. Explore with the browser (5–10 min)

- In your browser:
  - Right-click on the page → choose **“View Page Source”** or **“View Source”**.
  - Confirm you see the HTML you wrote.
- Again, right-click on the page → choose **“Inspect”** (or “Inspect Element”).
  - In the Elements/Inspector tab, click your `<h1>`, `<p>`, and `<img>`.
  - Notice how they highlight on the page.

You don’t need to understand all DevTools features yet; just see that the browser gives you a live view of your HTML.

### 2. Reflection and consolidation (10 min)

Create `notes-day1.txt` in `week1/day1/` and answer:

1. In your own words:
   - What is a **client**?
   - What is a **server**?
2. What does **HTML** do in a web page?
3. What part of Day 1 felt:
   - Easiest?
   - Most confusing or new?

Keep your answers short and simple. This file is only for you; it’s to track your thinking over time.

---

## Optional Mini Challenge (if you have 10–15 extra minutes)

Add one or two of these to `day1.html`:

- A list of your 3 favorite books, movies, or games using:
  - Unordered list:

    ```html
    <h2>My Favorite Books</h2>
    <ul>
      <li>Book 1</li>
      <li>Book 2</li>
      <li>Book 3</li>
    </ul>
    ```

- A second `h2` section with a different topic (e.g., “Why I’m Learning to Code”).

This starts building the habit of expanding beyond the bare minimum.

---

If you want, next I can create a similarly detailed, step‑by‑step guide for **Day 2 of Week 1** (semantic HTML and structuring an article page).
