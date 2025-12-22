### Day 1 – Web Foundations: How the Web Works + Your First Page

**Theme:** Understand what actually happens when you visit a website, and build your first HTML page from scratch.

**Estimated time:** 2–3 hours  

---

## 1. Learning Objectives

By the end of Day 1 you should be able to:

1. Explain, in simple terms, what happens when you type a URL into a browser.
2. Define key web terms: **client**, **server**, **URL**, **HTTP**, **HTML**, **CSS**, **JavaScript**.
3. Recognize basic **HTML structure** and core tags (`<!DOCTYPE>`, `<html>`, `<head>`, `<body>`, headings, paragraphs, links, images, lists).
4. Set up a minimal developer environment (folder, file, VS Code, browser).
5. Create and view a simple HTML page in your browser.

---

## 2. Conceptual Foundations (Learn)

Spend ~45–60 minutes here. Take short, bullet-style notes—don’t aim to memorize everything.

### 2.1 How the Web Works (Mental Model)

**Key concepts to understand:**

- **Client**  
  - Usually the browser (Chrome, Firefox, etc.).  
  - Makes requests and displays responses.

- **Server**  
  - A computer running special software that listens for requests and sends back responses (HTML, JSON, images, etc.).

- **URL** (Uniform Resource Locator)  
  - The “address” you type in the browser.  
  - Has parts like protocol, domain, path, query string.

  Example:  
  `https://example.com/products?category=books`  
  - `https` → protocol  
  - `example.com` → domain  
  - `/products` → path  
  - `?category=books` → query string

- **HTTP** (HyperText Transfer Protocol)  
  - The language / set of rules clients and servers use to talk.  
  - Client sends an **HTTP request**, server sends an **HTTP response**.

- **Request / Response cycle** (high level)  
  1. You type a URL and hit Enter.  
  2. Browser sends an HTTP **request** to the server: “Give me `/` from `example.com`.”  
  3. Server processes request and sends an HTTP **response** with:
     - A **status code** (e.g., 200 OK, 404 Not Found)
     - A **body** (often HTML, sometimes JSON).

- **HTML, CSS, JavaScript: roles**
  - **HTML** – structure and content (headings, paragraphs, images, forms).
  - **CSS** – visual presentation (colors, layout, fonts).
  - **JavaScript** – behavior (interactivity, dynamic updates, calls to servers).

You don’t need to know all the internals (DNS, TCP/IP) yet—just the basic flow:  
**Browser → Request → Server → Response → Browser renders HTML/CSS/JS.**

---

### 2.2 HTML Basics

**What HTML is:**

- A **markup language** describing the structure of a web page.
- Built from **elements/tags** like `<p>`, `<h1>`, `<a>`, etc.
- Tags usually come in pairs: `<tagname>content</tagname>`.

**Essential tags to know today:**

- Document structure:
  - `<!DOCTYPE html>` – tells the browser this is an HTML5 document.
  - `<html lang="en">` – root element.
  - `<head>` – metadata (title, charset, links to CSS, etc.).
  - `<body>` – everything visible on the page.

- Content:
  - Headings: `<h1>` (largest) to `<h6>` (smallest).
  - Paragraph: `<p>...</p>`
  - Anchor (link): `<a href="https://example.com">Link text</a>`
  - Image: `<img src="image.jpg" alt="Description" />` (note: self-closing)
  - Unordered list: `<ul>`, `<li>`
  - Ordered list: `<ol>`, `<li>`
  - Text emphasis:
    - `<strong>` for important/bold text.
    - `<em>` for emphasized/italic text.

**Attributes:**

- Extra information inside a tag, e.g.:

  ```html
  <a href="https://example.com" target="_blank">Example</a>
  ```

  - `href` – URL to link to.
  - `target="_blank"` – open in new tab.

Focus on recognizing element *structure* and *nesting* (elements can be inside other elements).

---

## 3. Hands-On Work (Do)

