Here’s your **Week 12 (Days 1–7) plan**, focused on building the **frontend for your capstone** and connecting it to your finished backend:

- React + Router + AuthContext  
- CRUD UI for your main resource (Task/Habit/etc.)  
- UX polish + deployment prep  

Assume ~2–3 hours/day.  
Each day: **Learn → Do → Reflect → Stretch**.  
I’ll call your main resource `Item` generically; substitute `Task`, `Habit`, etc.

---

## Day 1 – Frontend Project Setup & Basic Pages

**Goals:**
- Create a dedicated React frontend for your capstone.
- Set up routing, layout, and AuthContext (or reuse from your learning app).

### 1. Learn (20–30 minutes)

You already know React + Router; today is about applying it cleanly:

Think through:
- What **pages** you need:
  - `/` – Home/landing/dashboard overview.
  - `/login` – Login (and maybe register).
  - `/items` – Main list page.
  - `/items/:id` – Detail/edit page (optional, can come later).
- What **global layout** you want:
  - Navbar with links, login/logout, app title.

In your notes:
- List your planned pages and key components.

### 2. Do (60–90 minutes)

1. **Create React app (Vite + React suggested):**

   ```bash
   npm create vite@latest capstone-frontend -- --template react
   cd capstone-frontend
   npm install
   npm install react-router-dom
   ```

2. **Project structure (basic):**

   Inside `src/` create:

   - `pages/` – `HomePage.jsx`, `LoginPage.jsx`, `ItemsPage.jsx` (empty for now).
   - `components/` – `Navbar.jsx`, maybe `MessageBar.jsx`.
   - `context/` – `AuthContext.jsx`.
   - `services/` – `authApi.js`, `itemsApi.js`.

