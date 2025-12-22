Here’s your **Week 8 (Days 1–7) plan**, where you’ll connect your Express backend to a **real database with MongoDB + Mongoose**.

Assume ~2–3 hours/day.  
Each day: **Learn → Do → Reflect → Stretch**.

By the end of Week 8 you should be able to:
- Understand what a **NoSQL document database** is (MongoDB).
- Use **Mongoose** to define schemas/models and perform CRUD.
- Convert your in‑memory Express API (e.g. Todos) to a **persistent API** backed by MongoDB.
- Handle basic validation and errors from the database.

---

## Before Day 1 – One-Time Setup

If not already done:

1. **Install MongoDB:**
   - EITHER:
     - Use **MongoDB Atlas** (free cloud instance – recommended).
       - Create account at mongodb.com.
       - Create free cluster.
       - Create database user + password.
       - Get your connection string (looks like:  
         `mongodb+srv://<user>:<password>@cluster0.xxxx.mongodb.net/?retryWrites=true&w=majority`).
   - OR:
     - Install MongoDB locally and run `mongod` (if you prefer local).

2. Keep your **Week 7 Express project** ready (e.g. `week7-express`).

---

## Day 1 – MongoDB Concepts & Connecting with Mongoose

**Goals:**
- Understand basic MongoDB concepts.
- Install & connect Mongoose to your Express app.

### 1. Learn (40–60 minutes)

**Concepts:**
- MongoDB basics:
  - Database → collections → documents.
  - Documents = JSON-like objects (BSON).
- Differences vs SQL:
  - No tables/rows, schema is more flexible.
- Mongoose:
  - ODM (Object Data Modeling) library: defines schemas and models in JS.
  - Handles validation, queries, etc.

**Read/Watch:**
- MongoDB docs: “Introduction to MongoDB” (high level).
- Mongoose docs: “Getting Started”.
- Optional: short YouTube video “MongoDB vs SQL (for beginners)” (10–15 min).

In your notes, answer:
- What is a document in MongoDB?
- What is a Mongoose model?

### 2. Do (60–90 minutes)

In your Express project (copy `week7-express` to a new folder `week8-api` if you want to keep both):

1. **Install Mongoose:**

   ```bash
   cd week8-api
   npm install mongoose
   ```

