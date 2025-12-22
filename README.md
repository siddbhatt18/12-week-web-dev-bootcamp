Below is a focused 12‑week plan that follows the 80/20 rule: we’ll prioritize the core skills that let you actually build and deploy real full‑stack web apps. The goal is to get you from zero to shipping useful projects.

Assumptions:
- ~10–15 hours/week.
- Tech stack: **HTML + CSS + modern JavaScript + React + Node.js (Express) + MongoDB**.
- You should Google, read docs, and debug on your own first before looking at solutions.

---

## High-Level Roadmap (80/20 Focus)

- **Frontend essentials (Weeks 1–4)**  
  HTML, CSS fundamentals, responsive layouts, core JavaScript (arrays, objects, functions, async), DOM, basic React.

- **Backend & APIs (Weeks 5–8)**  
  Node.js, Express, REST APIs, MongoDB & Mongoose, authentication basics.

- **Full-stack integration & deployment (Weeks 9–12)**  
  Connecting React to your API, state management patterns, auth on frontend, deployment, performance basics.

---

## 12-Week Study Plan (Week-by-Week)

### Week 1 – Web Foundations: HTML, CSS, Mental Models

**Goals:**
- Understand how the web works.
- Build static pages using semantic HTML and basic CSS.

**Core topics (20% that matters):**
- How the web works: client, server, HTTP, request/response, what a URL is.
- **HTML**:
  - `<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`
  - Headings, paragraphs, links, images, lists
  - Forms (basic): `<form>`, `<input>`, `<label>`, `<button>`
  - Semantic tags: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- **CSS**:
  - Selectors: element, class, id
  - Box model: margin, border, padding
  - Display: `block`, `inline`, `inline-block`
  - Basic typography, colors, backgrounds
- Dev tools:
  - VS Code basics
  - Browser DevTools: inspect, elements, console

**Practical tasks:**
- Set up a project folder and simple HTML file.
- Recreate a simple landing page from a design you find online:
  - Header, nav, hero section, content sections, footer.
- Use DevTools to tweak styles live.

---

### Week 2 – CSS Layout & Responsive Design

**Goals:**
- Create responsive, modern layouts.
- Get comfortable reading and tweaking CSS.

**Core topics:**
- CSS Layout:
  - Flexbox: `display:flex`, `justify-content`, `align-items`, `flex-direction`, `flex-wrap`.
  - Simple responsive navbars and cards with Flexbox.
- Basic responsiveness:
  - Relative units (`%`, `rem`, `vh`, `vw`)
  - Media queries: `@media (max-width: 768px) { ... }`
- CSS organization:
  - Class naming, avoiding overly complex selectors.
- Light intro to a utility framework (optional): Tailwind or Bootstrap (but only basic usage).

**Practical tasks:**
- Convert last week’s landing page into a **fully responsive** layout (mobile first).
- Build a simple 3‑card feature section that reflows to 1 column on small screens.
- Practice: replicate 1–2 simple responsive components from any website.

---

### Week 3 – JavaScript Fundamentals (The Core 20%)

**Goals:**
- Be able to read, write, and reason about basic JavaScript.
- Understand variables, data types, control flow, functions, and arrays/objects.

**Core topics:**
- Language basics:
  - `let`, `const`, primitive types
  - Conditionals: `if/else`, `switch`
  - Loops: `for`, `while`, `for...of`
- Functions:
  - Function declarations and expressions
  - Arrow functions
- Data structures:
  - Arrays: `push`, `pop`, `map`, `filter`, `find`, `forEach`
  - Objects: key-value pairs; accessing and updating properties
- Working with the DOM:
  - `document.querySelector`, `addEventListener`
  - Reading/writing text and HTML: `textContent`, `innerHTML`, `value`
- Basic debugging:
  - `console.log`, reading error messages

**Practical tasks:**
- Build a simple “To‑Do List” in plain JS:
  - Add new tasks, mark completed, delete tasks.
  - Use DOM manipulation and event listeners.
- Write short functions in a separate JS file to:
  - Filter an array of numbers (e.g., all even numbers).
  - Find a user by id in an array of user objects.

---

### Week 4 – Modern JavaScript & Intro to Async

**Goals:**
- Get comfortable with modern JS patterns and asynchronous code.
- Learn how to make HTTP requests from the browser.

**Core topics:**
- Modern JS patterns:
  - Destructuring objects/arrays
  - Template literals
  - Spread/rest operators
- Modules (at least conceptually): `import` / `export`
- Async JavaScript:
  - Callbacks (conceptually)
  - Promises
  - `async/await`
