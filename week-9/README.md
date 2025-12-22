Here’s your **Week 9 (Days 1–7) plan**, focused on **authentication and user accounts** for your Express + MongoDB backend.

Assume ~2–3 hours/day.  
Each day: **Learn → Do → Reflect → Stretch**.  

By the end of Week 9 you should be able to:

- Explain **authentication vs authorization**.  
- Create a **User model** with **hashed passwords** (bcrypt).  
- Implement **register** and **login** routes that return **JWTs**.  
- Protect routes with **auth middleware** so only logged-in users can access them.  

You’ll work on top of your Week 8 API (Express + Mongo + Todos).

---

## Day 1 – Auth Concepts & Designing the User Model

**Goals:**
- Understand auth fundamentals.
- Design a `User` model for MongoDB.
- Decide which fields you need for now.

### 1. Learn (40–60 minutes)

Core concepts:

- **Authentication vs authorization**:
  - Authentication: “Who are you?” (login).
  - Authorization: “What are you allowed to do?” (e.g., access certain todos).
- Common patterns:
  - **Session + cookies** (server stores session).
  - **JWT tokens** (client holds token, sends on each request).
- For APIs + SPA frontends, JWT is common and good enough to learn.

Read/Watch (pick 1–2):

- Short article: “Authentication vs Authorization (beginner friendly)”.
- JWT intro: jwt.io “Introduction”.
- Skim: bcrypt (npm `bcrypt` or `bcryptjs`) docs to see hashing idea.

In your notes, answer:

- In your own words: difference between authentication and authorization.
- What’s the risk of storing plain-text passwords?
- What is a JWT in one or two sentences?

### 2. Do (60–90 minutes)

In your `week8-api` project (copy as `week9-auth-api` if you want to keep the old one untouched):

1. **Install dependencies:**

   ```bash
   npm install bcrypt jsonwebtoken
   ```

   - `bcrypt` – password hashing.
   - `jsonwebtoken` – creating/verifying JWTs.

2. **Design your User model:**

   Decide on fields:
   - `email` (String, required, unique, lowercase).
   - `passwordHash` (String, required).
   - `createdAt` / `updatedAt` (timestamps).
   - (Optionally: `name`).

   Write down an example user document (no real passwords):
   ```json
   {
     "email": "test@example.com",
     "passwordHash": "...hashed...",
     "createdAt": "2025-01-15T...Z"
   }
   ```

### 3. Reflect (10–15 minutes)

- What minimal fields do you truly need for a user account?
- How would you explain to a non-technical person why passwords must be hashed?

### 4. Stretch (optional, 20–30 minutes)

- Sketch what future fields might be: `role` (user/admin), `profile` info, etc.
- Think through: what happens if two users register with same email? How do you prevent it?

---

## Day 2 – Implementing the User Model & Register Route (Password Hashing)

**Goals:**
- Create the `User` Mongoose model.
- Implement a **register** route that:
  - Validates input.
  - Hashes password.
  - Saves user to DB.

### 1. Learn (40–60 minutes)

Concepts:

- **Password hashing with bcrypt**:
  - `bcrypt.hash(password, saltRounds)` → `passwordHash`.
  - `bcrypt.compare(plain, hash)` → `true/false`.
- `unique` index in Mongoose:
  - `unique: true` on email helps, but you still need to handle duplicate errors.

Read:

- Mongoose docs: “Unique indexes” (skim).
- `bcrypt` npm page: basic usage examples.

In your notes:

- Example pseudo-code for register:
  1. Check email/password presence.
  2. Check if email already exists.
  3. Hash password.
  4. Save user.
  5. Return success response.

### 2. Do (90–120 minutes)

1. **Create `models/User.js`:**

   ```js
   const mongoose = require("mongoose");

   const userSchema = new mongoose.Schema(
     {
       email: {
         type: String,
         required: true,
         unique: true,
         lowercase: true,
         trim: true,
       },
       passwordHash: {
         type: String,
         required: true,
       },
     },
     { timestamps: true }
   );

   const User = mongoose.model("User", userSchema);

   module.exports = User;
   ```

