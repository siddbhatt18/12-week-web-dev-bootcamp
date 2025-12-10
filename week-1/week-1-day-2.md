# Week 1, Day 2: Semantic HTML & Page Structure

## Today's Learning Objective
By the end of today, you'll understand semantic HTML5 elements and how to structure a complete, professional webpage. You'll build the HTML skeleton of your resume/portfolio page.

---

## 🎯 Why This Matters (2 minutes read)

Yesterday you learned the basic building blocks. Today you're learning **how to organize them properly**.

Think of it this way:
- **Day 1**: You learned individual Lego bricks
- **Day 2**: You're learning how to build actual structures

**Why semantic HTML matters:**
- **SEO**: Google ranks well-structured pages higher
- **Accessibility**: Screen readers understand your page better
- **Maintenance**: Other developers (including future you) understand your code
- **Professionalism**: Separates amateur from professional code

**Real-world impact:** Every job posting for web developers expects knowledge of semantic HTML. It's a non-negotiable fundamental.

---

## 📚 Core Concepts for Today

### 1. What is Semantic HTML? (Understanding Phase - 15 minutes)

**Semantic = Meaningful**

Compare these two examples:

**❌ Non-Semantic (Bad):**
```html
<div class="header">
    <div class="nav">
        <div>Home</div>
        <div>About</div>
    </div>
</div>
<div class="main-content">
    <div class="article">
        <div class="title">My Article</div>
        <div>Content here...</div>
    </div>
</div>
<div class="footer">
    <div>Copyright 2024</div>
</div>
```

**✅ Semantic (Good):**
```html
<header>
    <nav>
        <a href="#home">Home</a>
        <a href="#about">About</a>
    </nav>
</header>
<main>
    <article>
        <h1>My Article</h1>
        <p>Content here...</p>
    </article>
</main>
<footer>
    <p>Copyright 2024</p>
</footer>
```

**The difference:**
- Semantic tags tell you WHAT the content is
- Generic `<div>` tags just create boxes
- Both render the same visually, but semantic is better for machines and humans reading your code

---

### 2. Essential Semantic HTML5 Elements (45 minutes)

These are the **structural elements** you'll use in almost every webpage.

#### **A. `<header>` - Top Section**

```html
<header>
    <h1>Your Name</h1>
    <p>Web Developer</p>
    <nav>
        <a href="#about">About</a>
        <a href="#skills">Skills</a>
        <a href="#projects">Projects</a>
        <a href="#contact">Contact</a>
    </nav>
</header>
```

**When to use:**
- Top of your page
- Contains logo, site title, main navigation
- Can also be used for the header of an `<article>` or `<section>`

**Common mistake:** Using multiple `<header>` elements at the top level (one is usually enough for the page header)

---

#### **B. `<nav>` - Navigation Links**

```html
<nav>
    <ul>
        <li><a href="#home">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#contact">Contact</a></li>
    </ul>
</nav>
```

**When to use:**
- Main site navigation
- Table of contents
- Breadcrumbs
- Pagination

**Pro tip:** Usually contains a list of links (`<ul>` with `<li>` items)

**Common mistake:** Wrapping every single link in a `<nav>`. Reserve it for major navigation sections.

---

#### **C. `<main>` - Primary Content**

```html
<main>
    <!-- All your primary page content -->
    <section id="about">
        <h2>About Me</h2>
        <p>...</p>
    </section>
    
    <section id="skills">
        <h2>Skills</h2>
        <ul>...</ul>
    </section>
</main>
```

**When to use:**
- Wraps the main content of your page
- **Only ONE per page**
- Excludes headers, footers, navigation, and sidebars

**Think of it as:** The unique content of this specific page (not the stuff that appears on every page)

---

#### **D. `<section>` - Thematic Grouping**

```html
<section id="about">
    <h2>About Me</h2>
    <p>I'm a web developer learning full stack development...</p>
    <p>My background includes...</p>
</section>

<section id="experience">
    <h2>Experience</h2>
    <article>
        <h3>Job Title</h3>
        <p>Job description...</p>
    </article>
</section>
```

