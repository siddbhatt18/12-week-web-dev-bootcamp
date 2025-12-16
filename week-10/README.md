**Week 10 Theme:** Authentication & Authorization (JWT) – secure your API and connect it to React.  
Assume ~2 hours/day. You’ll work in both your **backend (Notes API)** and **frontend (React notes app)**.

By the end of the week you’ll have:

- User registration & login (JWT-based).
- Protected notes routes on the backend.
- React app that can log in, store a token, and access protected data.

---

## Day 1 – Auth Basics & User Model

**Objectives:**
- Understand authentication vs authorization.
- Add a `User` model to your backend.

### 1. Concept (20–30 min)

In `notes-day1.txt`, capture short notes on:

- **Authentication**: Proving who you are (login).
- **Authorization**: What you’re allowed to access (permissions).
- **JWT (JSON Web Token)** basics:
  - Signed token that encodes data (e.g., `userId`).
  - Sent with each request (usually in `Authorization: Bearer <token>` header).
- Passwords:
  - Never store plain text.
  - Store **hashed** (e.g., with `bcrypt`).

### 2. Install deps & create User model (60–70 min)

In your **Notes API** project:

```bash
cd notes-api
npm install bcryptjs jsonwebtoken
```

Create `models/User.js`:

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

Add a placeholder JWT secret to `.env`:

```env
JWT_SECRET=your_super_secret_jwt_key_here
JWT_EXPIRES_IN=7d
```

(Use a long random string in a real app.)

Ensure `index.js` still connects to MongoDB and runs.

### 3. Reflection (5–10 min)

In `notes-day1.txt`:

- Why store `passwordHash` instead of `password`?
- What secrets did you just add to `.env`?

---

## Day 2 – Registration Route (`/auth/register`)

**Objectives:**
- Implement a route to create new users.
- Hash passwords with bcrypt.

### 1. Concept (20–25 min)

Learn:

- Bcrypt basics:
  - `bcrypt.hash(password, saltRounds)`
  - `bcrypt.compare(plain, hash)`
- Standard registration flow:
  - Validate email & password.
  - Check if user already exists.
  - Hash password.
  - Save user.
  - (Optionally) return a token or ask user to log in separately.

### 2. Implement `/auth/register` (60–70 min)

Create `routes/auth.js`:

```js
const express = require("express");
const bcrypt = require("bcryptjs");
const jwt = require("jsonwebtoken");
const User = require("../models/User");

const router = express.Router();

router.post("/register", async (req, res) => {
  try {
    const { email, password } = req.body;

    if (!email || typeof email !== "string") {
      return res.status(400).json({ error: "Valid email is required" });
    }
    if (!password || typeof password !== "string" || password.length < 6) {
      return res
        .status(400)
        .json({ error: "Password must be at least 6 characters long" });
    }

    const existing = await User.findOne({ email });
    if (existing) {
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
    console.error("Error in /auth/register:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});

module.exports = router;
```

Wire it in `index.js`:

```js
const authRouter = require("./routes/auth");

app.use("/auth", authRouter);
```

Test with Postman:

- `POST http://localhost:4000/auth/register`
  - Body (JSON):

    ```json
    { "email": "test@example.com", "password": "secret123" }
    ```

- Check:
  - You get a `201` and user info (without password).
  - The user appears in `users` collection in MongoDB.

### 3. Reflection (5–10 min)

In `notes-day2.txt`:

- What checks did you do before creating a new user?
- Why do we return only `id` and `email` instead of full user document with passwordHash?

---

## Day 3 – Login Route (`/auth/login`) & JWT Issuing

**Objectives:**
- Implement login that checks credentials.
- Issue a JWT on successful login.

### 1. Concept (20–25 min)

- Login flow:
  - Find user by email.
  - Compare provided password with stored hash.
  - If valid, sign a JWT:

    ```js
    const token = jwt.sign(
      { userId: user._id },
      process.env.JWT_SECRET,
      { expiresIn: process.env.JWT_EXPIRES_IN || "7d" }
    );
    ```