3. **Set up Router in `main.jsx`:**

   ```jsx
   import React from "react";
   import ReactDOM from "react-dom/client";
   import { BrowserRouter } from "react-router-dom";
   import App from "./App";
   import { AuthProvider } from "./context/AuthContext";

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

4. **Define routes in `App.jsx`:**

   ```jsx
   import { Routes, Route } from "react-router-dom";
   import Navbar from "./components/Navbar";
   import HomePage from "./pages/HomePage";
   import LoginPage from "./pages/LoginPage";
   import ItemsPage from "./pages/ItemsPage";

   function App() {
     return (
       <div>
         <Navbar />
         <main style={{ maxWidth: 900, margin: "0 auto", padding: "1rem" }}>
           <Routes>
             <Route path="/" element={<HomePage />} />
             <Route path="/login" element={<LoginPage />} />
             <Route path="/items" element={<ItemsPage />} />
           </Routes>
         </main>
       </div>
     );
   }

   export default App;
   ```

5. **Create simple placeholder pages:**

   `HomePage.jsx`:

   ```jsx
   function HomePage() {
     return (
       <div>
         <h1>Your App Name</h1>
         <p>Welcome! Log in to manage your items.</p>
       </div>
     );
   }

   export default HomePage;
   ```

   `LoginPage.jsx` and `ItemsPage.jsx` can just return headings for now.

6. **Navbar component:**

   ```jsx
   import { Link } from "react-router-dom";

   function Navbar() {
     return (
       <nav style={{ padding: "0.5rem 1rem", borderBottom: "1px solid #ddd" }}>
         <Link to="/">Home</Link> | <Link to="/items">Items</Link> |{" "}
         <Link to="/login">Login</Link>
       </nav>
     );
   }

   export default Navbar;
   ```

### 3. Reflect (10–15 minutes)

- Does your route structure match the user flows you planned in Week 10?
- What pages will need auth protection?

### 4. Stretch (optional, 20–30 minutes)

- Add a simple `404` page with `Route path="*"` and a link back to Home.
- Start sketching the layout for `ItemsPage` (list on left, form on top or side, etc.).

---

## Day 2 – AuthContext & Login Flow (Frontend Only)

**Goals:**
- Implement authentication context (AuthProvider).
- Build a login form that calls your backend’s `/api/auth/login`.

### 1. Learn (20–30 minutes)

Concepts you’re applying:
- Storing `token` and `user` in React context.
- Persisting auth in `localStorage`.
- Redirecting after login.

In your notes:
- Sketch `AuthContext` value: `{ user, token, login, logout }`.
- Decide where you’ll redirect after login (e.g., `/items`).

### 2. Do (60–90 minutes)

1. **AuthContext (`src/context/AuthContext.jsx`):**

   ```jsx
   import { createContext, useContext, useEffect, useState } from "react";

   const AuthContext = createContext(null);

   export function AuthProvider({ children }) {
     const [user, setUser] = useState(null);
     const [token, setToken] = useState(null);

     useEffect(() => {
       const storedToken = localStorage.getItem("token");
       const storedUser = localStorage.getItem("user");
       if (storedToken && storedUser) {
         setToken(storedToken);
         setUser(JSON.parse(storedUser));
       }
     }, []);

     function login(token, user) {
       setToken(token);
       setUser(user);
       localStorage.setItem("token", token);
       localStorage.setItem("user", JSON.stringify(user));
     }

     function logout() {
       setToken(null);
       setUser(null);
       localStorage.removeItem("token");
       localStorage.removeItem("user");
     }

     return (
       <AuthContext.Provider value={{ user, token, login, logout }}>
         {children}
       </AuthContext.Provider>
     );
   }

   export function useAuth() {
     return useContext(AuthContext);
   }
   ```

2. **Auth API helper (`src/services/authApi.js`):**

   ```jsx
   const BASE_URL = import.meta.env.VITE_API_URL || "http://localhost:3000/api";

   export async function loginRequest(email, password) {
     const res = await fetch(`${BASE_URL}/auth/login`, {
       method: "POST",
       headers: { "Content-Type": "application/json" },
       body: JSON.stringify({ email, password }),
     });

     const data = await res.json().catch(() => ({}));

     if (!res.ok) {
       throw new Error(data.error || `Login failed (${res.status})`);
     }

     return data; // { token, user: { id, email, ... } }
   }
   ```

3. **Login Page (`pages/LoginPage.jsx`):**

   ```jsx
   import { useState } from "react";
   import { useNavigate, useLocation } from "react-router-dom";
   import { useAuth } from "../context/AuthContext";
   import { loginRequest } from "../services/authApi";

   function LoginPage() {
     const [email, setEmail] = useState("");
     const [password, setPassword] = useState("");
     const [error, setError] = useState(null);
     const [loading, setLoading] = useState(false);
     const auth = useAuth();
     const navigate = useNavigate();
     const location = useLocation();

     const from = location.state?.from?.pathname || "/items";

     async function handleSubmit(e) {
       e.preventDefault();
       setError(null);
       setLoading(true);
       try {
         const data = await loginRequest(email, password);
         auth.login(data.token, data.user);
         navigate(from, { replace: true });
       } catch (err) {
         setError(err.message);
       } finally {
         setLoading(false);
       }
     }

     return (
       <div>
         <h1>Login</h1>
         {error && <p style={{ color: "red" }}>{error}</p>}
         <form onSubmit={handleSubmit}>
           <div>
             <label>Email</label>
             <input
               type="email"
               value={email}
               onChange={(e) => setEmail(e.target.value)}
               required
             />
           </div>
           <div>
             <label>Password</label>
             <input
               type="password"
               value={password}
               onChange={(e) => setPassword(e.target.value)}
               required
             />
           </div>
           <button type="submit" disabled={loading}>
             {loading ? "Logging in..." : "Login"}
           </button>
         </form>
       </div>
     );
   }

   export default LoginPage;
   ```

4. **Update Navbar to show login/logout state:**

   ```jsx
   import { Link } from "react-router-dom";
   import { useAuth } from "../context/AuthContext";

   function Navbar() {
     const { user, logout } = useAuth();

     return (
       <nav style={{ padding: "0.5rem 1rem", borderBottom: "1px solid #ddd" }}>
         <Link to="/">Home</Link> | <Link to="/items">Items</Link>
         <span style={{ float: "right" }}>
           {user ? (
             <>
               <span style={{ marginRight: 8 }}>Logged in as {user.email}</span>
               <button onClick={logout}>Logout</button>
             </>
           ) : (
             <Link to="/login">Login</Link>
           )}
         </span>
       </nav>
     );
   }

   export default Navbar;
   ```

### 3. Reflect (10–15 minutes)

- What part of connecting the login form to your API felt most fragile or confusing?
- How will you handle login errors to keep the user informed without overwhelming them?

### 4. Stretch (optional, 20–30 minutes)

- Add a basic **register page** that calls `/api/auth/register`, then logs the user in.
- Add a “remember me” checkbox that you might later use to adjust token expiry on backend.

---

## Day 3 – Protected Routes & Initial Items Fetch

**Goals:**
- Protect `/items` route so only logged-in users can access.
- Fetch the user’s items from `/api/items` and display them.

### 1. Learn (20–30 minutes)

Concepts:
- ProtectedRoute pattern (you used it before).
- Using `token` from context when calling APIs.

In your notes:
- Write a minimal version of `ProtectedRoute` logic.

### 2. Do (60–90 minutes)

1. **ProtectedRoute (`src/components/ProtectedRoute.jsx`):**

   ```jsx
   import { Navigate, useLocation } from "react-router-dom";
   import { useAuth } from "../context/AuthContext";

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

