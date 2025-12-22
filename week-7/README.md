Here’s your **Week 7 (Days 1–7) plan**, where you’ll move from frontend to **backend with Node.js & Express**.

Assume ~2–3 hours/day.  
Each day: **Learn → Do → Reflect → Stretch**.  
By the end of Week 7 you should:

- Understand what Node.js is and how it differs from browser JS.  
- Know how to build a simple **Express server**.  
- Create and test basic **REST API endpoints** using **Postman/Insomnia**.  
- Handle JSON requests/responses and simple in‑memory data.

You’ll stay away from databases **this week** (we’ll add them in Week 8). This week is about HTTP, routes, and backend mental models.

---

## Day 1 – What is Node.js? Environment & First Script

**Goals:**
- Understand what Node.js is (JS outside the browser).
- Set up a Node project and run your first scripts.
- Learn basic `npm` usage.

### 1. Learn (40–60 minutes)

**Concepts:**
- Node.js:
  - JS runtime built on Chrome’s V8 engine.
  - Lets you run JS on the server (no DOM, no `window`).
- Differences between browser JS and Node:
  - No `document`, `window`, localStorage.
  - Access to filesystem, environment variables, etc.
- `npm`:
  - Node’s package manager.
  - `package.json` holds metadata + dependencies.

**Read/Watch:**
- Node.js docs: “About Node.js” (overview).
- MDN: “Introduction to Node.js” (high-level).
- Skim: what `npm init` does.

Notes:
- Write a few bullet points:
  - What Node can do that browser JS cannot.
  - What `package.json` is for.

### 2. Do (60–90 minutes)

Create a folder: `week7-node-basics/`.

1. **Initialize a Node project:**

   In terminal inside the folder:

   ```bash
   npm init -y
   ```

   - Open `package.json` and glance at contents (`name`, `version`, `main`, `scripts`).

2. **Create and run a Node script:**

   - Create `hello.js`:

     ```js
     console.log("Hello from Node!");

     const name = "Backend Learner";
     console.log(`Welcome, ${name}.`);
     ```

   - Run:

     ```bash
     node hello.js
     ```

3. **Practice a bit more logic (no HTTP yet):**
   - Create `math.js`:

     ```js
     function add(a, b) {
       return a + b;
     }

     function multiply(a, b) {
       return a * b;
     }

     console.log("2 + 3 =", add(2, 3));
     console.log("4 * 5 =", multiply(4, 5));
     ```

   - Run: `node math.js`.

### 3. Reflect (10–15 minutes)

- How does running `node hello.js` feel similar to/different from running JS in the browser console?
- What’s one thing Node lets you do that the browser doesn’t?

### 4. Stretch (optional, 20–30 minutes)

- Add a `scripts` entry in `package.json`:

  ```json
  "scripts": {
    "start": "node hello.js"
  }
  ```

  Then run: `npm start`.

- Create a small script `args.js` that reads command-line arguments:

  ```js
  const args = process.argv.slice(2);
  console.log("Arguments:", args);
  ```

  Run: `node args.js one two three`.

---

## Day 2 – HTTP Basics & Barebones Node Server (No Express Yet)

**Goals:**
- Understand HTTP requests/responses on a deeper level.
- Build a basic HTTP server using Node’s built-in `http` module.
- Inspect requests in a simple way.

### 1. Learn (40–60 minutes)

**Concepts:**
- HTTP basics:
  - Methods: GET, POST, PUT, DELETE.
  - URL, path, query string (`?key=value`).
  - Status codes: 200, 201, 400, 404, 500 (know what they mean conceptually).
- Node `http` module:
  - `http.createServer((req, res) => { ... })`.

**Read:**
- MDN: “An overview of HTTP”.
- Node docs: “HTTP” (overview and a simple example).

Notes:
- Write a short description for:
  - GET vs POST.
  - 200 vs 404 vs 500.

### 2. Do (60–90 minutes)

In `week7-node-basics/`, create `server-basic.js`.