- Return token to client. Client will store it (localStorage, memory, etc.).

### 2. Implement `/auth/login` (60–70 min)

In `routes/auth.js`, add:

```js
router.post("/login", async (req, res) => {
  try {
    const { email, password } = req.body;

    if (!email || typeof email !== "string" || !password) {
      return res.status(400).json({ error: "Email and password are required" });
    }

    const user = await User.findOne({ email });
    if (!user) {
      // To avoid leaking which emails exist, use generic message
      return res.status(401).json({ error: "Invalid email or password" });
    }

    const passwordMatch = await bcrypt.compare(password, user.passwordHash);
    if (!passwordMatch) {
      return res.status(401).json({ error: "Invalid email or password" });
    }

    const token = jwt.sign(
      { userId: user._id },
      process.env.JWT_SECRET,
      { expiresIn: process.env.JWT_EXPIRES_IN || "7d" }
    );

    res.json({
      token,
      user: {
        id: user._id,
        email: user.email,
      },
    });
  } catch (err) {
    console.error("Error in /auth/login:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});
```

Test with Postman:

- `POST /auth/login` with valid credentials:
  - Expect `200` with `token` and `user`.
- Wrong password:
  - Expect `401` with error.

### 3. Reflection (5–10 min)

In `notes-day3.txt`:

- What payload did you put inside the JWT?
- Why return a generic “Invalid email or password” instead of a more specific error?

---

## Day 4 – Auth Middleware & Protecting Notes Routes

**Objectives:**
- Create a middleware to verify JWT and attach user to `req`.
- Protect `/notes` routes so only logged-in users can access their own notes.

### 1. Concept (20–25 min)

- Token extraction:
  - Typically from `Authorization: Bearer <token>`.
- JWT verification:

  ```js
  const decoded = jwt.verify(token, process.env.JWT_SECRET);
  req.user = { id: decoded.userId };
  next();
  ```

- Error cases:
  - Missing header.
  - Malformed header.
  - Invalid/expired token.

### 2. Implement `authMiddleware` (60–70 min)

Create `middleware/auth.js`:

```js
const jwt = require("jsonwebtoken");

function authRequired(req, res, next) {
  const authHeader = req.headers.authorization || "";

  const [scheme, token] = authHeader.split(" ");

  if (scheme !== "Bearer" || !token) {
    return res.status(401).json({ error: "Authorization header missing or invalid" });
  }

  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = { id: decoded.userId };
    next();
  } catch (err) {
    console.error("JWT verification error:", err);
    return res.status(401).json({ error: "Invalid or expired token" });
  }
}

module.exports = authRequired;
```

Update `models/Note.js` to associate notes with a user:

```js
user: {
  type: mongoose.Schema.Types.ObjectId,
  ref: "User",
  required: true,
},
```

Now update `routes/notes.js`:

At top:

```js
const authRequired = require("../middleware/auth");
```

Wrap routes with `authRequired` and use `req.user.id`:

- Example for `POST /notes`:

```js
router.post("/", authRequired, async (req, res) => {
  try {
    const { title, content, pinned } = req.body;

    if (!title || typeof title !== "string") {
      return res
        .status(400)
        .json({ error: "Title is required and must be a string" });
    }

    const note = await Note.create({
      title,
      content,
      pinned,
      user: req.user.id,
    });

    res.status(201).json(note);
  } catch (err) {
    console.error("Error creating note:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});
```

For `GET /notes`:

```js
router.get("/", authRequired, async (req, res) => {
  try {
    const { search, pinned } = req.query;
    const query = { user: req.user.id };

    if (search) {
      query.title = { $regex: search, $options: "i" };
    }

    if (pinned === "true") {
      query.pinned = true;
    } else if (pinned === "false") {
      query.pinned = false;
    }

    const notes = await Note.find(query).sort({ createdAt: -1 });
    res.json(notes);
  } catch (err) {
    console.error("Error fetching notes:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});
```