2. **Wrap `/items` route in `App.jsx`:**

   ```jsx
   import ProtectedRoute from "./components/ProtectedRoute";

   // ...
   <Routes>
     <Route path="/" element={<HomePage />} />
     <Route path="/login" element={<LoginPage />} />
     <Route
       path="/items"
       element={
         <ProtectedRoute>
           <ItemsPage />
         </ProtectedRoute>
       }
     />
   </Routes>
   ```

3. **Items API helper (`src/services/itemsApi.js`):**

   ```jsx
   const BASE_URL = import.meta.env.VITE_API_URL || "http://localhost:3000/api";

   export async function fetchItems(token) {
     const res = await fetch(`${BASE_URL}/items`, {
       headers: {
         Authorization: `Bearer ${token}`,
       },
     });
     const data = await res.json().catch(() => ({}));
     if (!res.ok) {
       throw new Error(data.error || `Failed to fetch items (${res.status})`);
     }
     return data;
   }
   ```

4. **ItemsPage basic implementation (`pages/ItemsPage.jsx`):**

   ```jsx
   import { useEffect, useState } from "react";
   import { useAuth } from "../context/AuthContext";
   import { fetchItems } from "../services/itemsApi";

   function ItemsPage() {
     const { token } = useAuth();
     const [items, setItems] = useState([]);
     const [loading, setLoading] = useState(false);
     const [error, setError] = useState(null);

     useEffect(() => {
       async function load() {
         try {
           setLoading(true);
           setError(null);
           const data = await fetchItems(token);
           setItems(data);
         } catch (err) {
           setError(err.message);
         } finally {
           setLoading(false);
         }
       }
       load();
     }, [token]);

     if (loading) return <p>Loading items...</p>;
     if (error) return <p style={{ color: "red" }}>Error: {error}</p>;

     return (
       <div>
         <h1>Your Items</h1>
         {items.length === 0 ? (
           <p>No items yet.</p>
         ) : (
           <ul>
             {items.map((item) => (
               <li key={item._id}>
                 {item.title} – {item.status}
               </li>
             ))}
           </ul>
         )}
       </div>
     );
   }

   export default ItemsPage;
   ```

### 3. Reflect (10–15 minutes)

- How did you handle the “no token” case (via ProtectedRoute)?
- Do you see any duplication between this ItemsPage and your earlier todo React app that you could refactor later?

### 4. Stretch (optional, 20–30 minutes)

- Add a **refresh** button that re-calls `fetchItems`.
- Show a small count: “You have X items” above the list.

---

## Day 4 – Create/Update/Delete Items UI

**Goals:**
- Implement item creation and modification from the UI.
- Wire up POST/PUT/DELETE to your backend.

### 1. Learn (20–30 minutes)

Concepts:
- Controlled forms for item creation (title, description, etc.).
- Updating local state after successful API calls.

Plan in notes:
- What fields your create form will have.
- Whether you’ll do inline editing or a separate edit form.

### 2. Do (90–120 minutes)

