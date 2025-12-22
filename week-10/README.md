Here’s your **Week 10 (Days 1–7) plan**, focused on **turning what you’ve built into a more “real” app**:

- Frontend routing (multi-page SPA with React Router)  
- Better UX (protected routes, loading, error boundaries)  
- Project structure & cleanup  
- Planning your first “portfolio‑worthy” full‑stack app

Assume ~2–3 hours/day.  
Each day: **Learn → Do → Reflect → Stretch**.  
You’ll build on your existing stack: **React + Auth + Express + MongoDB**.

---

## Day 1 – Frontend Routing with React Router (Basic Pages)

**Goals:**
- Add **client-side routing** to your React app using React Router.
- Split your app into multiple “pages” (e.g. Home, Login, Todos).

### 1. Learn (40–60 minutes)

Concepts:
- SPA vs traditional multi-page apps:
  - SPA: single HTML page; JS swaps views client-side.
- React Router basics:
  - `<BrowserRouter>`, `<Routes>`, `<Route>`, `<Link>`, `<NavLink>`.

Read:
- React Router docs: “Quick Start” (v6+).
- Focus on:
  - Basic route definitions.
  - Navigating with `<Link>` instead of `<a>`.

Notes:
- Write down:
  - How to wrap your app in `<BrowserRouter>`.
  - One example of a route config: `/todos` → `<TodoPage />`.

### 2. Do (60–90 minutes)

In your React project:

1. **Install React Router:**

   ```bash
   npm install react-router-dom
   ```

2. **Set up routing in `main.jsx` (or similar entry):**

   ```jsx
   import { BrowserRouter } from "react-router-dom";

   ReactDOM.createRoot(document.getElementById("root")).render(
     <React.StrictMode>
       <AuthProvider>
         <BrowserRouter>
           <App />
         </BrowserRouter>
       </AuthProvider>
     </React.StrictMode>
   );
   ```

3. **Define routes in `App.jsx`:**

   Create simple page components:

   ```jsx
   import { Routes, Route, Link } from "react-router-dom";
   import { useAuth } from "./AuthContext";
   import LoginForm from "./LoginForm";
   import TodoApp from "./TodoApp";

   function HomePage() {
     return (
       <div>
         <h1>Welcome</h1>
         <p>This is your full-stack practice app.</p>
       </div>
     );
   }

   function App() {
     const { user, logout } = useAuth();

     return (
       <div>
         <nav>
           <Link to="/">Home</Link>{" | "}
           <Link to="/todos">Todos</Link>{" | "}
           {!user && <Link to="/login">Login</Link>}
           {user && (
             <button onClick={logout} style={{ marginLeft: 8 }}>
               Logout
             </button>
           )}
         </nav>

         <Routes>
           <Route path="/" element={<HomePage />} />
           <Route path="/login" element={<LoginForm />} />
           <Route path="/todos" element={<TodoApp />} />
         </Routes>
       </div>
     );
   }

   export default App;
   ```

4. **Test navigation:**
   - Click links, see URL change, component change without full page reload.
   - Confirm Todo app still works when visiting `/todos`.

### 3. Reflect (10–15 minutes)

- How is client-side routing different from separate HTML pages?
- What advantages does this give you for building richer apps?

### 4. Stretch (optional, 20–30 minutes)

- Use `<NavLink>` instead of `<Link>` to add active link styling.
- Add a simple **404 page** route (`path="*"`).

---

## Day 2 – Protected Routes (Only Authenticated Users Access Certain Pages)

**Goals:**
- Create **protected routes** that require login.
- Redirect unauthenticated users to the login page.

### 1. Learn (30–45 minutes)

Concepts:
- Route guarding:
  - Check auth state before rendering certain routes.
- Redirecting with React Router:
  - `useNavigate()` hook.
  - `<Navigate to="/login" />` element.

Read:
- React Router docs: “Authentication” guide (v6).
- Focus on the idea of a `<ProtectedRoute>` component.

Notes:
- Sketch how `<ProtectedRoute>` might work:
  - If `user`, render children.
  - Else, `<Navigate to="/login" replace />`.

### 2. Do (60–90 minutes)

1. **Create `ProtectedRoute.jsx`:**

   ```jsx
   import { Navigate, useLocation } from "react-router-dom";
   import { useAuth } from "./AuthContext";

   function ProtectedRoute({ children }) {
     const { user } = useAuth();
     const location = useLocation();

     if (!user) {
       return <Navigate to="/login" replace state={{ from: location }} />;
     }

     return children;
   }

   export default ProtectedRoute;
   ```

