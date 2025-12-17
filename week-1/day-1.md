### Week 1 – Day 1  
**Theme:** How the web works + your very first web page  
**Time target:** ~2 hours (adjust as needed)

---

## High-Level Objectives

By the end of Day 1, you should be able to:

1. Explain in simple terms what happens when you visit a website.  
2. Distinguish between **client**, **server**, **HTML**, **CSS**, and **JavaScript**.  
3. Create and open a **basic HTML page** in your browser.  
4. Use a small set of core HTML tags: headings, paragraphs, links, images.  

Keep everything for today in a folder like:

```text
week1/
  day1/
    day1.html
    notes-day1.txt
```

---

## Block 1 – Concept: How the Web Works (30–40 min)

**Goal:** Build a mental model: “When I type a URL, what actually happens?”

### 1. Vocabulary to understand

As you read/watch (any short beginner-friendly resource), focus on these terms:

- **Client:** Usually your browser (Chrome, Firefox, etc.). It *requests* pages.
- **Server:** A computer on the internet that *sends* back responses (HTML/CSS/JS/data).
- **URL:** The address you type into the browser (e.g., `https://example.com`).
- **HTTP/HTTPS:** The protocol (set of rules) for **request/response** between client and server.
- **Request:** The message your browser sends to ask for a resource (a page, image, etc.).
- **Response:** The message the server sends back (HTML, JSON, an error, etc.).

### 2. “The journey of a web page” (in your own words)

After reading/watching, pause and **summarize this flow** in a text editor (you’ll later paste into `notes-day1.txt`):

1. You type a URL in the browser and hit Enter.  
2. The browser looks up where that domain (e.g., `google.com`) lives (DNS).  
3. The browser opens a connection to the server at that address.  
4. The browser sends an **HTTP request** (e.g., “GET /”).  
5. The server receives the request, prepares a **response** (often HTML), and sends it back.  
6. The browser receives the response, reads the HTML, and then fetches additional resources (CSS, JS, images).  
7. The browser **renders** the page visually, applying CSS and running JavaScript.

Don’t worry about every detail. The important part is: **client asks, server responds, browser renders.**

---

## Block 2 – Your First HTML Page (60–70 min)

**Goal:** Create a real web page and see it in your browser.

### 1. Set up your folder and file (5–10 min)

- Create folder: `week1/day1/`
- Inside `day1/`, create a file called: `day1.html`

Open it in your code editor (VS Code or similar).

### 2. Add the base HTML structure (5–10 min)

Paste this starter:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My First Page</title>
  </head>
  <body>
    <h1>Hello, Web!</h1>
    <p>This is my first web page.</p>
  </body>
</html>
```

**Understand what each part is for:**

- `<!DOCTYPE html>` – tells the browser: “This is an HTML5 document.”
- `<html lang="en">` – wraps everything; `lang` helps with accessibility and SEO.
- `<head>` – contains metadata (not displayed content): title, character encoding, links to CSS, etc.
- `<meta charset="UTF-8" />` – ensures characters (letters/symbols) display correctly.
- `<title>` – what appears in the browser tab.
- `<body>` – everything *visible* on the page (headings, text, images, etc.).

### 3. Open it in a browser (5 min)

- In your file explorer, double‑click `day1.html` or drag it into your browser window.  
- You should see the heading and paragraph.

If it doesn’t display:

- Make sure the file is saved as `.html` (not `.txt`).
- Reload the page in the browser (`Ctrl+R` / `Cmd+R`).

### 4. Add more HTML content (40–45 min)

Now expand your page so you practice key tags.

#### a. Add multiple headings

Under the existing `<p>` in `<body>`, add:

```html
<h2>About This Page</h2>
<p>This page is my first step into web development.</p>