2. **Create `routes/auth.js` (router for auth):**

   ```js
   const express = require("express");
   const bcrypt = require("bcrypt");
   const User = require("../models/User");

   const router = express.Router();

   // POST /api/auth/register
   router.post("/register", async (req, res) => {
     try {
       const { email, password } = req.body;

       if (!email || !password) {
         return res.status(400).json({ error: "Email and password are required" });
       }

       if (password.length < 6) {
         return res
           .status(400)
           .json({ error: "Password must be at least 6 characters long" });
       }

       const existingUser = await User.findOne({ email });
       if (existingUser) {
         return res.status(409).json({ error: "Email already in use" });
       }

       const saltRounds = 10;
       const passwordHash = await bcrypt.hash(password, saltRounds);

       const user = await User.create({ email, passwordHash });

       res.status(201).json({
         id: user._id,
         email: user.email,
         createdAt: user.createdAt,
       });
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Registration failed" });
     }
   });

   module.exports = router;
   ```

3. **Wire router in your main `index.js`:**

   ```js
   const authRouter = require("./routes/auth");
   app.use("/api/auth", authRouter);
   ```

4. **Test with Postman/Insomnia:**
   - `POST http://localhost:3000/api/auth/register`  
     Body (JSON):
     ```json
     { "email": "test@example.com", "password": "secret123" }
     ```
   - Check DB to see new user created.

### 3. Reflect (10–15 minutes)

- Why do you never store the raw password in the DB?
- What response do you send back after registration, and why don’t you send the password or hash?

### 4. Stretch (optional, 20–30 minutes)

- Add basic email format validation (e.g., using a simple regex or more advanced library later).
- Consider handling MongoDB duplicate key errors:
  - If error code 11000, respond with 409 and `Email already in use`.

---

## Day 3 – Login Route & Issuing JWTs

**Goals:**
- Implement **login** with:
  - Email/password check.
  - Password comparison using bcrypt.
  - JWT generation on success.

### 1. Learn (40–60 minutes)

Concepts:

- JWT structure: header + payload + signature.
- Typical contents of JWT payload:
  - `userId`, `email`, maybe `role`.
- `jsonwebtoken` usage:
  - `jwt.sign(payload, secret, options)`
  - `jwt.verify(token, secret)`

Read:

- `jsonwebtoken` npm page.
- jwt.io – paste a sample token to see structure.

In your notes:

- What information will you store in the JWT payload? (Keep it small, no secrets.)
- What is your JWT secret, and where should it be stored (env variable)?

### 2. Do (90–120 minutes)

1. **Set JWT secret in `.env`:**

   ```env
   JWT_SECRET=some-long-random-string
   JWT_EXPIRES_IN=7d
   ```

2. **Update `routes/auth.js` – add `/login`:**

   ```js
   const jwt = require("jsonwebtoken");

   // POST /api/auth/login
   router.post("/login", async (req, res) => {
     try {
       const { email, password } = req.body;
       if (!email || !password) {
         return res.status(400).json({ error: "Email and password are required" });
       }

       const user = await User.findOne({ email });
       if (!user) {
         return res.status(401).json({ error: "Invalid email or password" });
       }

       const passwordMatch = await bcrypt.compare(password, user.passwordHash);
       if (!passwordMatch) {
         return res.status(401).json({ error: "Invalid email or password" });
       }

       const payload = { userId: user._id, email: user.email };
       const token = jwt.sign(payload, process.env.JWT_SECRET, {
         expiresIn: process.env.JWT_EXPIRES_IN || "7d",
       });

       res.json({
         token,
         user: {
           id: user._id,
           email: user.email,
         },
       });
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Login failed" });
     }
   });
   ```

3. **Test via Postman:**
   - Register a user if needed.
   - `POST /api/auth/login` with correct email/password → expect JSON with `token` and user info.
   - Try wrong email or password → expect 401.

### 3. Reflect (10–15 minutes)

- What happens if someone steals a JWT? Why is its **expiration** important?
- Why do you return the token to the client instead of storing it server-side?

### 4. Stretch (optional, 20–30 minutes)

- Add `rememberMe` concept (different expiry if `rememberMe` is true).
- Return a `tokenType: "Bearer"` field for clarity.

---

## Day 4 – Auth Middleware: Protecting Routes with JWT

**Goals:**
- Build middleware that:
  - Reads JWT from `Authorization` header.
  - Verifies it and attaches user info to `req`.
- Use the middleware to **protect Todo routes** so only logged-in users can access them.

### 1. Learn (40–60 minutes)