1. **Simple HTTP server:**

   ```js
   const http = require("http");

   const server = http.createServer((req, res) => {
     console.log(`${req.method} ${req.url}`);

     if (req.url === "/" && req.method === "GET") {
       res.statusCode = 200;
       res.setHeader("Content-Type", "text/plain");
       res.end("Hello from barebones Node server!");
     } else if (req.url === "/about" && req.method === "GET") {
       res.statusCode = 200;
       res.setHeader("Content-Type", "text/plain");
       res.end("About page");
     } else {
       res.statusCode = 404;
       res.setHeader("Content-Type", "text/plain");
       res.end("Not Found");
     }
   });

   const PORT = 3000;
   server.listen(PORT, () => {
     console.log(`Server running at http://localhost:${PORT}`);
   });
   ```

   - Run: `node server-basic.js`.
   - Visit `http://localhost:3000/` and `/about` in your browser.

2. **Experiment:**
   - Add another route `/contact`.
   - Log `req.headers` to see what headers look like.

### 3. Reflect (10–15 minutes)

- What happens when you hit an undefined route?
- How do you set the status code and headers in this manual server?

### 4. Stretch (optional, 20–30 minutes)

- Return JSON instead of text for one route:

  ```js
  if (req.url === "/api/info" && req.method === "GET") {
    res.statusCode = 200;
    res.setHeader("Content-Type", "application/json");
    res.end(JSON.stringify({ message: "Hello", time: new Date().toISOString() }));
  }
  ```

- Observe the difference in the browser and in Postman/Insomnia (if you already use them).

---

## Day 3 – Introducing Express & Basic Routing

**Goals:**
- Install and set up **Express**.
- Build routes with Express (`app.get`, `app.post`, etc.).
- Understand why Express is nicer than the bare `http` module.

### 1. Learn (40–60 minutes)

**Concepts:**
- Express:
  - Minimalist web framework for Node.
  - Simplifies routing, middleware, request parsing.
- Basic Express app:
  - `const app = express();`
  - `app.get("/path", (req, res) => { ... })`
  - `app.listen(PORT, ...)`.

**Read:**
- Express docs: “Getting started”.
- Skim “Basic routing” section.

Notes:
- Write down:
  - Minimal Express server structure.
  - How to send JSON: `res.json({ ... })`.

### 2. Do (60–90 minutes)

Create a new folder: `week7-express/`.

1. **Initialize and install Express:**

   ```bash
   npm init -y
   npm install express
   ```

2. **Create `index.js`:**

   ```js
   const express = require("express");

   const app = express();
   const PORT = 3000;

   app.get("/", (req, res) => {
     res.send("Hello from Express!");
   });

   app.get("/about", (req, res) => {
     res.send("About from Express");
   });

   app.get("/api/info", (req, res) => {
     res.json({
       message: "Express API",
       time: new Date().toISOString(),
     });
   });

   app.listen(PORT, () => {
     console.log(`Server is running at http://localhost:${PORT}`);
   });
   ```

3. **Run & test:**
   - Run: `node index.js`.
   - Visit `/`, `/about`, `/api/info`.

4. **Add a `nodemon` dev dependency (optional but useful):**

   ```bash
   npm install --save-dev nodemon
   ```

   In `package.json`:

   ```json
   "scripts": {
     "dev": "nodemon index.js"
   }
   ```

   Then run: `npm run dev`.

### 3. Reflect (10–15 minutes)

- Compared to the bare Node server, what did Express simplify?
- How easy was it to add JSON endpoints?

### 4. Stretch (optional, 20–30 minutes)

- Add a new route `/api/status` that returns JSON with:
  - `status: "ok"`, `uptime: process.uptime()`.
- Try returning different HTTP status codes using `res.status(201).json(...)`.

---

## Day 4 – Working with Query & Route Parameters, JSON Body

**Goals:**
- Read **query parameters** and **route parameters** in Express.
- Parse **JSON request bodies** using `express.json()`.

### 1. Learn (40–60 minutes)

**Concepts:**
- Query params: `/search?term=react&page=2`
  - Access via `req.query`.
- Route params: `/users/:id`
  - Access via `req.params`.
- JSON body:
  - Client sends JSON.
  - `app.use(express.json())` to parse `req.body`.

**Read:**
- Express docs: “req.query” and “req.params”.
- Express docs: “req.body” and body parsing (v4+ uses `express.json()`).

Notes:
- Write sample routes:
  - `GET /hello?name=Alex`
  - `GET /users/:id`
  - `POST /users` with JSON body.

### 2. Do (60–90 minutes)

In `week7-express/index.js`:

1. **Enable JSON body parsing:**

   ```js
   const express = require("express");
   const app = express();
   const PORT = 3000;

   app.use(express.json());
   ```

2. **Query parameter example:**

   ```js
   app.get("/hello", (req, res) => {
     const name = req.query.name || "stranger";
     res.send(`Hello, ${name}!`);
   });
   ```

   - Test: `http://localhost:3000/hello?name=Alex`.

