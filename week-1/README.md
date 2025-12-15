# Week 1: HTML & CSS Fundamentals - Daily Structured Plan

## **Day 1: HTML Foundations**
*Master the building blocks of web structure*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Read: What is HTML and how browsers interpret it
- [ ] Study: Document structure (`<!DOCTYPE>`, `<html>`, `<head>`, `<body>`)
- [ ] Learn: Common HTML tags and their purposes
  - Headings (`h1-h6`)
  - Paragraphs and text formatting (`p`, `strong`, `em`, `br`)
  - Lists (`ul`, `ol`, `li`)
  - Links (`a`) and attributes

**Resources:**
- MDN: [HTML Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics)
- Watch: [HTML Crash Course](https://www.youtube.com/watch?v=UB1O30fR-EE) (first 30 min)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Build "About Me" Page**
```html
<!-- Create this structure -->
1. Header with your name
2. Navigation menu (even if links don't work yet)
3. Three sections:
   - About Me (paragraph about yourself)
   - My Interests (unordered list)
   - My Goals (ordered list)
4. Footer with copyright
```

**Exercises:**
- [ ] Create 5 different HTML files exploring different tags
- [ ] Build a recipe page with ingredients list
- [ ] Create a simple news article structure
- [ ] Practice nesting elements properly

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Review what you built
- [ ] Write down 3 things you learned
- [ ] Identify 2 questions to research tomorrow
- [ ] Push code to GitHub (create repo if haven't already)

**Checklist for Day 1:**
- [ ] Can create a basic HTML document from memory
- [ ] Understand parent-child relationships in HTML
- [ ] Used at least 15 different HTML tags

---

## **Day 2: Semantic HTML & Forms**
*Structure content meaningfully*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: Semantic HTML5 elements
  - `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`
- [ ] Learn: Forms and inputs
  - Form structure and attributes
  - Input types (text, email, password, number, date, etc.)
  - Labels, placeholders, and accessibility
- [ ] Understand: Tables and when to use them

**Resources:**
- MDN: [HTML5 Semantic Elements](https://developer.mozilla.org/en-US/docs/Glossary/Semantics)
- Article: [Guide to HTML Forms](https://www.w3schools.com/html/html_forms.asp)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Multi-page Website Structure**
```html
<!-- Create 3 connected pages -->
1. index.html - Homepage with semantic structure
   - Header with logo area
   - Navigation linking to all pages
   - Main content with 2-3 article sections
   - Aside with related links
   - Footer

2. contact.html - Contact form page
   - Name, email, phone inputs
   - Message textarea
   - Dropdown for inquiry type
   - Radio buttons for preferred contact method
   - Checkbox for newsletter signup
   - Submit button

3. blog.html - Blog listing page
   - Multiple article elements
   - Each with header, content, footer
   - Time stamps using <time> element
```

**Exercises:**
- [ ] Create a registration form with 10 different input types
- [ ] Build a table displaying your weekly schedule
- [ ] Convert yesterday's "About Me" page to semantic HTML
- [ ] Add meta tags to all pages (description, keywords, viewport)

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Validate HTML using [W3C Validator](https://validator.w3.org/)
- [ ] Test all form inputs
- [ ] Document which semantic elements you used and why
- [ ] Commit with meaningful message: "Add semantic HTML structure and forms"

**Checklist for Day 2:**
- [ ] Understand when to use each semantic element
- [ ] Created a functional form with various input types
- [ ] All HTML validates without errors

---

## **Day 3: CSS Fundamentals**
*Style and visual design basics*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: How CSS works (cascade, specificity, inheritance)
- [ ] Learn: Three ways to add CSS (inline, internal, external)
- [ ] Master: Selectors
  - Element, class, ID selectors
  - Descendant and child selectors
  - Pseudo-classes (:hover, :focus, :nth-child)
- [ ] Understand: Colors (hex, rgb, hsl) and units (px, em, rem, %, vh/vw)

**Resources:**
- MDN: [CSS First Steps](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps)
- Interactive: [CSS Diner](https://flukeout.github.io/) (selector game)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Style Your Multi-page Website**
```css
/* Create styles.css with: */
1. Typography system
   - Font family for headings and body
   - Font sizes using rem units
   - Line height and letter spacing

2. Color scheme
   - Primary, secondary, accent colors
   - Text colors for different states
   - Background colors

3. Basic layouts
   - Container with max-width and center alignment
   - Header and footer styling
   - Navigation menu horizontal layout

4. Interactive elements
   - Hover effects on links
   - Focus styles on form inputs
   - Active states on buttons
```

**Exercises:**
- [ ] Create 5 different button styles
- [ ] Style the form from Day 2 to look professional
- [ ] Build a color palette tester page
- [ ] Create a CSS reset/normalize file

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Test hover states and interactions
- [ ] Check color contrast for accessibility
- [ ] Organize CSS file with comments
- [ ] Commit: "Add CSS styling system"

**Checklist for Day 3:**
- [ ] Understand CSS specificity
- [ ] Can center elements horizontally
- [ ] Created consistent color scheme
- [ ] Styled at least 20 different elements

---

## **Day 4: Box Model & Layout Basics**
*Understand spacing and positioning*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Master: Box Model (content, padding, border, margin)
- [ ] Learn: box-sizing: border-box
- [ ] Study: Display properties (block, inline, inline-block, none)
- [ ] Understand: Position (static, relative, absolute, fixed, sticky)
- [ ] Learn: Overflow and z-index

**Resources:**
- MDN: [The Box Model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)
- Interactive: [Box Model Visualization](https://codepen.io/carolineartz/full/ogVXZj)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Component Library**
```css
/* Build reusable components */
1. Card component
   - Image top
   - Content padding
   - Shadow and hover effect

2. Modal/Popup
   - Fixed positioning
   - Overlay background
   - Centered content box

3. Navigation bar
   - Fixed to top on scroll
   - Logo left, menu right
   - Dropdown submenu

4. Hero section
   - Full viewport height
   - Background image with overlay
   - Centered text content
```

**Exercises:**
- [ ] Create 3 different card layouts
- [ ] Build a sticky sidebar
- [ ] Make a tooltip using position: absolute
- [ ] Create spacing utility classes (.m-1, .p-2, etc.)

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Test all positioning scenarios
- [ ] Debug any overflow issues
- [ ] Create a spacing reference guide
- [ ] Commit: "Add box model layouts and components"

**Checklist for Day 4:**
- [ ] Can explain box-sizing: border-box
- [ ] Understand all position values
- [ ] Created at least 5 reusable components
- [ ] No unwanted scrollbars or overlaps

---

## **Day 5: Flexbox Mastery**
*Modern one-dimensional layouts*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: Flexbox container properties
  - display: flex
  - flex-direction, flex-wrap, flex-flow
  - justify-content, align-items, align-content
- [ ] Learn: Flexbox item properties
  - flex-grow, flex-shrink, flex-basis
  - align-self, order
- [ ] Understand: Common flexbox patterns

**Resources:**
- CSS-Tricks: [Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- Game: [Flexbox Froggy](https://flexboxfroggy.com/)
- Game: [Flexbox Defense](http://www.flexboxdefense.com/)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Flexbox Layout System**
```css
/* Build these layouts with flexbox */
1. Navigation variations
   - Logo left, menu center, button right
   - Evenly spaced menu items
   - Mobile-ready vertical menu

2. Card grid
   - Equal height cards
   - Flexible number per row
   - Last row alignment handled

3. Media object
   - Image left/right with content
   - Vertical centering
   - Flexible spacing

4. Footer layout
   - Multi-column footer
   - Social icons row
   - Copyright bar
```

**Exercises:**
- [ ] Create a pricing table with flexbox
- [ ] Build a photo gallery with flex-wrap
- [ ] Make a dashboard sidebar layout
- [ ] Create holy grail layout (header, footer, sidebar, main)

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Refactor previous layouts to use flexbox
- [ ] Test all layouts with different content amounts
- [ ] Document flexbox patterns you'll reuse
- [ ] Commit: "Implement flexbox layouts"

**Checklist for Day 5:**
- [ ] Can center anything with flexbox
- [ ] Understand main axis vs cross axis
- [ ] Built at least 5 different flexbox layouts
- [ ] Know when to use flexbox vs other methods

---

## **Day 6: CSS Grid & Responsive Design**
*Two-dimensional layouts and mobile-first approach*

### 🌅 Morning Session (9:00 - 10:30)
**Theory & Reading (90 min)**
- [ ] Study: CSS Grid basics
  - Grid container and items
  - grid-template-columns/rows
  - grid-gap
  - Grid areas and naming
- [ ] Learn: Responsive design principles
  - Mobile-first approach
  - Breakpoints and media queries
  - Responsive units (rem, em, %, vw/vh)
- [ ] Understand: Flexbox vs Grid use cases

**Resources:**
- CSS-Tricks: [Complete Guide to Grid](https://css-tricks.com/snippets/css/complete-guide-grid/)
- Game: [Grid Garden](https://cssgridgarden.com/)
- MDN: [Responsive Design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)

### ☀️ Afternoon Session (2:00 - 4:30)
**Hands-on Practice (2.5 hours)**

**Project: Responsive Portfolio Grid**
```css
/* Build responsive layouts */
1. Homepage grid
   - Header spanning full width
   - Sidebar on desktop, top on mobile
   - Main content area
   - Grid of portfolio items (responsive columns)

2. Media queries
   - Mobile: < 768px (single column)
   - Tablet: 768px - 1024px (2 columns)
   - Desktop: > 1024px (3-4 columns)

3. Responsive components
   - Navigation (hamburger on mobile)
   - Images that scale
   - Flexible typography (clamp())
   - Touch-friendly buttons

4. Grid experiments
   - Magazine layout
   - Masonry-style gallery
   - Dashboard with widgets
```

**Exercises:**
- [ ] Create responsive grid without media queries (minmax, auto-fit)
- [ ] Build a responsive pricing table
- [ ] Make a grid-based image gallery
- [ ] Create a responsive dashboard layout

### 🌙 Evening Review (8:00 - 8:30)
- [ ] Test on different screen sizes (use DevTools)
- [ ] Validate mobile usability
- [ ] Check loading performance
- [ ] Commit: "Add CSS Grid and responsive design"

**Checklist for Day 6:**
- [ ] Understand grid-template-areas
- [ ] Can create responsive layouts without frameworks
- [ ] Know when to use Grid vs Flexbox
- [ ] All layouts work on mobile

---

## **Day 7: Integration & Landing Page Project**
*Combine everything into a polished project*

### 🌅 Morning Session (9:00 - 10:30)
**Planning & Setup (90 min)**
- [ ] Choose landing page topic (product, service, or event)
- [ ] Create wireframes for mobile and desktop
- [ ] Plan color scheme and typography
- [ ] Set up file structure:
  ```
  landing-page/
  ├── index.html
  ├── css/
  │   ├── reset.css
  │   ├── styles.css
  │   └── responsive.css
  ├── images/
  └── README.md
  ```
- [ ] Find/create assets (images, icons, fonts)

### ☀️ Extended Build Session (10:30 - 4:30)
**Build Complete Landing Page**

**Required Sections:**
```html
1. Hero Section
   - Full viewport height
   - Background image/gradient
   - Headline, subtext, CTA button
   - Smooth scroll arrow

2. Navigation
   - Fixed/sticky positioning
   - Logo and menu items
   - Mobile hamburger menu
   - Smooth scroll to sections

3. Features/Services (Grid)
   - 3-4 feature cards
   - Icons and descriptions
   - Hover animations
   - Responsive grid layout

4. About Section (Flexbox)
   - Image and text side-by-side
   - Reverses on alternate rows
   - Mobile stacks vertically

5. Testimonials
   - Carousel or grid
   - Quote formatting
   - Author info with avatar

6. Pricing Table
   - 3 pricing tiers
   - Highlighted recommended plan
   - Feature comparison
   - CTA buttons

7. Contact Form
   - Styled inputs
   - Validation states
   - Submit button with hover

8. Footer
   - Multi-column layout
   - Social media links
   - Newsletter signup
   - Copyright info
```

**CSS Features to Include:**
- [ ] CSS animations (keyframes)
- [ ] Transitions on hover/focus
- [ ] Custom CSS properties (variables)
- [ ] Gradient backgrounds
- [ ] Box shadows and text shadows
- [ ] Transform effects
- [ ] Smooth scrolling
- [ ] Loading animation

### 🌙 Evening: Polish & Deploy (4:30 - 6:00)
- [ ] Cross-browser testing
- [ ] Performance optimization
  - Optimize images
  - Minify CSS
  - Check loading speed
- [ ] Accessibility check
  - Alt texts
  - Focus states
  - Color contrast
- [ ] Deploy to GitHub Pages or Netlify
- [ ] Write README with:
  - Project description
  - Technologies used
  - Lessons learned
  - Screenshot

**Final Checklist for Week 1:**
- [ ] Landing page is fully responsive
- [ ] All links and forms work
- [ ] Code is clean and commented
- [ ] Page loads in under 3 seconds
- [ ] Passes HTML/CSS validation
- [ ] Deployed and shareable
- [ ] Added to portfolio

---

## 📊 Week 1 Success Metrics

By the end of Week 1, you should be able to:

### Knowledge Check ✅
- [ ] Write semantic HTML from memory
- [ ] Explain the CSS cascade and specificity
- [ ] Choose between Flexbox and Grid for any layout
- [ ] Debug layout issues using DevTools
- [ ] Make any design responsive

### Skills Acquired 💪
- [ ] Built 5+ complete web pages
- [ ] Created 20+ reusable CSS components
- [ ] Implemented 3+ different layout techniques
- [ ] Wrote 500+ lines of CSS
- [ ] Used 30+ different HTML elements

### Portfolio Pieces 🎨
1. Multi-page semantic website
2. Component library
3. Responsive landing page (deployed)

### Next Week Preview 🚀
Week 2 will build on this foundation with JavaScript, adding interactivity to your pages. You'll manipulate the DOM, handle events, and create dynamic user experiences.

---

## 💡 Daily Tips for Success

1. **Start each day fresh** - Review yesterday's code with fresh eyes
2. **Type everything** - Don't copy-paste, build muscle memory
3. **Break when stuck** - 15-minute walks solve more problems than 2 hours of frustration
4. **Celebrate small wins** - Every working feature is an achievement
5. **Share your progress** - Post screenshots on social media for accountability

## 🛠 Troubleshooting Resources

- **When stuck:** First try to solve it yourself for 20 minutes
- **CSS not applying?** Check specificity and typos
- **Layout broken?** Use browser DevTools to inspect box model
- **Still stuck?** Ask on Stack Overflow with a minimal example
- **Need inspiration?** Browse CodePen and Dribbble

## 📝 Week 1 Notes Template

Keep a learning journal with:
```markdown
## Day X: [Topic]
### What I Learned:
- Key concept 1
- Key concept 2

### Challenges:
- Problem I faced
- How I solved it

### To Research:
- Questions for tomorrow

### Code Snippet of the Day:
```[paste your best code]```
```

Remember: **Progress > Perfection**. Focus on understanding concepts and building working projects. You can always refine and improve later! 🎯