Concepts:

- Middleware in Express:
  - Function `(req, res, next)` that runs before route handlers.
- Common pattern for JWT:
  - Header: `Authorization: Bearer <token>`.
  - Middleware decodes token and sets `req.user`.

Read:

- Express docs: “Using middleware”.
- Skim an example of JWT auth middleware (but write your own code).

In your notes:

- Pseudocode for `authMiddleware`:
  1. Read `Authorization` header.
  2. If missing or malformed, return 401.
  3. Extract token string.
  4. Verify with `jwt.verify`.
  5. Attach decoded payload to `req.user`.
  6. Call `next()`.

### 2. Do (90–120 minutes)

1. **Create `middleware/auth.js`:**

   ```js
   const jwt = require("jsonwebtoken");

   function authMiddleware(req, res, next) {
     const authHeader = req.headers.authorization;

     if (!authHeader || !authHeader.startsWith("Bearer ")) {
       return res.status(401).json({ error: "Authorization token missing" });
     }

     const token = authHeader.split(" ")[1];

     try {
       const decoded = jwt.verify(token, process.env.JWT_SECRET);
       req.user = decoded; // { userId, email, iat, exp }
       next();
     } catch (err) {
       console.error("JWT verification failed:", err.message);
       return res.status(401).json({ error: "Invalid or expired token" });
     }
   }

   module.exports = authMiddleware;
   ```

2. **Update your Todo model to have `user` field:**

   In `models/Todo.js`:

   ```js
   user: {
     type: mongoose.Schema.Types.ObjectId,
     ref: "User",
     required: true,
   },
   ```

   (Add this field and re-run your server; you may need to adjust code accordingly.)

3. **Protect Todo routes & associate todos with current user:**

   In `index.js` or `routes/todos.js`:

   ```js
   const auth = require("./middleware/auth");
   const Todo = require("./models/Todo");

   // All todo routes after app.use(auth) or individually attach middleware
   app.get("/api/todos", auth, async (req, res) => {
     try {
       const todos = await Todo.find({ user: req.user.userId }).sort({
         createdAt: -1,
       });
       res.json(todos);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to fetch todos" });
     }
   });

   app.post("/api/todos", auth, async (req, res) => {
     try {
       const { text } = req.body;
       const todo = await Todo.create({
         text,
         user: req.user.userId,
       });
       res.status(201).json(todo);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to create todo" });
     }
   });

   // ...and similar for PUT/DELETE: ensure you only modify todos for current user
   ```

4. **Update update/delete routes to check owner:**

   Example for DELETE:

   ```js
   app.delete("/api/todos/:id", auth, async (req, res) => {
     const { id } = req.params;
     const userId = req.user.userId;

     try {
       const todo = await Todo.findOneAndDelete({ _id: id, user: userId });
       if (!todo) {
         return res.status(404).json({ error: "Todo not found" });
       }
       res.json(todo);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to delete todo" });
     }
   });
   ```

### 3. Reflect (10–15 minutes)

- Why do you filter by `{ user: req.user.userId }` in queries?
- What would happen if you didn’t check user ownership?

### 4. Stretch (optional, 20–30 minutes)

- Add a `/api/auth/me` route using `authMiddleware` that returns the current user’s basic info (`id`, `email`).
- Consider using `router.use(auth)` in your todos router so all routes are protected without repeating `auth`.

---

## Day 5 – Frontend Auth: Logging In & Storing the Token (Conceptual + Small Implementation)

**Goals:**
- Sketch how your React app will:
  - Allow users to register/login.
  - Store JWT (e.g., in memory or `localStorage`).
  - Attach token to API requests.
- Implement a simple React login form and test end-to-end.

### 1. Learn (40–60 minutes)

Concepts:

- Where to store JWT on frontend:
  - `localStorage` (simple, but XSS risk if site compromised).
  - `sessionStorage` or in-memory.
  - For now, use `localStorage` for simplicity, but be aware of risks.
- Attaching token:
  - Add `Authorization: Bearer <token>` header on each API call.

Read:

- A beginner-friendly article: “JWT authentication in React (frontend side)”.
- Skim React docs: Context (you might use it for global auth later).

In your notes:

- Draw a flow:
  1. User submits login form.
  2. React sends POST /login.
  3. Backend returns token + user data.
  4. React stores token and user in state/storage.
  5. React includes token in future `/api/todos` requests.