2. **Connect to MongoDB:**
   - Create `config/db.js`:

     ```js
     const mongoose = require("mongoose");

     async function connectDB() {
       const uri = process.env.MONGODB_URI || "your-fallback-uri";
       try {
         await mongoose.connect(uri);
         console.log("MongoDB connected");
       } catch (err) {
         console.error("MongoDB connection error:", err.message);
         process.exit(1);
       }
     }

     module.exports = connectDB;
     ```

   - In `index.js` (or main server file):

     ```js
     const express = require("express");
     const cors = require("cors");
     const connectDB = require("./config/db");

     const app = express();
     const PORT = process.env.PORT || 3000;

     app.use(cors());
     app.use(express.json());

     // Connect to database
     connectDB();

     app.get("/", (req, res) => {
       res.send("API with MongoDB");
     });

     app.listen(PORT, () => {
       console.log(`Server running on http://localhost:${PORT}`);
     });
     ```

3. **Use environment variables:**
   - Install `dotenv`:

     ```bash
     npm install dotenv
     ```

   - At the top of `index.js`:

     ```js
     require("dotenv").config();
     ```

   - Create `.env` (DO NOT commit this to Git):

     ```env
     MONGODB_URI=your-mongodb-connection-string-here
     PORT=3000
     ```

   - Restart server and confirm “MongoDB connected” logs.

### 3. Reflect (10–15 minutes)

- How is connecting to a real DB different from your in‑memory arrays?
- What’s the benefit of using environment variables for the DB URI?

### 4. Stretch (optional, 20–30 minutes)

- Add a simple `/api/health` route that:
  - Returns `{ status: "ok", db: "connected" }`.
  - You can check `mongoose.connection.readyState` to infer status (optional).

---

## Day 2 – Defining a Mongoose Model (e.g. Todo)

**Goals:**
- Define a Mongoose schema + model.
- Create documents via code and inspect them in MongoDB.

### 1. Learn (40–60 minutes)

**Concepts:**
- Mongoose schema:
  - Field definitions: type, required, default.
- Model:
  - Created from schema.
  - Used to create/read/update/delete documents.
- Common field types:
  - `String`, `Number`, `Boolean`, `Date`.

**Read:**
- Mongoose docs: “Schemas”.
- Mongoose docs: “Models”.

In your notes:
- Sketch a schema for `Todo` with fields:
  - `text` (String, required),
  - `completed` (Boolean, default false),
  - `createdAt` (Date, default now).

### 2. Do (60–90 minutes)

1. **Create model file: `models/Todo.js`:**

   ```js
   const mongoose = require("mongoose");

   const todoSchema = new mongoose.Schema(
     {
       text: {
         type: String,
         required: true,
         trim: true,
       },
       completed: {
         type: Boolean,
         default: false,
       },
     },
     {
       timestamps: true, // adds createdAt and updatedAt
     }
   );

   const Todo = mongoose.model("Todo", todoSchema);

   module.exports = Todo;
   ```

2. **Test creating a document manually via a route (TEMPORARY):**

   In `index.js`:

   ```js
   const Todo = require("./models/Todo");

   app.get("/api/test-create-todo", async (req, res) => {
     try {
       const todo = await Todo.create({ text: "Test todo from route" });
       res.json(todo);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to create todo" });
     }
   });
   ```

   - Hit `GET /api/test-create-todo` in browser/Postman a few times.
   - Check your MongoDB cluster (or local DB) using MongoDB Atlas UI or `mongosh` to see documents.

3. **Temporary cleanup:**
   - You can remove or comment out `/api/test-create-todo` later; it’s just for learning.

### 3. Reflect (10–15 minutes)

- How does `Todo.create` compare to pushing into an array?
- What did `timestamps: true` give you for free?

### 4. Stretch (optional, 20–30 minutes)

- Add a `priority` field to the schema (`"low" | "medium" | "high"` using `enum`).
- Create another test route that creates a todo with a given `priority`.

---

## Day 3 – Converting GET/POST (Create & Read) to Use MongoDB

**Goals:**
- Replace your in‑memory todos API (from Week 7) with MongoDB-backed logic for **GET all** and **POST create**.

### 1. Learn (30–45 minutes)

Concepts:
- CRUD via Mongoose:
  - `Model.find()` – get list.
  - `Model.findById(id)` – get one.
  - `Model.create(doc)` – create.
- Async/await patterns and error handling.

Review:
- Week 7 Express CRUD logic (in-memory).
- Array methods you used — now replaced by Mongoose methods.

Write out pseudocode for:
- `GET /api/todos`:
  - `const todos = await Todo.find(); res.json(todos);`
- `POST /api/todos`:
  - Validate `req.body.text`, then `Todo.create(...)`.

### 2. Do (90–120 minutes)

In `week8-api`, update the Todos API (either in `index.js` or a separate `routes/todos.js` file).

1. **Remove old in-memory array & routes** (or comment them out).

2. **Implement `GET /api/todos`:**

   ```js
   app.get("/api/todos", async (req, res) => {
     try {
       const todos = await Todo.find().sort({ createdAt: -1 }); // newest first
       res.json(todos);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to fetch todos" });
     }
   });
   ```

3. **Implement `POST /api/todos`:**

   ```js
   app.post("/api/todos", async (req, res) => {
     try {
       const { text } = req.body;
       if (!text || typeof text !== "string") {
         return res.status(400).json({ error: "Text is required" });
       }

       const todo = await Todo.create({ text });
       res.status(201).json(todo);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to create todo" });
     }
   });
   ```

4. **Test with Postman/Insomnia:**
   - `GET /api/todos` – should return array from DB.
   - `POST /api/todos` – create new, then `GET` again to see it added.

5. **Observe DB:**
   - Look in MongoDB UI: the data is truly persistent now.

### 3. Reflect (10–15 minutes)

- What changed between your Week 7 code and this week’s code?
- Where is your data now, and what advantages does that give you?

### 4. Stretch (optional, 20–30 minutes)

- Allow optional `completed` in POST (default remains false).
- Add basic query support:
  - `GET /api/todos?completed=true` – use `Todo.find({ completed: true })`.

---

## Day 4 – Update & Delete with Mongoose (PUT/DELETE)

**Goals:**
- Implement **update** and **delete** routes with Mongoose.
- Understand and handle “not found” and validation errors.

### 1. Learn (30–45 minutes)

**Concepts:**
- Common Mongoose methods:
  - `findByIdAndUpdate(id, update, options)`
  - `findByIdAndDelete(id)`
- Options:
  - `{ new: true }` to return updated document.
  - `{ runValidators: true }` to enforce schema validation on update.
- Handling invalid IDs (e.g. malformed ObjectId).

Read:
- Mongoose docs: “Queries” (skim).
- Mongoose docs: “findByIdAndUpdate” and “findByIdAndDelete”.

In your notes, plan:
- `PUT /api/todos/:id`:
  - Extract `id`, read `text` and/or `completed`, update.
- `DELETE /api/todos/:id`:
  - Extract `id`, delete.

### 2. Do (90–120 minutes)

Add to your Todos routes:

1. **PUT /api/todos/:id – update:**

   ```js
   app.put("/api/todos/:id", async (req, res) => {
     const { id } = req.params;
     const { text, completed } = req.body;

     try {
       const update = {};
       if (typeof text === "string") update.text = text;
       if (typeof completed === "boolean") update.completed = completed;

       if (Object.keys(update).length === 0) {
         return res.status(400).json({ error: "No valid fields to update" });
       }

       const todo = await Todo.findByIdAndUpdate(id, update, {
         new: true,
         runValidators: true,
       });

       if (!todo) {
         return res.status(404).json({ error: "Todo not found" });
       }

       res.json(todo);
     } catch (err) {
       console.error(err);
       // Handle invalid ObjectId
       if (err.name === "CastError") {
         return res.status(400).json({ error: "Invalid ID format" });
       }
       res.status(500).json({ error: "Failed to update todo" });
     }
   });
   ```

2. **DELETE /api/todos/:id – delete:**

   ```js
   app.delete("/api/todos/:id", async (req, res) => {
     const { id } = req.params;

     try {
       const deleted = await Todo.findByIdAndDelete(id);
       if (!deleted) {
         return res.status(404).json({ error: "Todo not found" });
       }
       res.json(deleted);
     } catch (err) {
       console.error(err);
       if (err.name === "CastError") {
         return res.status(400).json({ error: "Invalid ID format" });
       }
       res.status(500).json({ error: "Failed to delete todo" });
     }
   });
   ```

3. **Test thoroughly:**
   - Use Postman:
     - Update `text`, `completed`.
     - Delete a todo.
     - Try invalid IDs and check errors.

### 3. Reflect (10–15 minutes)

- How do you handle the case where `findByIdAndUpdate` returns `null`?
- Why do you check for `CastError`?

### 4. Stretch (optional, 20–30 minutes)

- Add a `GET /api/todos/:id` using `Todo.findById(id)`.
- Add server-side validation on update (e.g. reject empty `text`).

---

## Day 5 – Basic Validation & Error Handling Patterns

**Goals:**
- Improve input validation at the API level.
- Structure error responses consistently.
- Understand common Mongoose validation errors.

### 1. Learn (40–60 minutes)

**Concepts:**
- Validation layers:
  - Client-side (React forms) – user convenience.
  - Server-side (Express + Mongoose) – security & correctness.
- Mongoose validation:
  - `required: true`, `minlength`, `maxlength`, `enum`, custom validators.
- Error handling:
  - Checking `err.name === "ValidationError"`.

Read:
- Mongoose docs: “Validation”.
- Skim Express error handling docs (built-in error middleware).

In your notes:
- Decide at least 2 validation rules for `Todo` (e.g. `text` min length 3).
- Decide on a simple, consistent error response structure:
  - `{ error: "Message" }` or `{ error: { message, details } }`.

### 2. Do (90–120 minutes)

1. **Enhance Todo schema (`models/Todo.js`):**

   ```js
   const todoSchema = new mongoose.Schema(
     {
       text: {
         type: String,
         required: [true, "Text is required"],
         trim: true,
         minlength: [3, "Text must be at least 3 characters"],
       },
       completed: {
         type: Boolean,
         default: false,
       },
     },
     {
       timestamps: true,
     }
   );
   ```

2. **Update POST & PUT handlers to catch validation errors:**

   Example for POST:

   ```js
   app.post("/api/todos", async (req, res) => {
     try {
       const { text, completed } = req.body;
       const todo = await Todo.create({ text, completed });
       res.status(201).json(todo);
     } catch (err) {
       console.error(err);
       if (err.name === "ValidationError") {
         return res.status(400).json({ error: err.message });
       }
       res.status(500).json({ error: "Failed to create todo" });
     }
   });
   ```

   Similarly update PUT to handle `ValidationError`.

3. **Test validation:**
   - Try creating with short text (`"OK"`).
   - Try missing text.
   - Confirm you get 400 and descriptive messages.

4. **Optional: central error-handling middleware:**
   - Create a function:

     ```js
     function errorHandler(err, req, res, next) {
       console.error(err);

       if (err.name === "ValidationError") {
         return res.status(400).json({ error: err.message });
       }
       if (err.name === "CastError") {
         return res.status(400).json({ error: "Invalid ID format" });
       }

       res.status(500).json({ error: "Something went wrong" });
     }
     ```

   - Use it:

     ```js
     app.use(errorHandler);
     ```

   - Then in routes, replace `try/catch` with `next(err)` (stretch; not required if too much).

### 3. Reflect (10–15 minutes)

- How does server-side validation protect your data?
- How do you distinguish between client errors (400) and server errors (500)?

### 4. Stretch (optional, 20–30 minutes)

- Create a simple `GET /api/todos/stats` endpoint:
  - Returns total count, completed count, incomplete count using MongoDB queries:
    - e.g. `const total = await Todo.countDocuments();`
- Think how this might be useful for a dashboard later.

---

## Day 6 – Integrating Your React Todo App with the Mongo API

**Goals:**
- Replace your React To‑Do app’s local/in‑memory logic with calls to your new MongoDB-backed API.
- Handle loading and error states.

### 1. Learn (30–45 minutes)

Concepts:
- Client–server responsibilities:
  - Backend: data persistence, validation, business rules.
  - Frontend: UI, user input, rendering.
- React data flow with API:
  - Initially load todos with `useEffect` → `setTodos`.
  - For actions: send POST/PUT/DELETE to API → update frontend state.

Review:
- Your React To‑Do app code (Week 5 & 6).
- Your new `/api/todos` endpoints.

In your notes:
- For each action (load, add, toggle, delete), write what HTTP call is needed.

### 2. Do (90–120 minutes)

In your React project (e.g. `week5-react`), update `TodoApp.jsx`:

Assume backend is running on `http://localhost:3000`.