**When to use:**
- Thematic grouping of content
- Each section should have a heading
- Typically represents a chapter or major topic

**Rule of thumb:** If it deserves its own heading, it's probably a section.

---

#### **E. `<article>` - Self-Contained Content**

```html
<article>
    <h2>My First Blog Post</h2>
    <p>Posted on <time datetime="2024-01-15">January 15, 2024</time></p>
    <p>This is the content of my blog post...</p>
</article>

<article>
    <h3>Project: Portfolio Website</h3>
    <p>Description of the project...</p>
    <a href="link-to-project.com">View Project</a>
</article>
```

**When to use:**
- Blog posts
- News articles
- Forum posts
- Product cards
- Comments
- Individual projects in a portfolio

**The key test:** Could this content be distributed independently? (RSS feed, sharing, etc.)

---

#### **F. `<aside>` - Tangential Content**

```html
<aside>
    <h3>Related Links</h3>
    <ul>
        <li><a href="#">Resource 1</a></li>
        <li><a href="#">Resource 2</a></li>
    </ul>
</aside>

<!-- Or a sidebar -->
<aside class="sidebar">
    <h3>About the Author</h3>
    <p>Quick bio...</p>
</aside>
```

**When to use:**
- Sidebars
- Pull quotes
- Advertisements
- Related links
- Author bios

**Think of it as:** Content related to the main content, but not essential to understanding it.

---

#### **G. `<footer>` - Bottom Section**

```html
<footer>
    <p>&copy; 2024 Your Name. All rights reserved.</p>
    <nav>
        <a href="#privacy">Privacy Policy</a>
        <a href="#terms">Terms</a>
    </nav>
    <div class="social-links">
        <a href="https://github.com/yourusername">GitHub</a>
        <a href="https://linkedin.com/in/yourusername">LinkedIn</a>
    </div>
</footer>
```

**When to use:**
- Bottom of page
- Copyright information
- Contact info
- Secondary navigation
- Social media links

**Note:** Like `<header>`, can be used for footers of articles/sections too.

---

### 3. Section vs Article vs Div - When to Use What? (20 minutes)

This confuses everyone at first. Here's the decision tree:

```
Is it the main navigation? → <nav>
Is it the page header? → <header>
Is it the page footer? → <footer>
Is it the main content area? → <main>

Within main content:
├─ Is it independent/reusable? → <article>
├─ Is it a thematic section? → <section>
├─ Is it tangential/sidebar? → <aside>
└─ Is it just for styling/grouping? → <div>
```

**Practical Examples:**

```html
<!-- Blog post page -->
<main>
    <article>  <!-- The blog post is independent content -->
        <h1>How I Learned Web Development</h1>
        <section>  <!-- Introduction section of the article -->
            <h2>My Background</h2>
            <p>...</p>
        </section>
        <section>  <!-- Another section of the same article -->
            <h2>My Learning Journey</h2>
            <p>...</p>
        </section>
    </article>
    
    <aside>  <!-- Related but not essential -->
        <h3>Related Posts</h3>
        <ul>...</ul>
    </aside>
</main>

<!-- Portfolio page -->
<main>
    <section id="projects">  <!-- Thematic grouping -->
        <h2>My Projects</h2>
        
        <article class="project-card">  <!-- Each project is independent -->
            <h3>Project 1</h3>
            <p>Description...</p>
        </article>
        
        <article class="project-card">
            <h3>Project 2</h3>
            <p>Description...</p>
        </article>
    </section>
</main>
```

**Still use `<div>` for:**
- Pure styling/layout containers
- Wrapper elements that have no semantic meaning
- Grouping elements for CSS/JavaScript purposes

---

### 4. Other Useful Semantic Elements (15 minutes)

#### **`<figure>` and `<figcaption>` - Images with Captions**

```html
<figure>
    <img src="project-screenshot.jpg" alt="Screenshot of my portfolio">
    <figcaption>My portfolio homepage design</figcaption>
</figure>
```