2. **Wrap your protected routes (`/todos`) in `App.jsx`:**

   ```jsx
   import ProtectedRoute from "./ProtectedRoute";

   // ...
   <Routes>
     <Route path="/" element={<HomePage />} />
     <Route path="/login" element={<LoginForm />} />
     <Route
       path="/todos"
       element={
         <ProtectedRoute>
           <TodoApp />
         </ProtectedRoute>
       }
     />
   </Routes>
   ```

3. **Optional “redirect back” after login:**
   - In `LoginForm`, read `location.state.from` and navigate there on success.

   Example (within `LoginForm`):

   ```jsx
   import { useLocation, useNavigate } from "react-router-dom";

   const location = useLocation();
   const navigate = useNavigate();
   const from = location.state?.from?.pathname || "/";

   // after successful login:
   auth.login(data.token, data.user);
   navigate(from, { replace: true });
   ```

4. **Test behavior:**
   - Logged out:
     - Try visiting `/todos` directly → should redirect to `/login`.
   - After login:
     - Visit `/todos` successfully.

### 3. Reflect (10–15 minutes)

- How does `ProtectedRoute` use composition (children) to guard any component?
- Why is redirecting back to `from` a nice UX improvement?

### 4. Stretch (optional, 20–30 minutes)

- Add a `/profile` page that also requires auth and shows `user.email` etc.
- Display a clear message on login page like “You must be logged in to view that page” when redirected.

---

## Day 3 – Better UX: Loading States, Error Handling, and Toast Notifications

**Goals:**
- Improve perceived quality of your app:
  - Consistent loading indicators.
  - Friendly error messages.
  - Optional: simple toast/alert notifications.

### 1. Learn (30–45 minutes)

Concepts:
- UX basics:
  - Don’t leave the user guessing.
  - Always show some feedback on async actions.
- Centralizing error and loading patterns.

Browse:
- Your existing components (`LoginForm`, `TodoApp`) and note inconsistent patterns.
- Optional: look at a minimal toast library (but you can build your own simple component).

In notes:
- List 2–3 improvements you want to make this week for UX:
  - E.g. “Show spinner on Todo fetch”, “Show success/error message after actions”.

### 2. Do (60–90 minutes)

1. **Global message/toast component (simple version):**

   - `MessageBar.jsx`:

     ```jsx
     function MessageBar({ message, type = "info", onClose }) {
       if (!message) return null;

       const background = type === "error" ? "#fdecea" : "#e6f4ea";
       const color = type === "error" ? "#b00020" : "#0d652d";

       return (
         <div
           style={{
             background,
             color,
             padding: "8px 12px",
             marginBottom: 8,
             borderRadius: 4,
             display: "flex",
             justifyContent: "space-between",
             alignItems: "center",
           }}
         >
           <span>{message}</span>
           <button onClick={onClose} style={{ marginLeft: 8 }}>
             ×
           </button>
         </div>
       );
     }

     export default MessageBar;
     ```

   - You can manage its state in `App` or per-page.

2. **Make TodoApp loading/error consistent:**
   - Ensure `TodoApp`:
     - Shows a clear “Loading todos…” message while fetching.
     - Shows friendly error: “Could not load todos. Please try again.”
     - Resets error when retrying.

3. **Add feedback for actions:**
   - After adding/deleting a todo:
     - Optionally show a temporary message using `MessageBar`.
     - E.g., “Task added” / “Task deleted”.

### 3. Reflect (10–15 minutes)

- What change from today makes the app feel most “professional”?
- How does having a reusable `MessageBar` component help clean up your code?

### 4. Stretch (optional, 20–30 minutes)

- Add a small loading spinner (CSS) instead of plain text for loading state.
- Add a confirm dialog (or simple `window.confirm`) before deleting a todo.

---

## Day 4 – Project Structure & Code Organization

**Goals:**
- Clean up your React project structure.
- Make backend routes more modular (e.g., split auth/todos routes & controllers).
- Prepare for scaling the codebase.

### 1. Learn (30–45 minutes)

Concepts:
- Common React folder structures:
  - `components/`, `pages/`, `hooks/`, `context/`, `services/`.
- Backend structure:
  - `routes/`, `controllers/`, `models/`, `middleware/`, `config/`.
- Separation of concerns:
  - Keep API calls in a separate `api`/`services` module instead of scattered in components.

Skim:
- An article or repo example: “Express project structure for beginners”.
- A React project structure article (ignore very advanced patterns for now).

In notes:
- Draft a target structure for:
  - Frontend folders.
  - Backend folders.

### 2. Do (60–90 minutes)