1. **Extend items API (`itemsApi.js`):**

   ```jsx
   export async function createItem(token, itemData) {
     const res = await fetch(`${BASE_URL}/items`, {
       method: "POST",
       headers: {
         "Content-Type": "application/json",
         Authorization: `Bearer ${token}`,
       },
       body: JSON.stringify(itemData),
     });
     const data = await res.json().catch(() => ({}));
     if (!res.ok) throw new Error(data.error || `Failed to create item (${res.status})`);
     return data;
   }

   export async function updateItem(token, id, updates) {
     const res = await fetch(`${BASE_URL}/items/${id}`, {
       method: "PUT",
       headers: {
         "Content-Type": "application/json",
         Authorization: `Bearer ${token}`,
       },
       body: JSON.stringify(updates),
     });
     const data = await res.json().catch(() => ({}));
     if (!res.ok) throw new Error(data.error || `Failed to update item (${res.status})`);
     return data;
   }

   export async function deleteItem(token, id) {
     const res = await fetch(`${BASE_URL}/items/${id}`, {
       method: "DELETE",
       headers: {
         Authorization: `Bearer ${token}`,
       },
     });
     const data = await res.json().catch(() => ({}));
     if (!res.ok) throw new Error(data.error || `Failed to delete item (${res.status})`);
     return data;
   }
   ```

2. **Add an “Add Item” form in `ItemsPage`:**

   - Above the list:

     ```jsx
     import { createItem, updateItem, deleteItem } from "../services/itemsApi";

     // inside ItemsPage component
     const [newTitle, setNewTitle] = useState("");

     async function handleAdd(e) {
       e.preventDefault();
       const title = newTitle.trim();
       if (!title) return;
       try {
         const created = await createItem(token, { title });
         setItems((prev) => [created, ...prev]);
         setNewTitle("");
       } catch (err) {
         setError(err.message);
       }
     }
     ```

   - JSX:

     ```jsx
     <form onSubmit={handleAdd} style={{ marginBottom: "1rem" }}>
       <input
         type="text"
         placeholder="New item title..."
         value={newTitle}
         onChange={(e) => setNewTitle(e.target.value)}
       />
       <button type="submit">Add</button>
     </form>
     ```

3. **Add complete/edit/delete controls to each item:**

   - For a minimal version, you might:
     - Toggle status (e.g. todo ↔ done).
     - Delete item.

   Example in the list:

   ```jsx
   async function handleToggleStatus(item) {
     const newStatus = item.status === "done" ? "todo" : "done";
     try {
       const updated = await updateItem(token, item._id, { status: newStatus });
       setItems((prev) => prev.map((i) => (i._id === updated._id ? updated : i)));
     } catch (err) {
       setError(err.message);
     }
   }

   async function handleDelete(id) {
     if (!window.confirm("Delete this item?")) return;
     try {
       await deleteItem(token, id);
       setItems((prev) => prev.filter((i) => i._id !== id));
     } catch (err) {
       setError(err.message);
     }
   }
   ```

   - Within `map`:

     ```jsx
     {items.map((item) => (
       <li key={item._id}>
         <span
           style={{
             textDecoration: item.status === "done" ? "line-through" : "none",
           }}
         >
           {item.title} – {item.status}
         </span>
         <button onClick={() => handleToggleStatus(item)}>
           {item.status === "done" ? "Mark todo" : "Mark done"}
         </button>
         <button onClick={() => handleDelete(item._id)}>Delete</button>
       </li>
     ))}
     ```

### 3. Reflect (10–15 minutes)

- How did you keep the frontend state in sync with the backend?
- What would break if you forgot to update the state after a successful API call?

### 4. Stretch (optional, 20–30 minutes)

- Add fields like `description`, `status`, `dueDate` to the create form.
- Add inline editing for the item title (click to turn into an input, then save via `updateItem`).

---

## Day 5 – Filters, Stats & Domain-Specific UI

**Goals:**
- Use your backend stats/filters endpoints to enhance the UI.
- Build domain-specific features (e.g. status filters, overdue tab, progress stats).

### 1. Learn (20–30 minutes)

Revisit:
- The extra backend endpoints you built in Week 11, e.g.:
  - `/api/items/stats`
  - `/api/items/overdue`
- Think how they map to UI:
  - A small stats panel at top of ItemsPage.
  - Tabs or buttons to switch between “All”, “Overdue”, “Done” views.