**When to use:** Any image, diagram, code snippet, or illustration that's referenced from the main content.

---

#### **`<time>` - Dates and Times**

```html
<p>Published on <time datetime="2024-01-15">January 15, 2024</time></p>

<!-- With time -->
<time datetime="2024-01-15T14:30:00">2:30 PM, Jan 15, 2024</time>
```

**Why it matters:** Machines can parse the `datetime` attribute while humans read the text inside.

---

#### **`<address>` - Contact Information**

```html
<footer>
    <address>
        Contact me at: <a href="mailto:you@example.com">you@example.com</a><br>
        Location: San Francisco, CA
    </address>
</footer>
```

**Note:** Only for contact information, not physical addresses in general text.

---

#### **`<mark>` - Highlighted Text**

```html
<p>The most important skill is <mark>consistency</mark>.</p>
```

**Renders as:** Yellow highlighted text (like a highlighter marker)

---

## 🛠️ Hands-On Practice (90 minutes)

### **Exercise 1: Analyze a Website Structure (15 minutes)**

**Task:** Pick a favorite website and identify its structure.

1. Visit any professional website (e.g., Medium.com, GitHub.com, your favorite blog)
2. Right-click → "Inspect" or "View Page Source"
3. Find these elements:
   - `<header>`
   - `<nav>`
   - `<main>`
   - `<section>` or `<article>`
   - `<footer>`

**Write down:**
- What's in their header?
- How many sections do they have?
- What's in their footer?

**Why this matters:** Professional developers constantly learn by inspecting other sites.

---

### **Exercise 2: Build Your Resume Structure (60 minutes)**

**Task:** Create a complete HTML resume using semantic elements.

**Create a new file:** `resume.html` in your `web-dev-journey` folder

**Your resume should include these sections:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Name - Resume</title>
</head>
<body>
    
    <!-- Page Header -->
    <header>
        <h1>Your Full Name</h1>
        <p>Web Developer | Your Location</p>
        <nav>
            <!-- Navigation links to sections -->
        </nav>
    </header>
    
    <!-- Main Content -->
    <main>
        
        <!-- About Section -->
        <section id="about">
            <!-- About content -->
        </section>
        
        <!-- Skills Section -->
        <section id="skills">
            <!-- List of skills -->
        </section>
        
        <!-- Experience Section -->
        <section id="experience">
            <!-- Each job as an article -->
        </section>
        
        <!-- Projects Section -->
        <section id="projects">
            <!-- Each project as an article -->
        </section>
        
        <!-- Education Section -->
        <section id="education">
            <!-- Education details -->
        </section>
        
    </main>
    
    <!-- Page Footer -->
    <footer>
        <!-- Contact info, social links, copyright -->
    </footer>
    
</body>
</html>
```

**Step-by-step instructions:**

#### **Step 1: Header Section**
```html
<header>
    <h1>John Doe</h1>
    <p>Aspiring Full Stack Web Developer</p>
    <p>San Francisco, CA | <a href="mailto:john@example.com">john@example.com</a></p>
    
    <nav>
        <ul>
            <li><a href="#about">About</a></li>
            <li><a href="#skills">Skills</a></li>
            <li><a href="#experience">Experience</a></li>
            <li><a href="#projects">Projects</a></li>
            <li><a href="#education">Education</a></li>
            <li><a href="#contact">Contact</a></li>
        </ul>
    </nav>
</header>
```

#### **Step 2: About Section**
```html
<section id="about">
    <h2>About Me</h2>
    <p>I'm a passionate web developer currently learning full stack development. 
       I have a background in [your background] and I'm excited about building 
       modern web applications.</p>
    <p>When I'm not coding, I enjoy [your hobbies].</p>
</section>
```

#### **Step 3: Skills Section**
```html
<section id="skills">
    <h2>Technical Skills</h2>
    
    <div>
        <h3>Currently Learning</h3>
        <ul>
            <li>HTML5</li>
            <li>CSS3</li>
            <li>JavaScript</li>
            <li>React</li>
            <li>Node.js</li>
        </ul>
    </div>
    
    <div>
        <h3>Tools</h3>
        <ul>
            <li>VS Code</li>
            <li>Git & GitHub</li>
            <li>Chrome DevTools</li>
        </ul>
    </div>
