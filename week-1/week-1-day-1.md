# Week 1, Day 1: HTML Structure Fundamentals

## Today's Learning Objective
By the end of today, you'll understand how to structure a basic HTML document and use the most essential HTML elements to create the skeleton of a webpage.

---

## 🎯 Why This Matters (2 minutes read)

HTML is the backbone of every website you've ever visited. While it might seem simple, understanding proper HTML structure is like learning the foundation of a house—everything else builds on top of it. Today, you're learning the 20% of HTML that you'll use 80% of the time.

**Real-world impact**: Every website, web app, and online platform starts with HTML. Master this, and you've taken your first real step into web development.

---

## 📚 Core Concepts for Today

### 1. What is HTML? (Understanding Phase - 15 minutes)

**HTML = HyperText Markup Language**

Think of HTML as the skeleton of a webpage:
- **Skeleton (HTML)**: Structure and content
- **Skin (CSS)**: How it looks (you'll learn this in Days 3-5)
- **Muscles (JavaScript)**: How it moves/interacts (Week 2)

**HTML uses "tags" to mark up content:**
```html
<tagname>Content goes here</tagname>
```

**Key points:**
- Tags usually come in pairs (opening and closing)
- The closing tag has a forward slash: `</tagname>`
- Some tags are self-closing (you'll see these soon)

---

### 2. Basic HTML Document Structure (20 minutes)

Every HTML page follows this template. **Type this out** (don't copy-paste—muscle memory matters):

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My First Webpage</title>
</head>
<body>
    <!-- Your visible content goes here -->
    <h1>Hello, World!</h1>
    <p>This is my first webpage.</p>
</body>
</html>
```

**Let's break this down:**

| Element | Purpose | Why It Matters |
|---------|---------|----------------|
| `<!DOCTYPE html>` | Tells browser this is HTML5 | Always include at the top |
| `<html>` | Root element, wraps everything | Contains all your HTML |
| `<head>` | Metadata (not visible on page) | Settings, title, CSS links |
| `<meta charset="UTF-8">` | Character encoding | Ensures text displays correctly |
| `<meta name="viewport"...` | Mobile responsiveness | Makes site work on phones |
| `<title>` | Page title (shows in browser tab) | Important for SEO & bookmarks |
| `<body>` | All visible content | Everything users see goes here |
| `<!-- comment -->` | Comments (browser ignores) | Notes for you and other developers |

---

### 3. Essential HTML Elements (60 minutes - The Core 20%)

These are the elements you'll use constantly. Focus on understanding WHAT they do and WHEN to use them.

#### **A. Headings (Hierarchy & Structure)**

```html
<h1>Main Title - Use Only Once Per Page</h1>
<h2>Major Section Heading</h2>
<h3>Subsection Heading</h3>
<h4>Smaller Subsection</h4>
<h5>Even Smaller</h5>
<h6>Smallest Heading</h6>
```

**Rules to remember:**
- `<h1>` is the most important (usually your page title)
- Use headings in order (don't skip from h1 to h4)
- Think of them like a table of contents hierarchy

**Real example:**
```html
<h1>John Doe - Web Developer</h1>
<h2>About Me</h2>
<h3>Background</h3>
<h3>Skills</h3>
<h2>Projects</h2>
<h3>Project 1</h3>
<h3>Project 2</h3>
```

---

#### **B. Paragraphs & Text**

```html
<p>This is a paragraph. Use it for blocks of text.</p>

<p>Each paragraph tag creates a new block with spacing.</p>

<strong>This text is bold and important</strong>
<em>This text is italicized for emphasis</em>
<br> <!-- Line break - forces new line -->
```

**When to use what:**
- `<p>`: Any paragraph of text
- `<strong>`: Important text (bold)
- `<em>`: Emphasized text (italic)
- `<br>`: Line breaks (use sparingly—CSS is usually better)

---

#### **C. Links (Connecting Pages)**

```html
<!-- Link to another website -->
<a href="https://www.google.com">Visit Google</a>

<!-- Link to another page in your site -->
<a href="about.html">About Me</a>

<!-- Link to a section on the same page -->
<a href="#contact">Jump to Contact</a>

<!-- Open link in new tab -->
<a href="https://www.github.com" target="_blank">GitHub</a>
```

**Anatomy of a link:**
- `href`: Where the link goes (the destination)
- Text between tags: What users click on
- `target="_blank"`: Opens in new tab (optional)

---

#### **D. Lists (Organizing Information)**

**Unordered List (Bullet Points):**
```html
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>
```

**Ordered List (Numbered):**
```html
<ol>
    <li>First step</li>
    <li>Second step</li>
    <li>Third step</li>
</ol>
```

**When to use:**
- `<ul>`: Items where order doesn't matter (features, skills)
- `<ol>`: Steps, rankings, or sequences

---

#### **E. Images**

```html
<img src="profile.jpg" alt="John Doe headshot">

<!-- With width -->
<img src="logo.png" alt="Company Logo" width="200">

<!-- From the internet -->
<img src="https://example.com/image.jpg" alt="Description">
```

**Key attributes:**
- `src`: Path to the image file
- `alt`: Description (for accessibility and if image fails)
- `width`/`height`: Size in pixels (optional)

**Important:** Always include `alt` text—screen readers use it for visually impaired users.

---

#### **F. Divs & Spans (Containers)**

```html
<!-- div: Block-level container (takes full width) -->
<div>
    <h2>Section Title</h2>
    <p>Section content...</p>
</div>

<!-- span: Inline container (only wraps content) -->
<p>This is <span>highlighted text</span> in a paragraph.</p>
```

**Think of them as:**
- `<div>`: A box that holds multiple elements
- `<span>`: A wrapper for part of text

*(You'll understand these better when we add CSS)*

---

## 🛠️ Hands-On Practice (90 minutes)

### **Exercise 1: Create Your First HTML Page (30 minutes)**

**Task:** Create a file called `index.html` and build a simple "About Me" page.

**Step-by-step:**

1. **Create a folder** on your computer called `web-dev-journey`
2. **Open VS Code** (if you don't have it, download from code.visualstudio.com)
3. **Open the folder** in VS Code (File → Open Folder)
4. **Create a new file** called `index.html`
5. **Type out this structure** (typing > copy/paste):

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>About Me - [Your Name]</title>
</head>
<body>
    <h1>About Me</h1>
    
    <h2>Introduction</h2>
    <p>Hi! My name is [Your Name] and I'm learning web development.</p>
    
    <h2>My Goals</h2>
    <p>I'm learning web development because...</p>
    
    <h2>Favorite Things</h2>
    <ul>
        <li>Thing 1</li>
        <li>Thing 2</li>
        <li>Thing 3</li>
    </ul>
    
</body>
</html>
```

6. **Save the file** (Ctrl/Cmd + S)
7. **Open it in your browser:**
   - Right-click the file in VS Code
   - Select "Open with Live Server" (if installed)
   - OR just double-click the file in your file explorer

**🎉 Congratulations!** You just created your first webpage!

---

### **Exercise 2: Add More Content (30 minutes)**

**Enhance your page with these additions:**

1. **Add an image** of yourself or a placeholder:
```html
<img src="https://via.placeholder.com/150" alt="My photo">
```

2. **Add a "Skills I'm Learning" section** with an ordered list

3. **Add links** to your favorite websites or social media

4. **Add a "Contact" section** with your email as a link:
```html
<h2>Contact</h2>
<p>Email me at: <a href="mailto:your.email@example.com">your.email@example.com</a></p>
```

**Challenge yourself:** Don't look at examples. Try to remember the syntax. Getting it wrong and fixing it is part of learning!

---

### **Exercise 3: Experiment & Break Things (30 minutes)**

**This is crucial for learning. Try these experiments:**

1. **What happens if you:**
   - Delete the closing `</body>` tag?
   - Nest a paragraph inside a heading?
   - Put an image inside a link?
   - Use multiple `<h1>` tags?

2. **Create intentional errors:**
   - Misspell a tag name
   - Forget to close a tag
   - Use quotes incorrectly in href

**Why?** Understanding what breaks and why makes you a better developer. Learn to read browser error messages.

3. **Right-click your page** → "View Page Source"
   - See how the browser reads your HTML
   - This is how you'll debug later

---

## 🧠 Knowledge Check (Self-Quiz)

**Before moving on, can you answer these without looking back?**

1. What does HTML stand for?
2. What goes in the `<head>` vs the `<body>`?
3. What's the difference between `<strong>` and `<em>`?
4. How do you create a link that opens in a new tab?
5. What's the purpose of the `alt` attribute in images?
6. When would you use `<ul>` vs `<ol>`?
7. What are the two parts of an HTML element?

**Can't answer them all?** That's okay! Review those sections before tomorrow.

---

## 📝 Today's Homework (~30 minutes)

### Required:
1. **Create a page about your favorite hobby** using:
   - At least 3 different heading levels
   - 3+ paragraphs
   - One list
   - 2+ links
   - At least one image

2. **Save it as `hobby.html`** in your web-dev-journey folder

### Optional Challenge:
Create a simple recipe page with:
- Recipe title (h1)
- Ingredients list (unordered)
- Instructions (ordered)
- Image of the dish
- Link to source

---

## 🚫 Common Beginner Mistakes (Avoid These!)

| Mistake | Why It's Wrong | Correct Way |
|---------|----------------|-------------|
| `<h1>text<h1>` | Missing closing slash | `<h1>text</h1>` |
| Using `<br>` for spacing | Creates accessibility issues | Use CSS margins (later) |
| `<p><h2>Title</h2></p>` | Can't nest block elements in p | Keep headings outside paragraphs |
| Forgetting `alt` on images | Bad for accessibility | Always include descriptive alt text |
| Using multiple `<h1>` tags | Confuses SEO and screen readers | One `<h1>` per page |

---

## 💡 Pro Tips From Day 1

1. **Indentation matters** (for you, not the browser):
```html
<!-- Good -->
<div>
    <h1>Title</h1>
    <p>Text</p>
</div>

<!-- Bad (works but hard to read) -->
<div>
<h1>Title</h1>
<p>Text</p>
</div>
```

2. **Use VS Code shortcuts:**
   - Type `!` and press Tab → generates HTML boilerplate
   - Ctrl/Cmd + S → Save
   - Alt + Shift + F → Auto-format your code

3. **Install these VS Code extensions** (if you haven't):
   - Live Server (instant preview)
   - Prettier (auto-formatting)
   - Auto Rename Tag

4. **Semantic HTML matters**: Use elements for their intended purpose
   - Headings for headings (not just for big text)
   - Paragraphs for paragraphs (not just any text)
   - Lists for lists (not for layout)

---

## 🔗 Resources for Today

### Must-Read:
- [MDN: Getting Started with HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Getting_started)
- [MDN: HTML Elements Reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

### Optional Videos (if you prefer visual learning):
- "HTML Crash Course" by Traversy Media (1 hour)
- "HTML Tutorial for Beginners" by freeCodeCamp

### Practice Sites:
- [freeCodeCamp Responsive Web Design](https://www.freecodecamp.org/learn/2022/responsive-web-design/)

---

## ✅ End of Day Checklist

Before you close your laptop, make sure you've:

- [ ] Created your `web-dev-journey` folder
- [ ] Built your first `index.html` file
- [ ] Opened it successfully in a browser
- [ ] Completed the "About Me" page
- [ ] Experimented with breaking and fixing code
- [ ] Started the homework assignment
- [ ] Can explain what each part of the HTML boilerplate does

---

## 🎯 Tomorrow's Preview: Day 2 - More HTML Elements

Tomorrow you'll learn:
- Semantic HTML5 elements (header, nav, main, section, footer)
- Tables (for data, not layout)
- Forms basics (getting ready for Week 2)
- How to structure a complete webpage layout

**Get excited!** By the end of Day 2, you'll build a complete resume page structure.

---

## 💬 Reflection Exercise (5 minutes)

Take a moment to write down:

1. **One thing that clicked for you today:**
   _____________________________________

2. **One thing you're still confused about:**
   _____________________________________

3. **One question you want answered tomorrow:**
   _____________________________________

**Why this matters:** Metacognition (thinking about your thinking) accelerates learning. Plus, you'll see your progress when you look back in Week 12.

---

## 🔥 Motivational Note

You just wrote your first lines of code. That page you created? It's real HTML running in a real browser. The same technology powering billion-dollar companies.

It might seem simple, but every expert developer started exactly where you are today. The difference between a beginner and a professional isn't talent—it's showing up tomorrow and doing Day 2.

**You're not learning to code. You're becoming a developer. See you tomorrow! 💪**

---

**Questions or stuck on something?** This is normal! Write down your questions and try to solve them by:
1. Reading error messages carefully
2. Checking your syntax (missing brackets, quotes?)
3. Googling the specific error
4. Comparing your code to working examples

Building debugging skills starts on Day 1!