### 2. Do (90–120 minutes)

In your React project:

1. **Create a simple `AuthContext` (optional but helpful):**

   If that feels like too much now, you can just keep token in a parent `App` state, but I’ll outline a context-based approach (you can simplify as needed).

   - `src/AuthContext.jsx`:

     ```jsx
     import { createContext, useContext, useState, useEffect } from "react";

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

2. **Wrap your app with `AuthProvider` in `main.jsx`:**

   ```jsx
   import { AuthProvider } from "./AuthContext";

   ReactDOM.createRoot(document.getElementById("root")).render(
     <React.StrictMode>
       <AuthProvider>
         <App />
       </AuthProvider>
     </React.StrictMode>
   );
   ```

3. **Create a `LoginForm.jsx`:**

   ```jsx
   import { useState } from "react";
   import { useAuth } from "./AuthContext";

   function LoginForm() {
     const [email, setEmail] = useState("");
     const [password, setPassword] = useState("");
     const [error, setError] = useState(null);
     const [loading, setLoading] = useState(false);
     const auth = useAuth();

     async function handleSubmit(e) {
       e.preventDefault();
       setError(null);
       setLoading(true);

       try {
         const res = await fetch("http://localhost:3000/api/auth/login", {
           method: "POST",
           headers: { "Content-Type": "application/json" },
           body: JSON.stringify({ email, password }),
         });

         if (!res.ok) {
           const data = await res.json().catch(() => ({}));
           throw new Error(data.error || `Login failed with status ${res.status}`);
         }

         const data = await res.json();
         auth.login(data.token, data.user);
       } catch (err) {
         setError(err.message);
       } finally {
         setLoading(false);
       }
     }

     return (
       <form onSubmit={handleSubmit}>
         <h2>Login</h2>
         {error && <p style={{ color: "red" }}>{error}</p>}
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
     );
   }

   export default LoginForm;
   ```

4. **Use `LoginForm` & protect `TodoApp`:**

   In `App.jsx`:

   ```jsx
   import { useAuth } from "./AuthContext";
   import LoginForm from "./LoginForm";
   import TodoApp from "./TodoApp";

   function App() {
     const { user, logout } = useAuth();

     return (
       <div>
         {user ? (
           <>
             <p>Logged in as {user.email}</p>
             <button onClick={logout}>Logout</button>
             <TodoApp />
           </>
         ) : (
           <LoginForm />
         )}
       </div>
     );
   }

   export default App;
   ```

5. **Update your Todo API calls to include token:**

   In `TodoApp.jsx`, use `useAuth()` and add header:

   ```jsx
   const { token } = useAuth();

   const res = await fetch("http://localhost:3000/api/todos", {
     headers: { Authorization: `Bearer ${token}` },
   });
   ```

   - Similarly add `Authorization` header to POST/PUT/DELETE.

### 3. Reflect (10–15 minutes)

- How does the app’s behavior change when logged out vs logged in?
- What risks do you see with storing the JWT in `localStorage`? (You don’t need a perfect answer; awareness is key.)

### 4. Stretch (optional, 20–30 minutes)

- Add a very simple **register form** in React and wire it up to `/api/auth/register`.
- Show a small “You must be logged in to manage todos” message instead of just a blank screen.

---

## Day 6 – Authorization & Ownership: Locking Todos to Their Owners

**Goals:**
- Ensure users can only see/modify **their own** todos.
- Review your routes for possible security holes.

### 1. Learn (30–45 minutes)

Concepts:

- **Authorization** on resource level:
  - User should only access data that belongs to them.
- Patterns:
  - Filter queries by `user: req.user.userId`.
  - For detail routes (PUT/DELETE), use `findOne` with both `_id` and `user`.

In your notes:

- For each todo route (GET all, GET by id, PUT, DELETE), describe how you ensure ownership is enforced.

### 2. Do (60–90 minutes)

1. **Review & tighten backend routes:**

   - Confirm every todo route:
     - Uses `authMiddleware`.
     - Filters queries by `{ user: req.user.userId }`.

   - For GET all:
     ```js
     Todo.find({ user: req.user.userId })
     ```

   - For single fetch/update/delete:
     ```js
     Todo.findOne({ _id: id, user: req.user.userId })
     // or findOneAndUpdate, findOneAndDelete
     ```

2. **Test with two users:**

   - In Postman:
     - Register user A (`a@example.com`), login, copy token A.
     - Register user B (`b@example.com`), login, copy token B.
   - With token A:
     - Create some todos.
   - With token B:
     - Try `GET /api/todos` → should only see B’s todos (maybe none).
     - Try hitting a todo id that belongs to A → expect 404 (not found).

### 3. Reflect (10–15 minutes)

- Why is returning 404 (instead of “forbidden”) sometimes used when resource doesn’t belong to user?
- What would be the risk if you only checked `_id` without `user`?

### 4. Stretch (optional, 20–30 minutes)

- Add a `role` field to User (default `"user"`), and add an admin-only route (e.g., `/api/admin/all-todos`) that lists all todos only if `req.user.role === "admin"`.
- Think through how you’d prevent a normal user from simply editing their JWT payload to claim they’re an admin (answer: signature and server-side verification).

---

## Day 7 – Consolidation & Security Review

**Goals:**
- Review your end-to-end auth flow.
- Identify security and UX improvements.
- Solidify mental model for future full-stack projects.

### 1. Review (30–45 minutes)

Revisit:

- Backend:
  - `User` model.
  - `auth` routes (`/register`, `/login`, maybe `/me`).
  - `authMiddleware`.
  - Protected `todos` routes (ownership checks).
- Frontend:
  - `AuthContext` (or equivalent state).
  - `LoginForm` + token storage.
  - Todo API calls with `Authorization` header.

In your notes, write:

- A bullet-point flow of:
  1. New user signs up.
  2. User logs in.
  3. User creates a todo.
  4. User refreshes the browser and still sees their todos.

### 2. Do – Cleanup & Mini Audit (60–90 minutes)

1. **Backend cleanup:**
   - Ensure no route returns password or `passwordHash`.
   - Confirm error messages don’t leak sensitive internals (e.g., full stack traces).
   - Check responses are consistent: `{ error: "message" }` or similar.

2. **Frontend cleanup:**
   - Ensure you handle:
     - Login failures gracefully (`Invalid email or password`).
     - Auth-expired errors (401) – maybe log out or show “Session expired” message.

3. **Manual tests:**
   - Try invalid email/password combos.
   - Delete JWT from `localStorage` and reload app – see if it correctly shows login screen.
   - Kill backend and see what the frontend does (should show error messages, not crash).

### 3. Self-Assessment Checklist (20–30 minutes)

Mark ✅ / ❌ and note any ❌ to revisit:

- Auth concepts:
  - [ ] I can explain authentication vs authorization.
  - [ ] I know why we hash passwords.
  - [ ] I understand the basic idea of JWTs (payload + signature + expiry).

- Backend auth:
  - [ ] I can implement a register route with password hashing.
  - [ ] I can implement a login route that returns a JWT.
  - [ ] I can write middleware that verifies a token and sets `req.user`.
  - [ ] I can restrict access to resources by user ownership.

- Frontend auth:
  - [ ] I can build a login form that talks to my API.
  - [ ] I can store a token and attach it to future API calls.
  - [ ] I can conditionally render UI based on auth state.

Write a short paragraph:

- What part of auth felt the trickiest this week (bcrypt, JWTs, middleware, frontend integration)?
- What do you want to practice again or refactor before building a bigger project?

### 4. Reflect (15–20 minutes)

Answer in your notes:

- If you were starting a **Task Manager** or **Habit Tracker** app:
  - How would you structure:
    - `User` model?
    - `Task` or `Habit` model (with `user` relationship)?
    - Auth routes and protected routes?
- What would be your main security concerns and how would you address them at a basic level?

### 5. Stretch (optional, 30–45 minutes)

- Add **password change** endpoint:
  - Requires auth.
  - Takes `currentPassword` + `newPassword`.
  - Verifies current password with `bcrypt.compare`.
  - Saves new hash.
- Or add **“forgot password”** mock flow (even just conceptual or with a placeholder token in DB).

---

If you want next, I can:

- Create a **Week 10 plan** focused on **polishing your full-stack app** (routing on frontend, better UX, maybe basic role-based access), or  
- Help you plan a concrete full-stack project (feature list, data models, API endpoints) that uses your new auth system end-to-end.