- Fetching data:
  - `fetch` API, `.then`, `await`
  - Handling JSON: `response.json()`
  - Basic error handling: `try/catch`

**Practical tasks:**
- Build a small “User List” page that:
  - Fetches users from a public API (e.g. https://jsonplaceholder.typicode.com/users).
  - Renders them in a list.
  - Handles loading and error states (e.g. “Loading…”, “Failed to load users”).
- Rewrite the same fetch logic using both:
  - `.then` syntax
  - `async/await` syntax

---

### Week 5 – React Fundamentals

**Goals:**
- Understand component-based thinking.
- Build small interactive UIs in React.

**Core topics:**
- React basics:
  - Components (function components)
  - JSX syntax, props
  - State with `useState`
  - Rendering lists: `.map`
  - Handling events: `onClick`, `onChange`
- Project structure:
  - Using `create-react-app` or Vite to bootstrap.
  - Separation into components folder.

**Practical tasks:**
- Set up a React app using Vite or CRA.
- Rebuild your plain JS To‑Do List in React:
  - A main `App` component.
  - A `TodoList` and `TodoItem` component.
  - Local state for tasks, add/delete/toggle complete.
- Create a simple controlled form:
  - A form with a few inputs that stores values in state and shows them live.

---

### Week 6 – React: Data Flow, Effects, and Simple Fetching

**Goals:**
- Understand state flow and side effects.
- Fetch and render data with React.

**Core topics:**
- Props vs state:
  - One-way data flow (parent → child props).
- `useEffect` basics:
  - Run on mount, dependency array.
  - Fetching data in `useEffect`.
- Conditional rendering:
  - Loading, error, empty states.
- Component composition:
  - Breaking UI into smaller reusable components.

**Practical tasks:**
- Build a “Users Dashboard” React app:
  - Fetch users (again from a public API).
  - Components: `UserList`, `UserCard`, maybe `UserDetail`.
  - Show loading/error states.
  - Add a search input to filter users by name (local filtering).
- Refactor: move repeated UI patterns into reusable components (e.g. `Card`).

---

### Week 7 – Backend Basics: Node.js & Express

**Goals:**
- Understand what a server is and how to build a basic API.
- Build and test simple REST endpoints.

**Core topics:**
- Node.js basics:
  - `npm init`, installing packages.
  - Running scripts with `node`, `nodemon`.
- Express fundamentals:
  - Creating a server.
  - Routes: `app.get`, `app.post`, `app.put`, `app.delete`.
  - Handling JSON: `express.json()`.
- HTTP basics in context:
  - Status codes: 200, 201, 400, 401, 404, 500.
  - Request vs response, headers, body, query params (`req.query`), route params (`req.params`).

**Practical tasks:**
- Create a basic Express server:
  - A few routes: `GET /`, `GET /users`, `POST /users`.
  - Use an in-memory array to store users.
- Test your endpoints with:
  - Postman or Insomnia, or `curl`.
- Add simple error handling: return appropriate status codes.

---

### Week 8 – Database & REST API with MongoDB

**Goals:**
- Persist data using a database.
- Build a real CRUD REST API.

**Core topics:**
- MongoDB basics:
  - Documents, collections.
  - Connecting from Node using Mongoose.
- Mongoose:
  - Defining schemas and models.
  - Basic CRUD: `create`, `find`, `findByIdAndUpdate`, `findByIdAndDelete`.
- REST design (80/20 version):
  - Resource-based routes: `/api/todos`, `/api/users`.
  - Consistent response shapes (e.g. `{ data: ..., error: ... }`).

**Practical tasks:**
- Set up MongoDB (Atlas or local).
- Build a `Todo` model with fields: `text`, `completed`, `createdAt`.
- Implement API routes:
  - `GET /api/todos` – list
  - `POST /api/todos` – create
  - `PUT /api/todos/:id` – update
  - `DELETE /api/todos/:id` – delete
- Test with Postman/Insomnia thoroughly.

---

### Week 9 – Connecting Frontend & Backend (Full Stack)

**Goals:**
- Connect your React frontend to your Express/Mongo backend.
- Understand CORS and environment configuration.

**Core topics:**
- CORS:
  - Why it exists, basic middleware in Express (`cors` package).
- Client–server communication:
  - Base URL configuration (using environment variables).
  - Fetching from your own API instead of a public one.
- Full-stack directory structure:
  - `client/` for React, `server/` for Express.
  - Separate `package.json` files.
- Basic error handling end-to-end:
  - Backend returns appropriate status and message.
  - Frontend shows helpful error messages.

**Practical tasks:**
- Create a full-stack “Todo App”:
  - Backend: Express + MongoDB API from last week.
  - Frontend: React app that:
    - Fetches todos from your API.
    - Allows create/update/delete.
  - Handle loading and error states.
- Set up `npm` scripts to run both client and server (e.g. using `concurrently`).

---

### Week 10 – Authentication Basics (Sessions/JWT) & Security Intro

**Goals:**
- Implement simple user authentication.
- Understand how auth works end-to-end (at a practical level).

**Core topics:**
- Authentication vs authorization (conceptual).
- Passwords:
  - Hashing with bcrypt (never store plaintext).
- JWT (JSON Web Tokens) or session-based auth (JWT is common for APIs):
  - Login route that returns a token.
  - Protecting routes with middleware that checks the token.
- Frontend auth basics:
  - Storing the token (short-term: localStorage; know risks).
  - Attaching token to API calls via headers (`Authorization: Bearer <token>`).
- Minimal security practices:
  - Never log raw passwords.
  - Validate input (at least basic checks).

**Practical tasks:**
- Extend your Express API:
  - `User` model: `email`, `passwordHash`, `createdAt`.
  - Routes: `POST /auth/register`, `POST /auth/login`.
  - JWT-based auth middleware (e.g. `authMiddleware`).
- Protect a route like `GET /api/todos` so it only returns todos for the logged-in user.
- In React:
  - Create a login/register form.
  - Store token and use it in requests.
  - Show different UI for logged-in vs logged-out states.

---

### Week 11 – Polishing UX, State Management Patterns, and Forms

**Goals:**
- Build better user experiences.
- Manage non-trivial state in React.
- Handle more complex forms.

**Core topics:**
- React state patterns:
  - Lifting state up, passing callbacks down.
  - Simple global state using Context (for auth/user).
- Forms:
  - Controlled inputs (again, but more complex forms).
  - Basic validation (required fields, email format).
- UX improvements:
  - Loading indicators (buttons disabled when submitting).
  - Toast-style messages or simple alert banners.

**Practical tasks:**
- Add a global auth context in React:
  - Provides current user and token.
  - Centralizes login/logout logic.
- Refine the login/register flow:
  - Show form validation errors.
  - Disable submit button while request is in progress.
- Add a “settings/profile” page that fetches and updates user info (protected route).

---

### Week 12 – Deployment & Production Mindset

**Goals:**
- Deploy a full-stack app.
- Understand the basics of running your app in production.

**Core topics:**
- Deployment options:
  - Frontend: Netlify, Vercel, or similar.
  - Backend: Render, Railway, Fly.io, or similar (Node + DB).
- Environment variables:
  - Keeping secrets (API keys, DB URIs) out of the repo.
- Production build:
  - `npm run build` for React.
  - Serving static files (optional: serve React from Express).
- Basic monitoring:
  - Checking logs, basic error handling in production.

**Practical tasks:**
- Deploy your full-stack app:
  - Push code to GitHub.
  - Deploy backend with a managed MongoDB instance.
  - Deploy frontend and point it at the deployed backend URL.
- Test all features in production:
  - Registration, login, CRUD operations, protected routes.
- Add a simple “About” page that explains what the app does and the stack you used.

---

## 5 Projects (Beginner → Advanced)

Work on these **during** the 12 weeks. They line up roughly with your progress but you can adjust as needed. Each project reinforces specific core skills.

---

### Project 1 (Beginner) – Static Portfolio Website  
**Best timing:** Weeks 1–2

**Description:**  
A simple, single-page personal portfolio site with sections: About, Skills, Projects, Contact.

**Key concepts reinforced:**
- Semantic HTML structure.
- CSS layout with Flexbox.
- Responsive design (mobile/desktop).
- Basic navigation (scrolling to sections).
- Using browser DevTools to tweak and debug.

**Stretch ideas:**
- Add a simple contact form (no backend yet).
- Add smooth scrolling and basic animations (CSS transitions).

---

### Project 2 (Beginner–Intermediate) – Vanilla JS To‑Do App  
**Best timing:** Weeks 3–4

**Description:**  
A client-side To‑Do List app that stores tasks in `localStorage` so they persist across refreshes.

**Core features:**
- Add, edit, delete, and mark tasks as complete.
- Filter tasks (all, active, completed).
- Persist data in `localStorage`.

**Key concepts reinforced:**
- DOM manipulation with JavaScript.
- Event handling (`click`, `submit`, `input`).
- Arrays and objects in real usage.
- Basic app state management.
- Saving and loading from `localStorage`.

**Stretch ideas:**
- Add basic priority levels (e.g., low/medium/high).
- Add a “due date” and sort tasks by due date.

---

### Project 3 (Intermediate) – React “Mini Dashboard” (Frontend Only)  
**Best timing:** Weeks 5–6

**Description:**  
A small React dashboard that pulls data from a public API and presents it in multiple views (e.g., a list, cards, detail view).

Example: “GitHub User Explorer”:
- Search for a GitHub username.
- Display their profile + repos.
- Filter repos by language or stars.

**Core features:**
- Search input and controlled forms.
- Fetching data from an external API.
- Loading and error states.
- Components for list, card, and detail views.

**Key concepts reinforced:**
- React components, props, and state.
- `useEffect` for data fetching.
- Conditional rendering.
- Thinking in components and lifting state up.

**Stretch ideas:**
- Pagination or “Load more” for repos.
- Client-side caching (store last searched user in state or localStorage).

---

### Project 4 (Intermediate–Advanced) – Full-Stack CRUD App (e.g., “Task Manager”)  
**Best timing:** Weeks 7–9

**Description:**  
A full-stack Task Manager app with users, tasks, and CRUD operations on tasks.

**Suggested features:**
- Backend:
  - Express + MongoDB REST API.
  - Models: `User`, `Task` (with fields like `title`, `description`, `status`, `dueDate`, `owner`).
  - Auth: registration, login, JWT-based auth.
  - Protected routes (only owner can access their tasks).
- Frontend:
  - React app with:
    - Authentication (login/register forms).
    - Task list, create/edit/delete tasks.
    - Filters (by status, due date).
    - Loading/error handling.

**Key concepts reinforced:**
- Node.js & Express routing.
- MongoDB & Mongoose models and queries.
- REST API design and HTTP status codes.
- Auth with JWT, protected backend routes.
- Consuming a custom API from React.
- Managing app-wide auth state.

**Stretch ideas:**
- Add pagination or infinite scroll for tasks.
- Add basic role-based access (e.g., admin can see all users’ tasks).

---

### Project 5 (Advanced) – “Feature-Rich” Full-Stack App & Deployment  
**Best timing:** Weeks 10–12

**Example idea:** “Habit Tracker” or “Simple Project Management Tool”.

**Description (Habit Tracker example):**
- Users can register and log in.
- Create habits (e.g., “Exercise”, “Read”).
- Track daily completion (e.g., checkboxes per day).
- Visualize streaks or progress (simple charts or counters).

**Core features:**
- Complete auth system (register, login, logout).
- Multiple data models with relationships (User, Habit, HabitEntry).
- Complex forms (create habit with schedule, reminders).
- Frontend:
  - Dashboard view (summary of today’s habits).
  - Habit detail pages.
  - State management via context for auth and user data.
- Deployment:
  - Backend + DB deployed (e.g. Render + MongoDB Atlas).
  - Frontend deployed (e.g. Netlify/Vercel).
  - Environment variables configured correctly across environments.

**Key concepts reinforced:**
- Designing and modeling data for a real use case.
- Handling more complex API endpoints.
- Frontend architecture: separating pages, components, and services.
- Global state (e.g., auth context).
- Deployment pipeline and production debugging.

**Stretch ideas:**
- Add email-based password reset (even if just simulated).
- Add basic analytics (e.g., how many days in a row a habit has been completed).
- Performance improvements (memoization, lazy loading routes, etc.).

---

## How to Get the Most Out of This Plan

1. **Learn just enough, then build.**  
   Don’t wait to “finish the chapter” before touching code. After each core topic, implement something small.

2. **Struggle productively.**  
   When stuck:
   - First: read the error carefully, inspect the network tab, check logs.
   - Second: Google the exact error message.
   - Third: look at docs (React, MDN, Express, Mongoose).
   - Only then: check tutorials/Stack Overflow.

3. **Keep everything in Git.**
   - Initialize a Git repo for each project.
   - Commit frequently with descriptive messages.
   - Push to GitHub and keep your profile growing.

4. **Write down questions.**  
   Maintain a “questions & gotchas” doc: whenever something confuses you, write it down and later look up the answer.

5. **Iterate on projects.**  
   It’s better to have 3–5 projects that you’ve improved multiple times than 20 half-finished ones.

---

If you’d like, I can next:
- Turn this into a printable weekly checklist, or
- Suggest concrete daily tasks for Week 1 to get you started.
