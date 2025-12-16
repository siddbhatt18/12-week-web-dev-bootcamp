Below is a 12‑week, 80/20-focused study plan for Full Stack Web Development, centered on the core concepts that get you building real projects fast. It assumes ~10–15 hours/week. Adjust pace if needed.

**Tech stack (opinionated, “80-20” friendly):**
- **Frontend:** HTML5, modern CSS (Flexbox/Grid), basic responsive design, vanilla JavaScript, then React.
- **Backend:** Node.js + Express.
- **Database:** MongoDB (with Mongoose).
- **Other essentials:** Git/GitHub, basic deployment (e.g., Render, Vercel, Netlify).

You’ll build **5 projects** (P1–P5) of increasing difficulty while you learn.

---

## Overview of the 12-Week Roadmap

- **Weeks 1–3:** Web fundamentals (HTML, CSS, core JavaScript)
- **Weeks 4–5:** DOM, asynchronous JS, APIs, Git, project structure
- **Weeks 6–7:** Node.js, Express, REST APIs, MongoDB basics
- **Weeks 8–9:** React fundamentals and integrating with a backend
- **Weeks 10–12:** Full-stack app, auth, deployment, polish

Projects:
1. **P1 – Personal Portfolio (static, HTML/CSS)** – Week 2–3  
2. **P2 – Vanilla JS TODO App (frontend only)** – Week 4  
3. **P3 – API-Powered Dashboard (frontend + public API)** – Week 5  
4. **P4 – RESTful Notes API (backend + DB)** – Week 7  
5. **P5 – Full Stack “Mini SaaS” App (React + Node + DB + auth + deploy)** – Weeks 9–12  

---

## Week 1 – Web Basics & Mental Models

**Goal:** Understand how the web works and build simple static pages.

### Core topics (80/20)
- What happens when you visit a website (client, server, request/response).
- **HTML essentials:**
  - Common tags: `html`, `head`, `body`, `h1–h6`, `p`, `a`, `img`, `div`, `span`
  - Lists: `ul`, `ol`, `li`
  - Forms (basic): `form`, `input`, `label`, `button`
  - Semantic tags: `header`, `nav`, `main`, `section`, `article`, `footer`
- **CSS essentials:**
  - Selectors, classes, IDs
  - The box model (margin, border, padding)
  - Basic layout: `display: block/inline/inline-block`, `width`, `height`
  - Colors, fonts, basic styling
- Developer tools:
  - Inspect element, modify CSS in browser
  - View source, console

### Practice
- Recreate a simple article page: title, subtitle, paragraphs, image, footer.
- Style it with CSS: change fonts, add spacing, center headings.

**Deliverable:** A single-page “About Me” site using semantic HTML + basic CSS.

---

## Week 2 – Layout, Responsive Design & Basic Git

**Goal:** Build reasonably nice layouts and version your code with Git.

### Core topics
- **CSS Layout:**
  - Flexbox: containers (`display:flex`), direction, justify-content, align-items
  - Simple responsive nav bar with Flexbox
- **Responsive basics:**
  - Fluid widths, max-width
  - Simple media queries for mobile vs desktop
- **Basic Git & GitHub:**
  - `git init`, `git add`, `git commit`
  - Pushing to GitHub
  - `.gitignore` basics

### Practice
- Rebuild your “About Me” as a 2-column layout on desktop and 1-column on mobile.
- Create a GitHub account and push your project.

### Start Project P1
**P1 – Personal Portfolio (Beginner)**  
- **Description:** A multi-section static portfolio site with:
  - Home / About section
  - Projects summary section
  - Contact form (no backend yet)
- **Key concepts reinforced:**
  - Semantic HTML
  - CSS layout (Flexbox)
  - Responsive design
  - Git basics & project organization (separate `css/` folder, etc.)

Work on P1 through Week 3.

---

## Week 3 – Deeper CSS & Intro to JavaScript

**Goal:** Make your pages look better and start coding with JS.

### Core topics
- **CSS improvements:**
  - CSS variables, hover effects, transitions
  - Basic CSS Grid (for galleries, portfolios)
- **JavaScript basics:**
  - Variables (`let`, `const`), data types
  - Operators, conditionals (`if`, `else`)
  - Functions and parameters
  - Arrays and objects (basic)
  - Console (`console.log`) for debugging