1. **State for loading & error:**

   ```jsx
   const [todos, setTodos] = useState([]);
   const [loading, setLoading] = useState(false);
   const [error, setError] = useState(null);
   ```

2. **Load todos on mount:**

   ```jsx
   useEffect(() => {
     async function fetchTodos() {
       try {
         setLoading(true);
         setError(null);
         const res = await fetch("http://localhost:3000/api/todos");
         if (!res.ok) throw new Error(`HTTP error ${res.status}`);
         const data = await res.json();
         setTodos(data);
       } catch (err) {
         setError(err.message);
       } finally {
         setLoading(false);
       }
     }

     fetchTodos();
   }, []);
   ```

3. **Update handlers to call API:**

   - Add:

     ```jsx
     async function handleAddTodo(text) {
       try {
         const res = await fetch("http://localhost:3000/api/todos", {
           method: "POST",
           headers: { "Content-Type": "application/json" },
           body: JSON.stringify({ text }),
         });
         if (!res.ok) throw new Error(`Failed to create todo (${res.status})`);
         const newTodo = await res.json();
         setTodos((prev) => [newTodo, ...prev]);
       } catch (err) {
         console.error(err);
         alert("Error adding todo: " + err.message);
       }
     }

     async function handleToggleTodo(id) {
       const todo = todos.find((t) => t.id === id || t._id === id);
       if (!todo) return;
       try {
         const res = await fetch(`http://localhost:3000/api/todos/${todo._id || todo.id}`, {
           method: "PUT",
           headers: { "Content-Type": "application/json" },
           body: JSON.stringify({ completed: !todo.completed }),
         });
         if (!res.ok) throw new Error(`Failed to update todo (${res.status})`);
         const updated = await res.json();
         setTodos((prev) =>
           prev.map((t) => (t._id === updated._id || t.id === updated.id ? updated : t))
         );
       } catch (err) {
         console.error(err);
         alert("Error updating todo: " + err.message);
       }
     }

     async function handleDeleteTodo(id) {
       const todo = todos.find((t) => t.id === id || t._id === id);
       if (!todo) return;
       try {
         const res = await fetch(`http://localhost:3000/api/todos/${todo._id || todo.id}`, {
           method: "DELETE",
         });
         if (!res.ok) throw new Error(`Failed to delete todo (${res.status})`);
         await res.json();
         setTodos((prev) =>
           prev.filter((t) => t._id !== (todo._id || todo.id) && t.id !== (todo._id || todo.id))
         );
       } catch (err) {
         console.error(err);
         alert("Error deleting todo: " + err.message);
       }
     }
     ```

   - Adjust `TodoItem` to pass the correct ID (`todo._id` from Mongo) if present.

4. **Render loading & error states:**

   - In JSX:

     ```jsx
     if (loading) return <p>Loading todos...</p>;
     if (error) return <p>Error: {error}</p>;
     ```

   - Then render list normally.

5. **Test thoroughly:**
   - Add, toggle, delete todos.
   - Verify DB changes in MongoDB UI.

### 3. Reflect (10–15 minutes)

- How does this feel different from your purely client-side todo app?
- What are the trade-offs (network dependency, latency, but persistence and multi-user support)?

### 4. Stretch (optional, 20–30 minutes)

- Add a “Refresh” button to re-fetch todos from the server.
- Add a small “last updated at” timestamp in your UI.

---

## Day 7 – Consolidation: Mini Full-Stack “Todo + Stats” & Review

**Goals:**
- Consolidate everything from Weeks 7–8:
  - Express + MongoDB + React.
- Add a small extra feature: **stats** or **filtering** based on DB queries.
- Reflect on backend fundamentals.

### 1. Plan (20–30 minutes)

Decide what to add or improve:

Ideas:
- Add a `/api/todos/stats` endpoint that returns:
  - total tasks, completed tasks, incomplete tasks.
- Show these stats in your React UI.
- OR:
  - Add simple server-side filtering (e.g. `?completed=true`), then expose it via frontend controls.

Write in your notes:
- List new backend routes/endpoints you’ll add.
- What UI changes you’ll make in React to display or use them.

### 2. Do – Implement & Wire Up (90–120 minutes)

1. **Backend – `GET /api/todos/stats`:**

   ```js
   app.get("/api/todos/stats", async (req, res) => {
     try {
       const total = await Todo.countDocuments();
       const completed = await Todo.countDocuments({ completed: true });
       const incomplete = total - completed;
       res.json({ total, completed, incomplete });
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to fetch stats" });
     }
   });
   ```

2. **Frontend – Stats display:**

   - In `TodoApp.jsx`, add:

     ```jsx
     const [stats, setStats] = useState(null);

     async function fetchStats() {
       try {
         const res = await fetch("http://localhost:3000/api/todos/stats");
         if (!res.ok) throw new Error(`HTTP error ${res.status}`);
         const data = await res.json();
         setStats(data);
       } catch (err) {
         console.error(err);
       }
     }

   useEffect(() => {
     fetchTodos();
     fetchStats();
   }, []);
     ```

   - After each change (add/toggle/delete), call `fetchStats()` as well.

   - In JSX:

     ```jsx
     {stats && (
       <p>
         Total: {stats.total} | Completed: {stats.completed} | Incomplete:{" "}
         {stats.incomplete}
       </p>
     )}
     ```

3. **Test:**
   - Perform CRUD operations.
   - Confirm stats update correctly.
   - Check DB to verify counts match reality.

### 3. Self-Review Checklist (20–30 minutes)

Mark ✅ / ❌:

- MongoDB & Mongoose:
  - [ ] I understand what a collection and document are.
  - [ ] I can define a Mongoose schema & model.
  - [ ] I can use `find`, `create`, `findByIdAndUpdate`, `findByIdAndDelete`.

- Express + Mongo:
  - [ ] I can wire up Express routes that talk to Mongoose.
  - [ ] I can handle basic validation and error cases.
  - [ ] I can return meaningful status codes & error messages.

- Full-stack integration:
  - [ ] I updated my React app to use my own Mongo-backed API.
  - [ ] I handle loading & error states in the frontend.
  - [ ] I can explain the flow from React → Express → Mongo → back to React.

Write a short paragraph:
- What part of Mongo/Mongoose felt most confusing?
- Which parts you now feel reasonably confident about?

### 4. Reflect (15–20 minutes)

In your notes:
- Describe, step by step, what happens when you:
  1. Add a todo in your React UI.
  2. Toggle a todo as completed.
  3. Refresh the page to see persisted todos.

- How does this set the stage for:
  - **Authentication** (Week 9–10),
  - **User-specific data** (each user has their own todos),
  - And ultimately a full featured **Task Manager / Habit Tracker** app?

### 5. Stretch (optional, 30–45 minutes)

- Add **server-side pagination** for todos:
  - `GET /api/todos?page=1&limit=10` using `skip` + `limit`.
- Or: Introduce a second model (e.g. `User`) and associate todos with a `userId` (even if you don’t have full auth yet).

---

If you’d like next, I can:

- Create a **Week 9 plan** focused on **authentication and user accounts** (JWT, password hashing, protected routes), or  
- Help you sketch the architecture & feature list for your first “real” full-stack project (Task Manager, Habit Tracker, etc.) that uses everything you’ve built so far.