In notes:
- Sketch how you want ItemsPage to look with filters/stats.

### 2. Do (60–90 minutes)

1. **Add stats API helper (`itemsApi.js`):**

   ```jsx
   export async function fetchStats(token) {
     const res = await fetch(`${BASE_URL}/items/stats`, {
       headers: { Authorization: `Bearer ${token}` },
     });
     const data = await res.json().catch(() => ({}));
     if (!res.ok) throw new Error(data.error || `Failed to fetch stats (${res.status})`);
     return data; // e.g. { total, statusCounts: { todo: X, ... } }
   }
   ```

2. **In `ItemsPage`, load stats alongside items:**

   - Add state:

     ```jsx
     const [stats, setStats] = useState(null);
     ```

   - Update `useEffect` to load both:

     ```jsx
     import { fetchItems, fetchStats } from "../services/itemsApi";

     useEffect(() => {
       async function load() {
         try {
           setLoading(true);
           setError(null);
           const [itemsData, statsData] = await Promise.all([
             fetchItems(token),
             fetchStats(token),
           ]);
           setItems(itemsData);
           setStats(statsData);
         } catch (err) {
           setError(err.message);
         } finally {
           setLoading(false);
         }
       }
       load();
     }, [token]);
     ```

   - Show stats above list:

     ```jsx
     {stats && (
       <p>
         Total: {stats.total} | Todo: {stats.statusCounts?.["todo"] || 0} | In Progress:{" "}
         {stats.statusCounts?.["in-progress"] || 0} | Done:{" "}
         {stats.statusCounts?.["done"] || 0}
       </p>
     )}
     ```

   - After create/update/delete, call `fetchStats` again to keep them in sync.

3. **Add simple client-side filters:**

   - State:

     ```jsx
     const [filterStatus, setFilterStatus] = useState("all");
     ```

   - Controls:

     ```jsx
     <div style={{ marginBottom: "0.5rem" }}>
       <button onClick={() => setFilterStatus("all")}>All</button>
       <button onClick={() => setFilterStatus("todo")}>Todo</button>
       <button onClick={() => setFilterStatus("in-progress")}>In Progress</button>
       <button onClick={() => setFilterStatus("done")}>Done</button>
     </div>
     ```

   - Derived filtered items:

     ```jsx
     const visibleItems =
       filterStatus === "all"
         ? items
         : items.filter((item) => item.status === filterStatus);
     ```

   - Render `visibleItems` instead of `items`.

### 3. Reflect (10–15 minutes)

- How do stats and filters make this feel more like a real product vs a basic CRUD list?
- Did you run into any edge cases when stats didn’t match items (e.g. forgot to refresh stats on change)?

### 4. Stretch (optional, 20–30 minutes)

- Use the `/api/items/overdue` endpoint (if you built it) to show a separate “Overdue” view.
- Add a progress indicator (e.g., percentage completed) based on stats.

---

## Day 6 – UI Polish, Responsiveness & Small UX Enhancements

**Goals:**
- Make the app visually and ergonomically pleasant.
- Add small UX touches that make a big difference.

### 1. Learn (20–30 minutes)

Concepts:
- Layout & responsiveness:
  - Reasonable spacing, alignment.
  - Mobile vs desktop considerations.
- Visual hierarchy:
  - Headings, button styles, card-like item rows.

Browse:
- A couple of simple dashboard UIs (Dribbble/Behance or existing apps) for inspiration.

In notes:
- List 3 concrete UI improvements you want:
  - e.g., better button styles, cards for items, mobile layout.

### 2. Do (60–90 minutes)

1. **Global styles:**
   - Create `src/App.css` or use CSS modules.
   - Set base font, background color, body margins.
   - Apply consistent spacing.

2. **Style Navbar & pages:**
   - Make navbar sticky or fixed at top if you like.
   - Style links with hover/active states.

3. **Style Items list:**
   - Instead of bare `<li>`, use a card-like container:
     - border, padding, flex layout for text + actions.
   - Add distinct styling for “done” items (muted color).

4. **Form & button improvements:**
   - Add margin/padding to inputs.
   - Use consistent button styling for primary actions (Add, Save) vs secondary (Cancel, Delete).