### Practice
- Add hover animations to links and buttons in P1.
- Write small JS snippets in a separate `.js` file:
  - A function that takes a list of numbers and returns the average.
  - An object representing a user with properties (name, age) and a method.

**Deliverable:**  
- A polished P1 portfolio deployed on GitHub Pages (or Netlify).

---

## Week 4 – DOM Manipulation & Interactivity (P2)

**Goal:** Make your pages interactive with DOM manipulation and events.

### Core topics
- **DOM & Events:**
  - Selecting elements (`querySelector`, `querySelectorAll`)
  - Modifying text and attributes
  - Creating/removing elements dynamically
  - Event listeners (`click`, `submit`, `input`)
- **Local Storage:**
  - `localStorage.setItem`, `getItem`, `JSON.stringify`, `JSON.parse`
- **Basic error handling:**
  - Try/catch (intro), meaningful console messages

### Project P2
**P2 – Vanilla JS TODO App (Beginner–Intermediate)**  
- **Description:** A simple app where users can:
  - Add, edit (optional), and delete tasks
  - Mark tasks as completed
  - Persist tasks in `localStorage` so they survive page reloads
- **Key concepts reinforced:**
  - DOM selection and manipulation
  - Event handling
  - Basic state management in JS (an array of todo objects)
  - Local storage for persistence

**Milestones:**
- Day 1–2: Basic UI in HTML/CSS; manually add dummy tasks.
- Day 3–4: Connect form to JS; add tasks dynamically.
- Day 5–6: Complete/delete tasks; save/load from localStorage.

---

## Week 5 – Async JS, Fetch, APIs & Project P3

**Goal:** Learn to work with APIs and async code.

### Core topics
- **Asynchronous JavaScript:**
  - Callbacks vs Promises (conceptually)
  - `fetch` API
  - `async/await`
  - Basic error handling for network calls (`try/catch`)
- **HTTP basics:**
  - Methods: GET, POST (and concept of others)
  - Status codes: 200, 400, 404, 500 (common ones)
  - JSON format

### Practice
- Use `fetch` to:
  - Call a public API (e.g., JSONPlaceholder, OpenWeatherMap, or a joke API).
  - Display data on the page (e.g., show a random joke or weather in a city).

### Project P3
**P3 – API-Powered Dashboard (Intermediate)**  
- **Description:** A single-page dashboard that shows data from one or two public APIs, for example:
  - Weather in a searched city
  - Random quote or news headlines
- **Features:**
  - Input field for city or query
  - Button to fetch data
  - Display formatted results (not just raw JSON)
- **Key concepts reinforced:**
  - Fetching and parsing JSON (`response.json()`)
  - Async/await, error handling
  - Working with third-party API docs
  - DOM updates based on async data

**Milestones:**
- Day 1–2: Pick APIs, design layout.
- Day 3–4: Implement `fetch` and display data.
- Day 5–6: Handle loading state and errors (e.g., “No results found”, “Network error”).

---

## Week 6 – Node.js & Express Fundamentals

**Goal:** Move to the backend and understand how servers work.

### Core topics
- **Node.js basics:**
  - What Node is; using `npm`
  - `package.json`, installing dependencies
- **Express basics:**
  - Creating a simple server
  - Route handlers: `app.get`, `app.post`
  - Reading query params and request body
- **REST API concepts:**
  - Resources and endpoints
  - CRUD (Create, Read, Update, Delete)
- **Postman or similar tool** to test endpoints.

### Practice
- Build a simple Express app that:
  - Returns `"Hello World"` at `/`.
  - Returns a list of hard-coded items at `/items`.
- Add routes to:
  - Create a new item (in an in-memory array).
  - Delete an item by ID (still in-memory).

**Deliverable:**  
- Simple REST API with Express, no database yet.

---

## Week 7 – Database (MongoDB) & Project P4

**Goal:** Persist data with a real database and create a RESTful backend.

### Core topics
- **MongoDB & Mongoose:**
  - Documents, collections
  - Connecting Node to MongoDB (local or Atlas)
  - Defining a schema and model
  - Basic operations: `create`, `find`, `findById`, `findByIdAndUpdate`, `findByIdAndDelete`