</section>
```

#### **Step 4: Experience Section**
```html
<section id="experience">
    <h2>Experience</h2>
    
    <article>
        <h3>Job Title</h3>
        <p><strong>Company Name</strong> | <time datetime="2022-01">Jan 2022</time> - Present</p>
        <ul>
            <li>Key responsibility or achievement 1</li>
            <li>Key responsibility or achievement 2</li>
            <li>Key responsibility or achievement 3</li>
        </ul>
    </article>
    
    <article>
        <h3>Previous Job Title</h3>
        <p><strong>Previous Company</strong> | <time datetime="2020-06">Jun 2020</time> - <time datetime="2021-12">Dec 2021</time></p>
        <ul>
            <li>Key responsibility or achievement 1</li>
            <li>Key responsibility or achievement 2</li>
        </ul>
    </article>
</section>
```

**Note:** If you don't have work experience yet, use:
- Volunteer work
- School projects
- Freelance work
- Personal projects
- Or create a "Relevant Coursework" section instead

#### **Step 5: Projects Section**
```html
<section id="projects">
    <h2>Projects</h2>
    
    <article class="project">
        <h3>Project Name</h3>
        <p><strong>Technologies:</strong> HTML, CSS, JavaScript</p>
        <p>Description of what the project does and what problem it solves. 
           Mention any interesting challenges you overcame.</p>
        <p>
            <a href="https://github.com/yourusername/project" target="_blank">View Code</a> |
            <a href="https://yourproject.com" target="_blank">Live Demo</a>
        </p>
    </article>
    
    <!-- Add more project articles as you build them -->
</section>
```

**For now:** Include your Day 1 "About Me" page and yesterday's hobby page as projects!

#### **Step 6: Education Section**
```html
<section id="education">
    <h2>Education</h2>
    
    <article>
        <h3>Degree Name</h3>
        <p><strong>University Name</strong> | Graduated <time datetime="2020-05">May 2020</time></p>
        <p>Relevant coursework: List courses related to tech/programming</p>
    </article>
    
    <article>
        <h3>Online Courses & Certifications</h3>
        <ul>
            <li>Full Stack Web Development - Self Study (In Progress)</li>
            <li>Any other courses you've taken</li>
        </ul>
    </article>
</section>
```

#### **Step 7: Footer Section**
```html
<footer id="contact">
    <h2>Get In Touch</h2>
    <address>
        <p>Email: <a href="mailto:your.email@example.com">your.email@example.com</a></p>
        <p>Phone: <a href="tel:+15551234567">+1 (555) 123-4567</a></p>
    </address>
    
    <nav>
        <p>Connect with me:</p>
        <ul>
            <li><a href="https://github.com/yourusername" target="_blank">GitHub</a></li>
            <li><a href="https://linkedin.com/in/yourusername" target="_blank">LinkedIn</a></li>
            <li><a href="https://twitter.com/yourusername" target="_blank">Twitter</a></li>
        </ul>
    </nav>
    
    <p><small>&copy; 2024 Your Name. All rights reserved.</small></p>
</footer>
```

**Tips:**
- Replace all placeholder text with your real information
- If you don't have social media accounts for development yet, remove those links (you can add them later)
- Use `<small>` for copyright text—it's semantic!

---

### **Exercise 3: Add Semantic Richness (15 minutes)**

**Enhance your resume with these additions:**

1. **Add a profile image with figure:**
```html
<section id="about">
    <h2>About Me</h2>
    <figure>
        <img src="profile.jpg" alt="Your Name headshot" width="200">
        <figcaption>Your Name - Web Developer</figcaption>
    </figure>
    <p>About text...</p>