1. **Frontend reorganization:**
   - Create:
     - `src/components/` – reusable UI components (`MessageBar`, `TodoList`, `TodoItem`, `ProtectedRoute`, etc.).
     - `src/pages/` – route-level components (`HomePage`, `TodosPage`, `LoginPage`).
     - `src/context/` – `AuthContext`.
     - `src/services/` – API helper functions (`todoApi.js`, `authApi.js`).

   - Example: move API calls from `TodoApp` into `services/todoApi.js`:

     ```jsx
     const BASE_URL = "http://localhost:3000/api";

     export async function fetchTodos(token) {
       const res = await fetch(`${BASE_URL}/todos`, {
         headers: { Authorization: `Bearer ${token}` },
       });
       if (!res.ok) throw new Error(`HTTP error ${res.status}`);
       return res.json();
     }

     // etc. for createTodo, updateTodo, deleteTodo
     ```

   - `TodoApp` now calls these functions instead of raw `fetch`.

2. **Backend reorganization:**
   - Ensure:
     - `models/` has `User.js`, `Todo.js`.
     - `routes/` has `auth.js`, `todos.js`.
     - `middleware/` has `auth.js`.
     - `config/` has `db.js`.

   - Move your todo routes into `routes/todos.js`:

     ```js
     const express = require("express");
     const Todo = require("../models/Todo");
     const auth = require("../middleware/auth");

     const router = express.Router();

     router.use(auth);

     router.get("/", async (req, res) => { ... });
     router.post("/", async (req, res) => { ... });
     // etc.

     module.exports = router;
     ```

   - In `index.js`:

     ```js
     const todoRouter = require("./routes/todos");
     app.use("/api/todos", todoRouter);
     ```

3. **Fix imports & test:**
   - Run frontend & backend, confirm everything still works.

### 3. Reflect (10–15 minutes)

- How does this structure make it easier to find and change code?
- If you handed this project to another developer, would they understand where things go?

### 4. Stretch (optional, 20–30 minutes)

- Add a brief `README.md` at the root of each project describing:
  - What it does.
  - How to run it (commands).
  - Basic routes/pages.

---

## Day 5 – Planning Your “Capstone” Full-Stack Project

**Goals:**
- Define a concrete, realistic full-stack project to build in Weeks 11–12.
- Design its features, data models, and high-level architecture.

Examples:
- Task Manager (with projects, tasks, status).
- Habit Tracker.
- Simple Project Management Board (like mini Trello).
- Book Tracker / Learning Journal.

### 1. Learn (30–45 minutes)

Concepts:
- MVP (Minimum Viable Product):
  - Start small, core features only.
- User stories:
  - “As a [user type], I want [feature] so that [value].”
- Data modeling:
  - Entities, relationships (User–Task, User–Habit, etc.).

Read:
- Short article on “How to define an MVP for a side project”.
- Optional: quick read on basic data modeling for MongoDB.

### 2. Do (60–90 minutes)

1. **Pick your project idea (commit to one):**
   - Write a short 2–3 sentence description.

2. **Write user stories:**
   - Aim for 6–10 core user stories.
   - Example (Task Manager):
     - As a logged-in user, I can create tasks with title, description, due date, and status.
     - As a logged-in user, I can see a list of all my tasks.
     - As a logged-in user, I can filter tasks by status (To Do, In Progress, Done).
     - As a logged-in user, I can mark tasks completed.

3. **Define data models:**
   - Start with `User` (you mostly have this).
   - Define main resource model(s), e.g. `Task`, `Project`, `Habit`.
   - For each, list fields and types (roughly), e.g.:

     ```txt
     Task:
       - title (String, required)
       - description (String)
       - status (String: "todo" | "in-progress" | "done")
       - dueDate (Date | null)
       - user (ObjectId ref User, required)
       - createdAt, updatedAt (timestamps)
     ```

4. **Draft API endpoints:**
   - For each resource, list:
     - GET /api/tasks
     - POST /api/tasks
     - GET /api/tasks/:id
     - PUT /api/tasks/:id
     - DELETE /api/tasks/:id

   - Note which ones require auth (most of them).

### 3. Reflect (10–15 minutes)

- Does your MVP feel achievable in 2 weeks (Weeks 11–12)?
- Which parts reuse patterns you already know (todos, auth)? Which parts are new?

### 4. Stretch (optional, 20–30 minutes)

- Sketch UI wireframes (on paper or digital):
  - Main dashboard page.
  - Detail/edit view for a resource (e.g., task).
  - Auth flow pages.
- Identify one “wow” feature you might add later (kanban drag-and-drop, charts, etc.), but keep it out of the initial MVP.

---

## Day 6 – Breaking the Capstone into Backend & Frontend Tasks

**Goals:**
- Translate your project design into concrete implementation steps.
- Create a rough **task list** for backend and frontend work.