- **Environment variables:**
  - `.env` for DB connection strings
- **Basic validation & error handling on the backend.**

### Project P4
**P4 – RESTful Notes API (Intermediate Backend)**  
- **Description:** A backend API for a “Notes” resource.
  - Routes:
    - `POST /notes` – create a note
    - `GET /notes` – list notes
    - `GET /notes/:id` – get a single note
    - `PUT or PATCH /notes/:id` – update a note
    - `DELETE /notes/:id` – delete a note
- **Data model:**  
  - `title` (string), `content` (string), `createdAt`, `updatedAt`
- **Key concepts reinforced:**
  - CRUD operations with MongoDB
  - RESTful routing conventions
  - Mongoose models and schemas
  - Handling errors (invalid ID, missing fields)
  - Separation of concerns (routes vs models vs app.js)

**Milestones:**
- Day 1–2: Setup MongoDB, connect via Mongoose, define Note model.
- Day 3–4: Implement all CRUD routes.
- Day 5–6: Add basic validation and error responses (e.g., missing `title`).

Optional stretch:
- Write minimal frontend or use Postman/Insomnia for testing only.

---

## Week 8 – React Fundamentals

**Goal:** Learn modern frontend development with React for building interactive UIs.

### Core topics
- **React basics (with Vite or Create React App):**
  - Components (function components)
  - JSX rules
  - Props (passing data down)
  - State with `useState`
  - Handling events (`onClick`, `onChange`)
  - Controlled forms (values from state)
- **Thinking in components & state:**
  - Breaking UI into smaller components
  - One-way data flow

### Practice
- Build a small React app:
  - A counter with increment/decrement/reset buttons.
  - A simple form that captures name and email and displays them below.

**Deliverable:**  
- A small but complete React app with multiple components and props.

---

## Week 9 – React + REST API & Start P5

**Goal:** Connect React to a backend API (your own or a public one).

### Core topics
- **React + Fetch / Axios:**
  - Using `useEffect` to fetch data on load
  - Loading and error states for API calls
- **Basic client-side routing (optional but useful):**
  - `react-router-dom` for simple multi-page SPA

### Practice
- Create a React “Notes” frontend that:
  - Fetches notes from P4’s API.
  - Displays them in a list.
  - Allows creating a new note via a form and POST request.

### Project P5 (Start)
**P5 – Full Stack “Mini SaaS” App (Advanced)**  
You’ll work on this from Week 9–12.

- **Description (choose one):**
  - Task manager / Kanban board
  - Simple habit tracker
  - Basic “expense tracker”
- **Minimum features:**
  - User registration & login (auth)
  - CRUD on a main resource (tasks/habits/expenses) tied to the logged-in user
  - Basic analytics or filters (e.g., filter by date/status)
  - Deployed frontend + backend

- **Key concepts (overall for Weeks 9–12):**
  - Full-stack flow: React → Express → MongoDB
  - Authentication (JWT or sessions)
  - Protected routes on backend
  - Basic protected pages on frontend
  - Deployment

**Week 9 focus for P5:**
- Decide the domain (tasks/habits/expenses).
- Sketch basic UI and data models.
- Initialize React app & Express app in separate folders.
- Setup basic routing in Express and React.

---

## Week 10 – Authentication & Authorization (P5)

**Goal:** Add user accounts and protect data.

### Core topics
- **Auth basics:**
  - Hashing passwords with `bcrypt`
  - JWT (JSON Web Tokens): sign, verify, expiration
- **Backend auth:**
  - Auth routes: `/auth/register`, `/auth/login`
  - Middleware to protect routes:
    - Extract token from headers
    - Verify token
    - Attach user info to `req.user`
- **Frontend auth flow:**
  - Login form, registration form
  - Storing the auth token in memory or `localStorage` (simple approach)
  - Passing token in `Authorization` headers in API calls

### P5 milestones (Week 10):
- Implement user model (email, passwordHash, etc.).
- Auth routes on backend with JWT.
- Protect main resource routes so only logged-in users can access their items.
- React:
  - Registration and login pages
  - After login, store token and redirect to main dashboard

---

## Week 11 – Core App Features & UI Polish (P5)