Similarly update `GET /notes/:id`, `PUT /notes/:id`, `DELETE /notes/:id` to:

- Use `authRequired`.
- Ensure note belongs to `req.user.id` (e.g., `Note.findOne({ _id: id, user: req.user.id })`).

Example for find-one:

```js
const note = await Note.findOne({ _id: id, user: req.user.id });
```

### 3. Test with Postman (15–20 min)

- First, `POST /auth/login` and copy token.
- For `GET /notes`, add header:

  ```
  Authorization: Bearer <token>
  ```

- Confirm:
  - Without header → `401`.
  - With token → works.
- Create notes and see they are tied to the authenticated user.

### 4. Reflection (5–10 min)

In `notes-day4.txt`:

- How does the middleware know which user is making the request?
- What happens if a user tries to access a note that belongs to someone else?

---

## Day 5 – Frontend: Auth Context & Login Form UI

**Objectives:**
- Add auth API helpers to your React app.
- Create a login/register page and store token in React state (and localStorage).

### 1. Backend helper: CORS (if needed) (10–15 min)

If your frontend is on another port (e.g., 5173) and you see CORS errors, install and enable CORS on the backend:

```bash
npm install cors
```

In `index.js`:

```js
const cors = require("cors");

app.use(cors({
  origin: "http://localhost:5173", // adjust if needed
  credentials: false,
}));
```

### 2. Frontend auth API helpers (20–25 min)

In your React app `api.js`, add:

```js
export function registerUser(credentials) {
  return request("/auth/register", {
    method: "POST",
    body: JSON.stringify(credentials),
  });
}

export function loginUser(credentials) {
  return request("/auth/login", {
    method: "POST",
    body: JSON.stringify(credentials),
  });
}
```

Update `request` function to accept optional `token` (if you wish), or you’ll handle Authorization header in a custom wrapper later. For now we’ll add the header where needed.

### 3. AuthContext for global auth state (40–50 min)

Create `src/AuthContext.jsx`:

```jsx
import { createContext, useContext, useEffect, useState } from "react";
import { loginUser } from "./api";

const AuthContext = createContext(null);

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null); // { id, email }
  const [token, setToken] = useState(null);

  useEffect(() => {
    const saved = localStorage.getItem("auth");
    if (saved) {
      try {
        const parsed = JSON.parse(saved);
        setUser(parsed.user);
        setToken(parsed.token);
      } catch {
        // ignore
      }
    }
  }, []);

  function saveAuth(newUser, newToken) {
    setUser(newUser);
    setToken(newToken);
    localStorage.setItem("auth", JSON.stringify({ user: newUser, token: newToken }));
  }

  function clearAuth() {
    setUser(null);
    setToken(null);
    localStorage.removeItem("auth");
  }

  async function login(email, password) {
    const data = await loginUser({ email, password });
    saveAuth(data.user, data.token);
  }

  const value = {
    user,
    token,
    login,
    logout: clearAuth,
    isAuthenticated: !!user,
  };

  return <AuthContext.Provider value={value}>{children}</AuthContext.Provider>;
}

export function useAuth() {
  return useContext(AuthContext);
}
```

Wrap your app in `AuthProvider` in `main.jsx`:

```jsx
import { AuthProvider } from "./AuthContext";

ReactDOM.createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <AuthProvider>
      <App />
    </AuthProvider>
  </BrowserRouter>
);
```

### 4. Login page UI (30–35 min)

Create `src/components/LoginPage.jsx`:

```jsx
import { useState } from "react";
import { useNavigate } from "react-router-dom";
import { useAuth } from "../AuthContext";

function LoginPage() {
  const { login } = useAuth();
  const navigate = useNavigate();

  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [submitting, setSubmitting] = useState(false);
  const [error, setError] = useState(null);

  async function handleSubmit(e) {
    e.preventDefault();
    setSubmitting(true);
    setError(null);

    try {
      await login(email, password);
      navigate("/"); // go to notes
    } catch (err) {
      setError(err.message || "Login failed");
    } finally {
      setSubmitting(false);
    }
  }

  return (
    <div className="card">
      <h2>Login</h2>
      {error && <p style={{ color: "red" }}>{error}</p>}
      <form onSubmit={handleSubmit}>
        <div>
          <input
            type="email"
            placeholder="Email"
            value={email}
            autoComplete="email"
            onChange={(e) => setEmail(e.target.value)}
            disabled={submitting}
          />
        </div>
        <div>
          <input
            type="password"
            placeholder="Password"
            value={password}
            autoComplete="current-password"
            onChange={(e) => setPassword(e.target.value)}
            disabled={submitting}
          />
        </div>
        <button type="submit" disabled={submitting}>
          {submitting ? "Logging in..." : "Login"}
        </button>
      </form>
    </div>
  );
}

export default LoginPage;
```

Add route in `App.jsx`:

```jsx
import LoginPage from "./components/LoginPage";

<Routes>
  <Route path="/login" element={<LoginPage />} />
  {/* existing routes */}
</Routes>
```

Add nav link:

```jsx
import { useAuth } from "./AuthContext";

function App() {
  const { isAuthenticated, user, logout } = useAuth();
  // ...
  <nav>
    <Link to="/">Notes</Link>{" "}
    <Link to="/quote">Random Quote</Link>{" "}
    {!isAuthenticated && <Link to="/login">Login</Link>}
    {isAuthenticated && (
      <>
        <span style={{ marginLeft: "1rem" }}>Hello, {user.email}</span>
        <button onClick={logout}>Logout</button>
      </>
    )}
  </nav>;
}
```

### 5. Reflection (5–10 min)

In `notes-day5.txt`:

- Where are you storing the auth token?
- What happens in the UI when you log out?

---

## Day 6 – Calling Protected Endpoints from React

**Objectives:**
- Attach the JWT to requests to `/notes`.
- Redirect unauthenticated users to `/login`.

### 1. Update API helper to include token (25–30 min)

In `api.js`, change `request` to optionally take a `token`:

```js
async function request(path, options = {}, token) {
  const url = `${API_BASE_URL}${path}`;

  const defaultHeaders = {
    "Content-Type": "application/json",
  };

  const headers = { ...defaultHeaders, ...(options.headers || {}) };

  if (token) {
    headers.Authorization = `Bearer ${token}`;
  }

  const config = {
    ...options,
    headers,
  };

  // rest same
}
```

Update exported functions to accept `token`:

```js
export function getNotes(token) {
  return request("/notes", {}, token);
}

export function createNote(note, token) {
  return request("/notes", {
    method: "POST",
    body: JSON.stringify(note),
  }, token);
}

export function deleteNote(id, token) {
  return request(`/notes/${id}`, {
    method: "DELETE",
  }, token);
}

export function getNoteById(id, token) {
  return request(`/notes/${id}`, {}, token);
}

export function updateNote(id, note, token) {
  return request(`/notes/${id}`, {
    method: "PUT",
    body: JSON.stringify(note),
  }, token);
}
```

### 2. Use token in `NotesPage` (45–60 min)

In `NotesPage.jsx`:

```jsx
import { useAuth } from "../AuthContext";
import { getNotes, createNote, deleteNote } from "../api";
// ...

function NotesPage() {
  const { token, isAuthenticated } = useAuth();
  const [notes, setNotes] = useState([]);
  const [status, setStatus] = useState("idle");
  const [error, setError] = useState(null);

  useEffect(() => {
    if (!isAuthenticated) {
      setStatus("idle");
      setNotes([]);
      return;
    }

    async function loadNotes() {
      setStatus("loading");
      setError(null);

      try {
        const data = await getNotes(token);
        setNotes(data);
        setStatus("success");
      } catch (err) {
        setError(err.message || "Failed to load notes");
        setStatus("error");
      }
    }

    loadNotes();
  }, [token, isAuthenticated]);

  async function handleCreate(noteData) {
    const newNote = await createNote(noteData, token);
    setNotes((prev) => [newNote, ...prev]);
  }

  async function handleDelete(id) {
    const ok = window.confirm("Delete this note?");
    if (!ok) return;
    await deleteNote(id, token);
    setNotes((prev) => prev.filter((note) => note._id !== id));
  }

  if (!isAuthenticated) {
    return <p>Please log in to view your notes.</p>;
  }

  // rest of component JSX as before
}
```