Spend 60–90 minutes here. Type *everything* yourself; don’t copy–paste. That repetition is how it sticks.

### 3.1 Set Up Your Environment

1. **Create a project folder**  
   - Name it something like `fullstack-week1-day1/`.

2. **Open the folder in VS Code**  
   - VS Code → File → Open Folder → select `fullstack-week1-day1`.

3. **Create your first HTML file**  
   - File → New File → `index.html` inside that folder.

---

### 3.2 Build a Minimal HTML Page

In `index.html`, type this boilerplate manually (no copy–paste):

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

**Then:**

- Save the file (`Ctrl+S` / `Cmd+S`).
- Open it in your browser:
  - Option 1: Double-click `index.html` in your file explorer.
  - Option 2: In VS Code, right-click `index.html` → “Open with Live Server” if you have that extension.

Observe: you’ve now created a client-side page that the **browser** is rendering directly from a file on your machine.

---

### 3.3 Expand the Page with Basic Content

Now extend the body:

1. **Add more headings and text**

```html
<h2>About Me</h2>
<p>
  I am learning web development to build full-stack applications. This is my
  very first step.
</p>

<h3>My Goals</h3>
<p>
  I want to be able to build websites that look good and actually do something
  useful.
</p>
```

2. **Add a list**

```html
<h3>Technologies I Will Learn</h3>
<ul>
  <li>HTML &amp; CSS</li>
  <li>JavaScript (ES6+)</li>
  <li>React</li>
  <li>Node.js &amp; Express</li>
  <li>MongoDB</li>
</ul>
```

3. **Add a link**

```html
<p>
  One of the best reference sites for web technologies is
  <a href="https://developer.mozilla.org/">MDN Web Docs</a>.
</p>
```

4. **Add an image (optional if you have one handy)**  
   Save an image (e.g. `profile.jpg`) in the same folder and add:

```html
<h3>My Avatar</h3>
<img src="profile.jpg" alt="My profile picture" />
```

If you don’t have an image, skip this or link to an online image (`src="https://..."`).

Refresh the browser after each meaningful change and see what changed.

---

### 3.4 Tiny Experiment: Breaking vs Valid HTML

To understand that HTML is structured, deliberately:

1. Remove a closing `</p>` or `</h2>` and refresh.  
2. Notice how the browser still tries to render, but the layout might look off.  
3. Put it back and observe the fix.

This builds an instinct that **tags must be correctly opened, nested, and closed**.

---

## 4. Reflection & Consolidation

Spend 10–15 minutes writing answers (in a `notes-day1.md` file or a notebook). Use your own words.

1. **Explain the web in your own words:**
   - What is a **client**?
   - What is a **server**?
   - What is a **URL**?
   - What is a **request** and what is a **response**?

2. **HTML understanding check:**
   - What is the difference between `<head>` and `<body>`?
   - Name 3 HTML tags you used today and describe what each is for.
   - What is an **attribute** in HTML? Give an example.

3. **Meta reflection:**
   - What felt confusing today?
   - What concept are you most confident about after Day 1?

Rewriting concepts in your own words dramatically reinforces them.

---

## 5. Practice Questions (Increasing Difficulty)

Use these as mini-exercises and prompts to solidify understanding and gently stretch into full-stack thinking.

### 5.1 Conceptual Questions (Basics)

**Level 1 – Recall**

1. What is the role of a **web browser** in the client–server model?
2. What does **HTTP** stand for, and what is its purpose?
3. Name the three core technologies of the web and state the main purpose of each (HTML, CSS, JavaScript).
4. In an HTML file, where do you put:
   - The page title shown on the browser tab?
   - The content that the user actually sees?

5. What is the difference between:
   - `<h1>` and `<p>`?
   - `<ul>` and `<ol>`?

Try answering without looking things up; check later.

---

### 5.2 Applied HTML Questions

**Level 2 – Apply**

6. Write the minimal valid HTML structure (no need for `<meta>` tags, just the core skeleton) from memory.