3. **Route parameter example:**

   ```js
   app.get("/users/:id", (req, res) => {
     const userId = req.params.id;
     res.json({ message: `User ID is ${userId}` });
   });
   ```

   - Test: `GET /users/123`.

4. **POST with JSON body:**

   ```js
   app.post("/echo", (req, res) => {
     const data = req.body;
     res.json({
       received: data,
       receivedAt: new Date().toISOString(),
     });
   });
   ```

   - Use Postman/Insomnia or VS Code REST client to send:
     - POST `http://localhost:3000/echo` with JSON body: `{ "message": "Hi", "count": 2 }`.

### 3. Reflect (10–15 minutes)

- How do `req.query`, `req.params`, and `req.body` differ?
- When would you use each in a real API?

### 4. Stretch (optional, 20–30 minutes)

- Add a route `/search/users` that:
  - Takes `q` in query string (e.g. `/search/users?q=alex`).
  - Returns JSON with `{ query: q, results: [] }` for now.
- Add basic validation in POST `/echo`:
  - If no body or `message` is missing, respond with `400` and an error JSON.

---

## Day 5 – In-Memory REST API (CRUD for a Resource)

**Goals:**
- Build a simple **RESTful API** for a resource (e.g., `todos`) using Express.
- Implement basic **CRUD** operations with an **in-memory array**.

### 1. Learn (30–45 minutes)

**Concepts:**
- REST resource routes:
  - `GET /api/todos` – list
  - `POST /api/todos` – create
  - `GET /api/todos/:id` – read one
  - `PUT/PATCH /api/todos/:id` – update
  - `DELETE /api/todos/:id` – delete
- HTTP status codes for API:
  - 200 OK, 201 Created, 400 Bad Request, 404 Not Found.

Review:
- Week 4 array methods (`find`, `filter`, `map`), since you’ll use them here.

Sketch:
- State: `let todos = [...]`.
- Operations: `getAll`, `create`, `update`, `delete`.

### 2. Do (90–120 minutes)

In `week7-express/index.js` (or create `todos.js` and import it), implement a basic Todos API.

1. **Set up in-memory store:**

   ```js
   let nextId = 1;
   let todos = [
     { id: nextId++, text: "Learn Express", completed: false },
     { id: nextId++, text: "Build an API", completed: false },
   ];
   ```

2. **GET /api/todos – list all:**

   ```js
   app.get("/api/todos", (req, res) => {
     res.json(todos);
   });
   ```

3. **POST /api/todos – create new:**

   ```js
   app.post("/api/todos", (req, res) => {
     const { text } = req.body;
     if (!text || typeof text !== "string") {
       return res.status(400).json({ error: "Text is required" });
     }

     const newTodo = { id: nextId++, text, completed: false };
     todos.push(newTodo);
     res.status(201).json(newTodo);
   });
   ```

4. **GET /api/todos/:id – get by id:**

   ```js
   app.get("/api/todos/:id", (req, res) => {
     const id = Number(req.params.id);
     const todo = todos.find((t) => t.id === id);
     if (!todo) {
       return res.status(404).json({ error: "Todo not found" });
     }
     res.json(todo);
   });
   ```