Similarly, in `NoteDetailPage.jsx` use `getNoteById(id, token)` and `useAuth`.

### 3. Optional: ProtectedRoute component (15–20 min)

Create `ProtectedRoute.jsx`:

```jsx
import { Navigate } from "react-router-dom";
import { useAuth } from "../AuthContext";

function ProtectedRoute({ children }) {
  const { isAuthenticated } = useAuth();

  if (!isAuthenticated) {
    return <Navigate to="/login" replace />;
  }

  return children;
}

export default ProtectedRoute;
```

Wrap routes in `App.jsx`:

```jsx
import ProtectedRoute from "./components/ProtectedRoute";

<Route
  path="/"
  element={
    <ProtectedRoute>
      <NotesPage />
    </ProtectedRoute>
  }
/>
<Route
  path="/notes/:id"
  element={
    <ProtectedRoute>
      <NoteDetailPage />
    </ProtectedRoute>
  }
/>
```

### 4. Reflection (5–10 min)

In `notes-day6.txt`:

- How does the token reach the backend from React?
- What happens if the token is missing or invalid?

---

## Day 7 – End-to-End Testing, Cleanup & Reflection

**Objectives:**
- Test the full auth flow from React through backend.
- Clean up and comment your code.
- Reflect on the auth flow.

### 1. End-to-end test (30–40 min)

With backend and frontend running:

1. Ensure your DB is clean or note multiple users:
   - Register a new user via Postman or a temporary register page (you can also add a basic register form similar to login).
2. In the frontend:
   - Go to `/login`.
   - Log in with that user.
   - Verify:
     - Navbar changes (shows email + logout).
     - Notes page accessible; “Please log in” message disappears.
3. Create a new note:
   - Check in MongoDB that it has `user` set to this user’s id.
4. Logout:
   - Confirm notes page now redirects or shows “Please log in”.
5. If you have two users:
   - Login as user A, create notes.
   - Login as user B:
     - Should see only user B’s notes.

Record any bugs or rough edges in `auth-bugs-or-todos.txt`.

### 2. Cleanup & comments (20–25 min)

- In backend:
  - `routes/auth.js`, `middleware/auth.js`, `routes/notes.js`:
    - Add a one-line description at top.
    - Ensure consistent error messages.
- In frontend:
  - `AuthContext.jsx`, `LoginPage.jsx`, `NotesPage.jsx`, `ProtectedRoute.jsx`:
    - Add small comments explaining key pieces (auth state, token usage).
- Remove leftover debugging `console.log`s (keep essential ones if helpful).

### 3. Weekly reflection (20–25 min)

In `notes-week10-summary.txt`, answer:

- End-to-end understanding:
  - When you click “Login” in React, what **exact steps** happen until you see your notes?
- Do you understand:
  - How passwords are stored and verified with bcrypt?
  - How JWTs are created, verified, and where they are stored?
  - How to protect backend routes with middleware?
  - How to manage auth state and send tokens from React?
- What still feels confusing (e.g., token expiration, refresh tokens, security nuance like XSS/CSRF)?
- One clear auth-related improvement for later:
  - E.g., add “Register” page, show validation messages, add password confirmation, handle token expiry gracefully, etc.

---

If you’d like next, I can design a **Week 11 day‑by‑day plan** focused on:

- Rounding out your mini SaaS app: more features, better UI, simple analytics/stats.
- Refactoring code, adding reusable hooks/components.
- Preparing for deployment in Week 12.