7. You want to create a list of your 3 favorite programming languages in HTML.  
   - Which tags do you use?  
   - Write the HTML.

8. You want to create a link to `https://github.com/` that opens in a new tab and says “My GitHub”.  
   - Write the HTML for that link.

9. You want to add a paragraph that includes both bold and italic text:
   - The word “important” should be bold.
   - The word “note” should be italic.
   - Write the HTML.

10. You have an image called `avatar.png` in the same folder as `index.html`.  
   - Write the HTML to display it and describe briefly what the `alt` attribute is for.

---

### 5.3 “Mini Design” Scenarios

**Level 3 – Build a Mental Model**

11. You’re designing the **top section** of a personal site that has:
    - Your name as a big title.
    - A short description under it.
    - A small navigation at the top linking to “About”, “Projects”, and “Contact” sections on the same page.

   - Which HTML tags would you use?
   - How would you structure the navigation so that clicking “About” scrolls down to the About section?

12. Suppose you want to create a “Features” section for an app, with three bullet points:
    - Fast
    - Secure
    - Easy to Use

   - Which HTML structure is more semantically correct:  
     A) Three `<p>` tags; or  
     B) A list (`<ul>` with `<li>`)?
   - Explain your choice.

---

### 5.4 Connecting to Full-Stack Ideas (Preview-style)

These questions extend your Day 1 knowledge into the full-stack world at a conceptual level—don’t worry if they feel a bit abstract; they’re meant to plant seeds.

**Level 4 – Deeper Reasoning**

13. Right now, you’re opening `index.html` directly from your file system (e.g., `file:///C:/.../index.html`).  
    Later, you’ll have a **server** (Node.js/Express) that sends HTML in response to an HTTP request.

   - Conceptually, what’s the difference between:
     - Opening `index.html` from your computer, and
     - The browser requesting `index.html` from a remote server?

14. In a future full-stack app:
    - The **frontend** might send a request to `/api/users` (an API endpoint).
    - The **backend** (Node.js + Express) will handle that request and talk to a **database** (e.g., MongoDB).

   Using today’s “request/response” model, describe:
   - Who is the client?  
   - Who is the server?  
   - Where does the **database** fit into this picture?

15. Imagine you built a form in HTML that lets users “sign up” with a name and email.  
    Today, the form doesn’t “do” anything real.  
    Later, with full-stack skills, what new capabilities would you add on the backend so this becomes a real signup feature?

(This question is about **imagining** the responsibilities of the backend: receiving data, validating, storing in DB, sending a response.)

---

### 5.5 Stretch Coding Exercises

If you have extra time and want more practice:

**Level 5 – Small Tasks**

16. Create a new file `about.html` that includes:
    - A heading with your name.
    - A short bio paragraph.
    - A list of 3 hobbies.
    - A link back to `index.html`.

17. In `index.html`, add a section called “Contact” with:
    - A heading.
    - A paragraph that includes your email address as a mailto link, e.g. `mailto:you@example.com`.

18. Try rebuilding `index.html` **from scratch** without looking at your previous code:
    - Type out the structure, save, and compare with the original.

---

## 6. How This Connects to Full-Stack Development

Even though Day 1 is “just HTML”, you’re already laying foundations that matter later:

- **Understanding the client–server model** prepares you for:
  - Building APIs with Node.js + Express.
  - Knowing why and how your React app will communicate with your backend.

- **Getting comfortable with HTML structure**:
  - Makes React JSX easier (JSX is essentially HTML-like syntax in JavaScript).
  - Helps when you build forms that send data to your backend.

- **Creating and opening a file in the browser**:
  - Is the first step toward serving that file from a real server and, eventually, deploying your app.

---

If you’d like, next I can:
- Turn **Day 2** into a similarly detailed guide (focusing on semantic HTML and page structure), or
- Provide **answers / sample solutions** for the practice questions so you can self-check after attempting them.