5. **PUT /api/todos/:id – update:**

   ```js
   app.put("/api/todos/:id", (req, res) => {
     const id = Number(req.params.id);
     const todo = todos.find((t) => t.id === id);
     if (!todo) {
       return res.status(404).json({ error: "Todo not found" });
     }

     const { text, completed } = req.body;

     if (typeof text === "string") {
       todo.text = text;
     }
     if (typeof completed === "boolean") {
       todo.completed = completed;
     }

     res.json(todo);
   });
   ```

6. **DELETE /api/todos/:id – delete:**

   ```js
   app.delete("/api/todos/:id", (req, res) => {
     const id = Number(req.params.id);
     const index = todos.findIndex((t) => t.id === id);
     if (index === -1) {
       return res.status(404).json({ error: "Todo not found" });
     }
     const deleted = todos.splice(index, 1)[0];
     res.json(deleted);
   });
   ```

7. **Test all routes with Postman/Insomnia:**
   - Verify:
     - Creating returns 201 + new object.
     - Getting returns correct data.
     - Updating actually changes things.
     - Deleting removes the todo.

### 3. Reflect (10–15 minutes)

- Which endpoints felt straightforward? Which were trickier (usually PUT/DELETE)?
- How does this setup compare to your earlier vanilla JS To‑Do logic?

### 4. Stretch (optional, 20–30 minutes)

- Add simple filtering via query param on GET `/api/todos`:
  - e.g. `?completed=true` – returns only completed todos.
- Add basic validation to `PUT`:
  - If both `text` and `completed` are missing, return 400.

---

## Day 6 – API Design & Connecting to Your React Frontend (Conceptual + Small Demo)

**Goals:**
- Understand logical API design.
- Create CORS‑friendly Express config.
- Do a small test fetch from React to your local API.

### 1. Learn (40–60 minutes)

**Concepts:**
- API design:
  - Use `/api/...` prefix for backend routes.
  - Consistent JSON shapes: `{ data: ..., error: ... }` (optional style).
- CORS (Cross-Origin Resource Sharing):
  - Browser security rule: frontend on one origin calling backend on another.
  - Fix with `cors` middleware during development.

**Read:**
- MDN: “CORS”.
- Express `cors` package docs (npm page).

Notes:
- Write down:
  - Why CORS exists.
  - When you need it (React dev server on port 5173 calling API on 3000).

### 2. Do (90–120 minutes)

1. **Set up CORS in Express:**

   In `week7-express`:

   ```bash
   npm install cors
   ```

   In `index.js`:

   ```js
   const cors = require("cors");
   app.use(cors());
   ```

   - This allows all origins in dev (fine for learning).

2. **Connect from React (test only):**

   In your React project (`week5-react`), create `TestApi.jsx`:

   ```jsx
   import { useState, useEffect } from "react";

   function TestApi() {
     const [todos, setTodos] = useState([]);
     const [error, setError] = useState(null);

     useEffect(() => {
       async function loadTodos() {
         try {
           const res = await fetch("http://localhost:3000/api/todos");
           if (!res.ok) throw new Error(`HTTP error ${res.status}`);
           const data = await res.json();
           setTodos(data);
         } catch (err) {
           setError(err.message);
         }
       }

       loadTodos();
     }, []);

     if (error) return <p>Error: {error}</p>;

     return (
       <div>
         <h2>Todos from Backend</h2>
         <ul>
           {todos.map((todo) => (
             <li key={todo.id}>
               {todo.text} ({todo.completed ? "done" : "pending"})
             </li>
           ))}
         </ul>
       </div>
     );
   }

   export default TestApi;
   ```

   - Render `<TestApi />` in `App.jsx` while both servers are running:
     - Express on 3000, React dev server on 5173.

3. **Test & debug:**
   - If you get CORS errors, confirm `cors()` is applied before routes.
   - Check Network tab in DevTools to inspect request/response.

### 3. Reflect (10–15 minutes)

- How does it feel to have your React app talk to your own backend?
- What pieces have to be running and configured correctly for it to work?