</section>
```

2. **Highlight key achievements with `<mark>`:**
```html
<li>Increased efficiency by <mark>40%</mark> through process automation</li>
```

3. **Add a quote/testimonial with `<blockquote>`:**
```html
<aside>
    <h3>Testimonial</h3>
    <blockquote>
        <p>"[Your Name] is a quick learner and brings great enthusiasm to every project."</p>
        <footer>— Jane Smith, <cite>Former Manager</cite></footer>
    </blockquote>
</aside>
```

---

## 🧠 Knowledge Check (Self-Quiz)

**Answer these without looking back:**

1. What's the difference between `<section>` and `<article>`?
2. When should you use `<div>` vs semantic elements?
3. Can you have multiple `<main>` elements on a page?
4. What goes inside a `<nav>` element?
5. What's the purpose of `<figure>` and `<figcaption>`?
6. What semantic element should you use for a blog post?
7. Where would you put copyright information?
8. What's special about the `<time>` element?

**Struggling?** Review the sections above. Understanding WHY you use each element is more important than memorizing.

---

## 📝 Validation & Best Practices (15 minutes)

### **Validate Your HTML**

1. Go to [W3C HTML Validator](https://validator.w3.org/#validate_by_input)
2. Copy your HTML code
3. Paste and click "Check"
4. Fix any errors

**Common errors beginners make:**
- Unclosed tags
- Nested elements incorrectly (e.g., `<p>` inside `<p>`)
- Missing required attributes (like `alt` on images)
- Duplicate IDs

### **HTML Best Practices Checklist**

- [ ] Only one `<h1>` per page
- [ ] Headings in order (don't skip levels)
- [ ] All images have `alt` attributes
- [ ] Links have descriptive text (not "click here")
- [ ] Proper nesting (close tags in reverse order of opening)
- [ ] Consistent indentation (2 or 4 spaces)
- [ ] All IDs are unique
- [ ] Semantic elements used where appropriate

---

## 🚫 Common Mistakes to Avoid

| Mistake | Why It's Wrong | Better Approach |
|---------|----------------|-----------------|
| `<div class="header">` | Not semantic | `<header>` |
| Multiple `<main>` elements | Only one per page | One `<main>` with multiple `<section>` |
| `<section>` without heading | Sections should have headings | Always include `<h2>` - `<h6>` |
| Using `<br>` for spacing | Accessibility issues | CSS margins (you'll learn soon) |
| `<a href="#">Link</a>` | Empty links don't work | Use real URLs or IDs |
| Overusing `<article>` | Not everything is independent | Use `<section>` or `<div>` |

---

## 💡 Pro Tips

### **1. Document Outline**
Your headings create an outline:
```
Your Name (h1)
├── About Me (h2)
├── Skills (h2)
│   ├── Currently Learning (h3)
│   └── Tools (h3)
├── Experience (h2)
└── Contact (h2)
```

**Test:** Can someone understand your page structure just from the headings?

### **2. Keyboard Navigation**
- Click in your browser, then press Tab repeatedly
- Does it navigate through your links logically?
- This is how many users navigate (accessibility!)

### **3. Use Descriptive IDs**
```html
<!-- Good -->
<section id="work-experience">

<!-- Bad -->
<section id="section2">
```

### **4. Comments for Organization**
```html
<!-- ========== HEADER ========== -->
<header>
    ...
</header>

<!-- ========== MAIN CONTENT ========== -->
<main>
    <!-- About Section -->
    <section id="about">
        ...
    </section>
    
    <!-- Skills Section -->
    <section id="skills">
        ...
    </section>