<h3>Things I Will Learn</h3>
<p>Over the next weeks, I will learn how to build full web applications.</p>
```

- Use `h1` for the main title of the page, then `h2`, `h3` as subheadings.

#### b. Add paragraphs that say something specific

Add 2–3 more paragraphs about:

- Why you’re learning web development  
- What you hope to build  
- Any background you’re coming from

Example:

```html
<p>I am learning web development because I want to build my own projects.</p>
<p>I’m especially interested in creating tools that help people be more productive.</p>
```

Write your own words—this helps keep you engaged.

#### c. Add links (`<a>` tags)

Add a small “Links I find useful” section:

```html
<h2>Links I Find Useful</h2>
<p>
  Here are a few websites I may use while learning:
</p>
<ul>
  <li><a href="https://developer.mozilla.org/en-US/" target="_blank">MDN Web Docs</a></li>
  <li><a href="https://www.freecodecamp.org/" target="_blank">freeCodeCamp</a></li>
  <li><a href="https://www.w3schools.com/" target="_blank">W3Schools</a></li>
</ul>
```

- `href` is the URL.
- `target="_blank"` opens link in a new tab (optional, but common).

Also add at least one **internal** link (just a placeholder) like:

```html
<a href="#top">Back to top</a>
```

(You can later add `id="top"` to your `<h1>`.)

#### d. Add an image (`<img>`)

Use a publicly available image URL or download a small image into your `day1` folder.

Example (using a URL):

```html
<h2>A Random Image</h2>
<img
  src="https://via.placeholder.com/300x200"
  alt="Placeholder image with gray background and 300 by 200 text"
/>
<p>This is an example of an image displayed on a web page.</p>
```

If you use a local file (say `my-photo.jpg` in the same folder):

```html
<img src="my-photo.jpg" alt="A photo of me" />
```

Key point: **Always** include descriptive `alt` text.

#### e. Check the structure visually

Reload `day1.html` in your browser:

- Are headings in a clear hierarchy?  
- Do the links work?  
- Does the image appear?  

Don’t worry about styling yet; that’s for later days.

---

## Block 3 – Reflection & Mental Model Check (10–15 min)

**Goal:** Lock in today’s understanding in your own words.

Create a file: `notes-day1.txt` in `week1/day1/` and answer briefly:

1. **What is a client?**  
   (e.g., “The client is …”)

2. **What is a server?**  
   (e.g., “The server is …”)

3. **What does HTML do?**  
   - Try to describe: structure, content, not style.

4. **One thing that was easy today, and one thing that felt new/odd.**

Example structure:

```text
Day 1 – Notes

1. What is a client?
   - ...

2. What is a server?
   - ...

3. What does HTML do?
   - ...

4. Easy vs Hard
   - Easy:
   - Hard/new:
```

Writing this out forces your brain to process, not just consume.

---

## Optional Stretch (if you have extra time, 15–20 min)

**Mini challenge:** Add a simple “table of contents” at the top of your page linking to sections lower down.

1. Give your sections IDs:

```html
<h2 id="about-section">About This Page</h2>
...
<h2 id="links-section">Links I Find Useful</h2>
...
<h2 id="image-section">A Random Image</h2>
```

2. At the top of `<body>`, add:

```html
<h2>Table of Contents</h2>
<ul>
  <li><a href="#about-section">About This Page</a></li>
  <li><a href="#links-section">Useful Links</a></li>
  <li><a href="#image-section">Image</a></li>
</ul>
```

Now clicking those links scrolls to each section.  
This gives you:

- More practice with `id` and `href="#..."`  
- A taste of how navigation works inside a single page.

---

## End-of-Day Checklist

By the end of Day 1, you should have:

- [ ] `week1/day1/day1.html` with:
  - [ ] Correct HTML boilerplate (`<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`)
  - [ ] At least:
    - 1 `h1`, 1–2 `h2`/`h3`
    - 3+ paragraphs
    - 2–3 links (`<a>`)
    - 1 image (`<img>`)
- [ ] `week1/day1/notes-day1.txt` with your own explanations of:
  - [ ] client
  - [ ] server
  - [ ] what HTML does
- [ ] You can open `day1.html` in your browser and describe what you see.

---

If you’d like, next I can:

- Break **Day 2** into similar blocks focused on **semantic HTML** (header/nav/main/section/footer) and a simple blog article structure.