### 4. Stretch (optional, 20–30 minutes)

- In React, add a small form to POST a new todo to `/api/todos`.
- After successful POST, reload the list (or optimistically add to state).

---

## Day 7 – Consolidation: Mini Backend Project & Review

**Goals:**
- Solidify backend concepts by building a small **API-only project**.
- Review Node/Express fundamentals and identify gaps.

You’ll build a small in‑memory **API** for a different resource, e.g. **“Notes”**, **“Books”**, or **“Users”**.

### 1. Plan (20–30 minutes)

Pick a simple resource, e.g. `notes`:

- Fields: `id`, `title`, `content`, maybe `createdAt`.
- Routes (CRUD):
  - `GET /api/notes`
  - `POST /api/notes`
  - `GET /api/notes/:id`
  - `PUT /api/notes/:id`
  - `DELETE /api/notes/:id`

In your notes:
- List each route and what it should do.
- Decide minimal validation rules (e.g. `title` required, `content` optional).

### 2. Do – Build the Mini API (90–120 minutes)

Create a new file in `week7-express`, e.g. `notes-api.js` (or reuse `index.js` and move todos aside).

1. **Set up Express with JSON + CORS:**

   ```js
   const express = require("express");
   const cors = require("cors");

   const app = express();
   const PORT = 3001;

   app.use(cors());
   app.use(express.json());
   ```

2. **In-memory data:**

   ```js
   let nextId = 1;
   let notes = [
     { id: nextId++, title: "First note", content: "Hello", createdAt: new Date().toISOString() },
   ];
   ```

3. **Implement CRUD routes:**
   - `GET /api/notes` – return array.
   - `POST /api/notes` – create new (validate title).
   - `GET /api/notes/:id` – find by id, 404 if not found.
   - `PUT /api/notes/:id` – update title/content.
   - `DELETE /api/notes/:id` – delete.

4. **Test thoroughly in Postman/Insomnia:**
   - Try valid and invalid requests.
   - Confirm status codes and responses make sense.

5. **Optional: Connect simple React client:**
   - If time/energy, in React create a barebones client like you did with todos.

### 3. Self-Review Checklist (20–30 minutes)

For each item, mark ✅ / ❌ and note if ❌:

- Node basics:
  - [ ] I can explain what Node is and why it’s used for backends.
  - [ ] I can run a basic Node script with `node file.js`.

- Express basics:
  - [ ] I can set up an Express server and add routes.
  - [ ] I can read `req.params`, `req.query`, and `req.body`.
  - [ ] I can send JSON responses and choose proper status codes.

- REST API:
  - [ ] I can design CRUD endpoints for a simple resource.
  - [ ] I can store data in an in‑memory array and manipulate it (create, read, update, delete).
  - [ ] I can test endpoints with Postman/Insomnia.

- Frontend–backend integration (basic):
  - [ ] I understand CORS conceptually.
  - [ ] I have at least one React component fetching from my Express API.

Write 3 bullet points:
- 2 things you feel confident about.
- 1 aspect you need to revisit (e.g. PUT vs PATCH, error handling, CORS details).

### 4. Reflect (15–20 minutes)

In your notes:
- Describe, step by step, what happens when your React frontend calls `GET /api/todos`:
  - Browser → Request → Express route → Response → React state → Render.
- How does this week’s backend work connect to:
  - Your upcoming **MongoDB integration** (Week 8),
  - Your eventual **full-stack project** (React frontend + Express API + DB)?

### 5. Stretch (optional, 30–45 minutes)

- Add **basic validation & error messages** to your Notes API:
  - If `title` is missing or too short, return `400` with `{"error":"..."}`.
- Add **filtering** or simple search on GET `/api/notes?query=...`.
- Brainstorm: how would you adapt this API to store data in a database instead of memory?

---

If you’d like next, I can:

- Create a **Week 8 plan** for adding **MongoDB/Mongoose** to this Express API,  
- Or help you design the data models and endpoints for your first serious full‑stack project (e.g., Task Manager or Habit Tracker) that you’ll build across upcoming weeks.