</main>
```

---

## 📝 Today's Homework (~45 minutes)

### Required:

1. **Complete your resume if you haven't finished**
   - All 5-6 sections
   - Real content (or realistic placeholder content)
   - Validated with W3C validator
   - Proper semantic structure

2. **Create a second page: `blog.html`**
   Build a simple blog post page with:
   - Page header with navigation
   - One main `<article>` (the blog post)
   - 3+ `<section>` elements within the article
   - `<aside>` with related links or author bio
   - Footer with contact info
   - Use `<time>` for publication date
   - Include at least one image with `<figure>` and `<figcaption>`

3. **Link your pages together**
   - Update `index.html` to link to `resume.html` and `blog.html`
   - Add a navigation menu to all pages

### Optional Challenge:

**Create a recipe collection page:**
- Use `<article>` for each recipe
- Each recipe should have:
  - Title and image
  - Ingredients list
  - Instructions (ordered list)
  - Preparation time (use `<time>`)
  - Difficulty level

---

## 🎨 Before/After Comparison

**Yesterday's Code (Day 1):**
```html
<div>
    <div>My Page</div>
    <div>
        <a href="#about">About</a>
    </div>
</div>
<div>
    <div>About Me</div>
    <p>Content...</p>
</div>
```

**Today's Code (Day 2):**
```html
<header>
    <h1>My Page</h1>
    <nav>
        <a href="#about">About</a>
    </nav>
</header>
<main>
    <section id="about">
        <h2>About Me</h2>
        <p>Content...</p>
    </section>
</main>
```

**See the difference?** Same visual output, but the second version is:
- More readable
- Better for SEO
- Accessible to screen readers
- Easier to style with CSS (coming soon!)
- More professional

---

## 🔗 Resources for Today

### Must-Read:
- [MDN: HTML5 Semantic Elements](https://developer.mozilla.org/en-US/docs/Glossary/Semantics#semantic_elements)
- [HTML5 Doctor: Element Index](http://html5doctor.com/element-index/)

### Visual Reference:
- [HTML5 Semantic Elements Flowchart](https://html5doctor.com/downloads/h5d-sectioning-flowchart.pdf)

### Practice:
- [freeCodeCamp: Learn HTML Forms by Building a Registration Form](https://www.freecodecamp.org/learn/2022/responsive-web-design/#learn-html-forms-by-building-a-registration-form)

### Validation:
- [W3C HTML Validator](https://validator.w3.org/)

---

## ✅ End of Day Checklist

- [ ] Understand the difference between semantic and non-semantic HTML
- [ ] Can explain when to use `<section>`, `<article>`, and `<div>`
- [ ] Created a complete resume page with semantic structure
- [ ] Validated your HTML (no errors)
- [ ] All pages linked together
- [ ] Code is properly indented and commented
- [ ] Used at least 7 different semantic elements
- [ ] Pushed to GitHub (if you set it up)

---

## 🎯 Tomorrow's Preview: Day 3 - CSS Fundamentals

Tomorrow you'll make your resume actually look good!

**You'll learn:**
- CSS syntax and selectors
- The Box Model (margin, padding, border)
- Colors, fonts, and basic styling
- How to connect CSS to HTML

**Get excited!** Your black-and-white resume is about to get a complete makeover.

---

## 💬 Reflection Exercise (5 minutes)

1. **What's the biggest "aha moment" you had today?**
   _____________________________________

2. **Which semantic element confused you the most?**
   _____________________________________

3. **How does your resume look compared to what you imagined?**
   _____________________________________

4. **What are you most excited to style with CSS tomorrow?**
   _____________________________________

---

## 🔥 Motivational Note

You just built a complete webpage structure using professional, semantic HTML. This is the same foundation that million-dollar websites are built on.

Right now, it might not look impressive (no colors, basic fonts), but you've built something solid. **You're building a house starting with a strong foundation, not with the paint colors.**

Tomorrow, you add the design. And when you see your resume transform with CSS, you'll understand why we spent two full days on HTML structure first.

**The foundation is set. Tomorrow, we make it beautiful. See you on Day 3! 🎨**

---

**Stuck on something?** 

**Common issues:**
1. **Links not working?** Check that your `href` matches the `id` (including the `#`)
2. **Sections not showing?** Make sure all tags are closed properly
3. **Validation errors?** Read the error message carefully—it usually tells you exactly what's wrong
4. **Indentation messy?** In VS Code: Select All (Ctrl/Cmd+A) → Right-click → "Format Document"

Tomorrow you'll see why good HTML structure makes CSS so much easier! 💪