5. **Responsiveness:**
   - Use simple media queries or flexible layout (e.g., items stacked on small screens).
   - Check app on a narrow viewport (DevTools device toolbar).

### 3. Reflect (10–15 minutes)

- Which visual change made the biggest improvement in perceived quality?
- If someone saw only a screenshot, would they guess it was a student project or a small real product?

### 4. Stretch (optional, 20–30 minutes)

- Add light/dark mode toggle (class on root + CSS).
- Add a small “Loading…” overlay or spinner during actions (especially login and initial items fetch).

---

## Day 7 – Final Review, README & Deployment Prep (Optional)

**Goals:**
- Review the entire full-stack app end-to-end.
- Document your project clearly.
- Optionally deploy (or at least outline deployment steps).

### 1. Review (30–45 minutes)

Walk through:

- Backend:
  - Does `/api/auth/register` and `/api/auth/login` work correctly?
  - Are `/api/items` routes scoped to user and validated?
  - Any errors in logs when you perform normal actions?

- Frontend:
  - Can you:
    - Register/login (if implemented).
    - See your items after login.
    - Create/update/delete items.
    - See stats/filters working.
  - Does navigation (`/`, `/login`, `/items`) work as expected with protected routes?

In notes:
- Write a short **“demo script”**:
  - Steps you’d walk someone through to show your app.

### 2. Do – README & Screenshots (60–90 minutes)

1. **Write a solid README for your capstone (frontend repo, or root of combined repo):**

   Include:
   - Project name & one-sentence description.
   - Tech stack (React, Express, MongoDB, JWT).
   - Features:
     - Bullet list (auth, CRUD items, stats, filters).
   - Setup instructions:
     - Backend:
       - `npm install`, `.env` variables, `npm run dev`.
     - Frontend:
       - `npm install`, set `VITE_API_URL`, `npm run dev`.
   - Basic usage:
     - “Register login → go to Items → create tasks…”
   - Screenshots (optional but great):
     - Login page.
     - Items page with some data.

2. **Consider deployment (outline steps even if you don’t execute yet):**

   - Backend:
     - Platforms: Render, Railway, Fly.io, etc.
     - Needs env vars (`MONGODB_URI`, `JWT_SECRET`).
   - Frontend:
     - Platforms: Netlify, Vercel, etc.
     - Needs `VITE_API_URL` set to the deployed backend URL.

   Even just writing the steps gives you a roadmap.

3. **(Optional) Actually deploy:**
   - Deploy backend first, confirm API works.
   - Then deploy frontend pointing to that API.
   - Test the app live.

### 3. Self-Assessment (20–30 minutes)

Mark ✅ / ❌:

- Full-stack flow:
  - [ ] I can explain how a login request goes from frontend → backend → DB → frontend.
  - [ ] I can explain how a new item creation is handled end-to-end.
  - [ ] I can troubleshoot an error by looking at both frontend console and backend logs.

- Frontend:
  - [ ] I can manage auth state and protected routes.
  - [ ] I built reusable components and API helpers instead of duplicating code.
  - [ ] I handle loading and error states in the UI.

- Project:
  - [ ] My app solves a clear problem (even if small).
  - [ ] The README is clear enough for someone else to run it.
  - [ ] I can demo it confidently.

Write 3 bullet points:
- 2 things you’re **most proud of** in this project.
- 1 thing you’d improve if you had another week.

### 4. Reflect (15–20 minutes)

Answer in your notes:

- What aspects of full-stack development now feel “natural” to you?
- What still feels like magic or shaky (e.g. deployment, advanced security, state management patterns)?
- If you were to start the same project over, what would you do differently in design or planning?

### 5. Stretch (optional, 30–45 minutes)

- Record a short **screen capture demo** (no need to publish; it’s for you) walking through:
  - Logging in.
  - Creating items.
  - Using filters/stats.
- Start a small “Next Steps” list:
  - E.g. add tests, better error boundaries, more complex relationships, etc.

---

You now have a complete 12‑week path from HTML/CSS basics to a deployed, authenticated full‑stack app.  
If you’d like, I can next help you:

- Turn this capstone into a stronger portfolio piece (writeup, small blog post, etc.), or  
- Design a follow-up learning track (TypeScript, testing, performance, or another stack like Next.js).