### 1. Learn (20–30 minutes)

Concepts:
- “Walking skeleton”:
  - Get a minimal end-to-end system running before adding features.
- Iterative development:
  - Implement smallest usable version, then expand.

In notes:
- Write what your “walking skeleton” for this project would look like:
  - e.g., Signup/login + one basic create/list view for main resource.

### 2. Do (60–90 minutes)

1. **Backend task breakdown:**
   - Example (for Task Manager):
     - [ ] Create `Task` model in `models/Task.js`.
     - [ ] Add `routes/tasks.js` with CRUD routes (all protected).
     - [ ] Implement ownership checks (`user: req.user.userId`).
     - [ ] Add basic validation (title required, status enum).
     - [ ] Add optional stats endpoint (e.g., counts by status).

2. **Frontend task breakdown:**
   - Example:
     - [ ] Add route `/tasks` (protected).
     - [ ] Create `TasksPage` with:
       - [ ] List of tasks.
       - [ ] Form to create new task.
     - [ ] Add ability to edit a task.
     - [ ] Add filters (by status).
     - [ ] Integrate with auth (only show tasks for logged-in user).
   - Prioritize tasks:
     - Mark what’s essential for MVP vs nice-to-have.

3. **Timeline:**
   - Roughly assign tasks to Week 11 and Week 12:
     - Week 11: backend endpoints + basic frontend pages + core CRUD.
     - Week 12: polish, UX, deployment.

### 3. Reflect (10–15 minutes)

- Does your breakdown feel realistic with your available time?
- Which part are you most excited to start? Which part feels intimidating?

### 4. Stretch (optional, 20–30 minutes)

- Create GitHub repos (frontend + backend) for this project if you haven’t already.
- Add issues or a TODO list based on the task breakdown.

---

## Day 7 – Week 10 Review & Readiness Check

**Goals:**
- Review and solidify everything from Weeks 7–10 (backend + auth + routing).
- Confirm you’re ready to start building your capstone in Weeks 11–12.

### 1. Review (30–45 minutes)

Revisit key files and concepts:

- Backend:
  - `User` model, `auth` routes, `authMiddleware`.
  - `Todo` (or equivalent) model and routes with ownership.
  - DB connection and environment variables.

- Frontend:
  - `AuthContext` (or auth state management).
  - `ProtectedRoute`.
  - React Router setup (`Routes`, `Route`, `Link`).
  - API services (`services/`).

In notes, write brief answers:

- How does a login request flow from React → Express → Mongo → React?
- How does a protected route prevent unauthorized access?
- What’s the difference between authentication and authorization in your app right now?

### 2. Do – Small Cleanup/Polish Pass (60–90 minutes)

1. **Code cleanup:**
   - Remove unused code/files.
   - Ensure naming is consistent (e.g., `TasksPage` vs `TaskPage`).
   - Fix any obvious linting issues if you use ESLint.

2. **UX sanity pass:**
   - Navigate from login → todos → logout.
   - Try invalid routes (e.g., `/abc`) and make sure 404 page appears.
   - Check error messages are human-readable.

3. **Docs:**
   - Update or create a top-level `README.md` for your current learning project:
     - Stack summary (React, Express, MongoDB, JWT auth).
     - How to run frontend & backend.
     - Basic features and routes.

### 3. Self-Assessment Checklist (20–30 minutes)

Mark ✅ / ❌ and note what to review if ❌:

- Routing & UX:
  - [ ] I can set up React Router and define routes.
  - [ ] I can create protected routes that require auth.
  - [ ] I provide feedback for loading and errors.

- Backend + Auth:
  - [ ] I can design and implement secure CRUD endpoints with Express + Mongoose.
  - [ ] I can build register/login with hashed passwords + JWTs.
  - [ ] I can enforce user ownership on resources.

- Project planning:
  - [ ] I have a clear project idea for my capstone.
  - [ ] I have written user stories and data models.
  - [ ] I have a rough task breakdown for backend and frontend.

Write a paragraph:
- What feels like your **biggest strength** right now?
- What is the **one concept** you want to keep revisiting as you build your capstone (e.g., error handling, state management, auth flows)?

### 4. Stretch (optional, 30–45 minutes)

- Do a “mini dry run” of your capstone:
  - Create stub files for your new models/routes/components.
  - Get a minimal “Hello from NewProject” page served on frontend and backend.
- Or:
  - Try deploying your current app (or a simplified version) to a platform like Render (backend) + Netlify/Vercel (frontend), just to see the deployment flow before your capstone.

---

If you’d like next, I can:

- Create a **Week 11** plan specifically for implementing the **backend** of your capstone project, or  
- Help you refine your capstone idea and data model before you start building.