**Goal:** Build out the main feature set of your mini SaaS app.

### Core topics
- **Full CRUD from frontend:**
  - Create/read/update/delete resource items for the logged-in user
  - Forms in React for create/update
- **Better UI flow:**
  - Handling loading and error states
  - Showing success/failure messages
- **Filtering & basic “analytics”:**
  - e.g., for tasks:
    - Show completed vs pending counts
    - Filter by status or due date

### P5 milestones (Week 11):
- Main dashboard page:
  - List items (tasks/habits/expenses)
  - Add new items
  - Edit and delete existing items
- Basic stats section: e.g., number of tasks completed this week.
- Improve layout (responsive, simple but clean).

---

## Week 12 – Deployment, Cleanup & Reflection (P5)

**Goal:** Put your app online and solidify your understanding.

### Core topics
- **Deployment:**
  - Deploy backend (e.g., Render, Railway, or similar)
  - Deploy frontend (Vercel, Netlify)
  - Configure environment variables for production (DB URI, JWT secret)
  - Update frontend API base URL to production backend
- **Production considerations (lightweight):**
  - Basic logging
  - Handling 404 and 500 errors gracefully
- **Refactoring:**
  - Clean up folder structure
  - Extract repeated code into utilities/hooks (e.g., `useAuth`, `api.js`)

### P5 milestones (Week 12):
- Backend deployed and reachable via HTTPS.
- Frontend deployed and connected to backend.
- Manual end-to-end test: sign up, log in, create resource, edit, delete, log out.
- Write a short README:
  - Overview
  - Tech stack
  - How to run locally
  - Live demo link, screenshots

---

## Summary of the 5 Projects

### P1 – Personal Portfolio (Beginner)
- **Description:** A static, responsive site showcasing your bio, skills, and (eventually) projects.
- **Key concepts:**
  - Semantic HTML
  - CSS layout (Flexbox/Grid), responsive design
  - Basic styling and hover effects
  - Git & GitHub, simple deployment (GitHub Pages/Netlify)

---

### P2 – Vanilla JS TODO App (Beginner–Intermediate)
- **Description:** Browser-based task manager with create/complete/delete tasks and persistence via `localStorage`.
- **Key concepts:**
  - DOM manipulation and events
  - Arrays/objects as in-memory “database”
  - Local storage for persistence
  - Handling forms and user input

---

### P3 – API-Powered Dashboard (Intermediate Frontend)
- **Description:** A single-page app pulling data from public APIs (weather, quotes, news, etc.) with search/filtering.
- **Key concepts:**
  - Async JS with `fetch` and `async/await`
  - Working with JSON and API documentation
  - Error/empty-state handling
  - Organizing code into functions/modules

---

### P4 – RESTful Notes API (Intermediate Backend)
- **Description:** A Node.js + Express + MongoDB API that manages notes with full CRUD.
- **Key concepts:**
  - Node.js/Express server setup
  - RESTful routing conventions
  - MongoDB with Mongoose (models, schema, queries)
  - Basic validation and error handling
  - Testing endpoints with Postman/Insomnia

---

### P5 – Full Stack “Mini SaaS” App (Advanced Full Stack)
- **Description:** A fully integrated app (React + Node + MongoDB) with user authentication and a main resource (tasks/habits/expenses) plus basic analytics and production deployment.
- **Key concepts:**
  - Full-stack integration (frontend ↔ backend ↔ DB)
  - Authentication & authorization (JWT, protected routes)
  - React state management, forms, and data fetching
  - Deployment & environment configuration
  - Application structure and code organization

---

## How to Challenge Yourself & Think Independently

- Before searching for “the answer,” **describe the problem in your own words** and sketch a solution.
- For each new concept:
  - Build a **tiny experiment** (a separate file or app) that uses just that idea.
- With each project, ask:
  - “What’s one extra feature I can add without a tutorial?” (e.g., filters, sorting, simple stats).
- Keep a **debugging log**:
  - When stuck, write: “What I expected,” “What happened,” “What I tried.”  
  This habit builds problem-solving skills.

If you’d like, I can next:
- Help you choose the specific APIs for P3 and the domain (tasks/habits/expenses) for P5, and  
- Provide a minimal file/folder structure template for each project.
