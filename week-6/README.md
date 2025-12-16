**Week 6 Theme:** Backend fundamentals with Node.js and Express – build and test a simple REST API.  
Assume ~2 hours/day. Work in a `week6/` folder.

By the end of the week you’ll have a small Node/Express API serving JSON, tested with a tool like Postman or your browser.

---

## Prerequisites

- Node.js and npm installed (check with `node -v` and `npm -v` in a terminal).
- Basic terminal comfort: `cd`, `ls`, etc.

---

## Day 1 – Backend Mental Model & Node.js Basics

**Objectives:**
- Understand how backend differs from frontend.
- Get comfortable running simple Node scripts.

### 1. Concept (25–30 min)
Review/learn:
- Frontend vs backend:
  - Frontend: runs in browser, handles UI, DOM.
  - Backend: runs on server, handles data, APIs, business logic.
- Node.js:
  - JavaScript runtime on the server.
  - Can read/write files, listen on ports, etc.
- `npm` basics:
  - Manages packages (express, etc.).

Key terms: runtime, package, dependency, script.

### 2. Practice: simple Node scripts (45–60 min)
In `week6/`:

1. Create `hello.js`:

   ```js
   console.log("Hello from Node.js!");
   ```

   Run:

   ```bash
   node hello.js
   ```

2. Create `greet.js`:

   ```js
   function greet(name) {
     return `Hello, ${name}!`;
   }

   const name = process.argv[2] || "world";
   console.log(greet(name));
   ```

   Run:

   ```bash
   node greet.js
   node greet.js Alice
   ```

3. Basic module usage: create `math-utils.js`:

   ```js
   function add(a, b) {
     return a + b;
   }

   function multiply(a, b) {
     return a * b;
   }

   module.exports = { add, multiply };
   ```

   And `use-math.js`:

   ```js
   const { add, multiply } = require("./math-utils");

   console.log("2 + 3 =", add(2, 3));
   console.log("4 * 5 =", multiply(4, 5));
   ```

   Run `node use-math.js`.

### 3. Reflection (5–10 min)
In `notes-day1.txt`:
- How is running JS with Node different from running JS in the browser?
- What is `npm` used for?

---

## Day 2 – Intro to Express & Your First HTTP Server

**Objectives:**
- Install Express.
- Build a minimal HTTP server that responds to GET requests.

### 1. Setup project (20–25 min)
In `week6/`, create folder `simple-api/`:

```bash
cd week6
mkdir simple-api
cd simple-api
npm init -y
npm install express
```

Check `package.json` was created and Express is listed in `dependencies`.

### 2. Create basic Express server (60–70 min)
Create `index.js`:

```js
const express = require("express");
const app = express();

// For parsing JSON request bodies (we'll use later)
app.use(express.json());

// Basic route
app.get("/", (req, res) => {
  res.send("Hello from Express!");
});

// Choose a port (usually from env, but hardcode for now)
const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
```

In `package.json`, add a script:

```json
"scripts": {
  "start": "node index.js"
}
```

Run:

```bash
npm start
```

Open `http://localhost:3000/` in your browser – you should see `"Hello from Express!"`.

### 3. Add another route (20–25 min)
In `index.js`, add:

```js
app.get("/hello", (req, res) => {
  res.send("Hello route!");
});

app.get("/status", (req, res) => {
  res.json({ status: "ok", time: new Date().toISOString() });
});
```

Check `/hello` (plain text) and `/status` (JSON) in your browser.

### 4. Reflection (5–10 min)
In `notes-day2.txt`:
- What does `app.get()` do?
- What is the role of `app.listen()`?

---

## Day 3 – Routes, Query Params & JSON Responses

**Objectives:**
- Understand routes and route parameters.
- Use query parameters to customize responses.
- Return JSON consistently.

### 1. Concept (25–30 min)
Learn:
- Routes: URL paths and HTTP methods (GET, POST, etc.).
- Query parameters: `?key=value&other=something`
  - Accessed via `req.query`.
- Route parameters: `/users/:id`
  - Accessed via `req.params`.

### 2. Practice: user greeting routes (60–70 min)
In `index.js`, add routes under a comment `// Day 3 routes`:

1. Route with query parameters:

   ```js
   app.get("/greet", (req, res) => {
     const name = req.query.name || "stranger";
     const lang = req.query.lang || "en";

     let message;
     if (lang === "en") message = `Hello, ${name}!`;
     else if (lang === "es") message = `Hola, ${name}!`;
     else message = `Hi, ${name}! (language not supported)`;

     res.json({ message });
   });
   ```

   Try:
   - `http://localhost:3000/greet`
   - `http://localhost:3000/greet?name=Alex`
   - `http://localhost:3000/greet?name=Alex&lang=es`

2. Route with path parameter:

   ```js
   app.get("/users/:id", (req, res) => {
     const userId = req.params.id;
     res.json({ id: userId, name: `User ${userId}` });
   });
   ```

   Try:
   - `http://localhost:3000/users/1`
   - `http://localhost:3000/users/abc`

### 3. Reflection (5–10 min)
In `notes-day3.txt`:
- Difference between `req.query` and `req.params`?
- Why is JSON (`res.json`) useful for APIs?

---

## Day 4 – In-Memory CRUD: Building a Simple “Items” API

**Objectives:**
- Implement CRUD operations (Create, Read, Update, Delete) in memory.
- Use different HTTP methods: GET, POST, PUT/PATCH, DELETE.

### 1. Concept (25–30 min)
Learn:
- REST & CRUD:
  - **Create**: POST `/items`
  - **Read**: GET `/items`, GET `/items/:id`
  - **Update**: PUT or PATCH `/items/:id`
  - **Delete**: DELETE `/items/:id`
- Request body:
  - Sent from client (e.g., JSON) and read via `req.body`.
  - You already added `app.use(express.json())` for parsing.

### 2. Implement in-memory store (60–70 min)
At top of `index.js`, add:

```js
let items = [];
let nextId = 1;
```

Then add routes:

1. GET all items:

   ```js
   app.get("/items", (req, res) => {
     res.json(items);
   });
   ```

2. GET one item by id:

   ```js
   app.get("/items/:id", (req, res) => {
     const id = Number(req.params.id);
     const item = items.find((it) => it.id === id);

     if (!item) {
       return res.status(404).json({ error: "Item not found" });
     }

     res.json(item);
   });
   ```

3. POST create item:

   ```js
   app.post("/items", (req, res) => {
     const name = req.body.name;

     if (!name || typeof name !== "string") {
       return res.status(400).json({ error: "Name is required and must be a string" });
     }

     const newItem = {
       id: nextId++,
       name,
     };
     items.push(newItem);
     res.status(201).json(newItem);
   });
   ```

4. PUT update item:

   ```js
   app.put("/items/:id", (req, res) => {
     const id = Number(req.params.id);
     const item = items.find((it) => it.id === id);

     if (!item) {
       return res.status(404).json({ error: "Item not found" });
     }

     const name = req.body.name;
     if (!name || typeof name !== "string") {
       return res.status(400).json({ error: "Name is required and must be a string" });
     }

     item.name = name;
     res.json(item);
   });
   ```

5. DELETE item:

   ```js
   app.delete("/items/:id", (req, res) => {
     const id = Number(req.params.id);
     const index = items.findIndex((it) => it.id === id);

     if (index === -1) {
       return res.status(404).json({ error: "Item not found" });
     }

     const deleted = items.splice(index, 1)[0];
     res.json({ deleted });
   });
   ```

### 3. Reflection (5–10 min)
In `notes-day4.txt`:
- List your CRUD endpoints and what each one does.
- What status codes did you use (201, 404, 400, etc.) and why?

---

## Day 5 – Testing Your API with Postman/Insomnia & Basic Error Handling

**Objectives:**
- Use a tool like Postman or Insomnia to test endpoints.
- Improve error messages and validation.

### 1. Install & setup Postman or Insomnia (15–20 min)
- Download and install:
  - [Postman](https://www.postman.com/downloads/) or
  - [Insomnia](https://insomnia.rest/download)
- Create a new “Collection” named `Week6 Simple API`.

### 2. Test endpoints (60–70 min)
With the server running (`npm start`):

1. **GET `/items`**:
   - Should return `[]` initially.

2. **POST `/items`**:
   - Set method to POST, URL: `http://localhost:3000/items`.
   - In Body → raw → JSON:

     ```json
     { "name": "First item" }
     ```

   - Send → you should get a new item with an `id`.

3. **GET `/items`** again:
   - Should include your new item.

4. **GET `/items/:id`**:
   - Use an existing ID → should return that item.
   - Use a non-existing ID (e.g., 999) → should get 404 with error message.

5. **PUT `/items/:id`**:
   - Update name:

     ```json
     { "name": "Updated item" }
     ```

6. **DELETE `/items/:id`**:
   - Delete the item, confirm with GET `/items`.

7. Try sending bad data:
   - POST with `{}` or wrong types, see 400 error.

### 3. Improve error handling (20–25 min)
In `index.js`:
- Add a catch-all 404 route near the bottom (but before `app.listen`):

  ```js
  app.use((req, res) => {
    res.status(404).json({ error: "Route not found" });
  });
  ```

- Add a simple error handler (optional, but useful):

  ```js
  app.use((err, req, res, next) => {
    console.error("Unexpected error:", err);
    res.status(500).json({ error: "Internal server error" });
  });
  ```

(You can trigger it later if needed by `next(err)` from a route.)

### 4. Reflection (5–10 min)
In `notes-day5.txt`:
- How does Postman/Insomnia help compared to using only the browser?
- Which error cases did you test?

---

## Day 6 – Organizing Code: Routers & Clean Structure

**Objectives:**
- Separate routes into their own file using `express.Router`.
- Prepare for larger APIs (like your Week 7 notes API).

### 1. Concept (25–30 min)
Learn:
- Why organize code?
  - Easier to maintain, read, and scale.
- `express.Router`:
  - Allows you to group routes (e.g., all `/items` routes in one file).

### 2. Refactor into router (60–70 min)
In `simple-api/`:

1. Create `routes/items.js`:

   ```js
   const express = require("express");
   const router = express.Router();

   let items = [];
   let nextId = 1;

   router.get("/", (req, res) => {
     res.json(items);
   });

   router.get("/:id", (req, res) => {
     const id = Number(req.params.id);
     const item = items.find((it) => it.id === id);

     if (!item) {
       return res.status(404).json({ error: "Item not found" });
     }

     res.json(item);
   });

   router.post("/", (req, res) => {
     const name = req.body.name;

     if (!name || typeof name !== "string") {
       return res.status(400).json({ error: "Name is required and must be a string" });
     }

     const newItem = {
       id: nextId++,
       name,
     };
     items.push(newItem);
     res.status(201).json(newItem);
   });

   router.put("/:id", (req, res) => {
     const id = Number(req.params.id);
     const item = items.find((it) => it.id === id);

     if (!item) {
       return res.status(404).json({ error: "Item not found" });
     }

     const name = req.body.name;
     if (!name || typeof name !== "string") {
       return res.status(400).json({ error: "Name is required and must be a string" });
     }

     item.name = name;
     res.json(item);
   });

   router.delete("/:id", (req, res) => {
     const id = Number(req.params.id);
     const index = items.findIndex((it) => it.id === id);

     if (index === -1) {
       return res.status(404).json({ error: "Item not found" });
     }

     const deleted = items.splice(index, 1)[0];
     res.json({ deleted });
   });

   module.exports = router;
   ```

2. Update `index.js` to use the router:

   ```js
   const express = require("express");
   const app = express();

   app.use(express.json());

   const itemsRouter = require("./routes/items");

   app.get("/", (req, res) => {
     res.send("Hello from Express!");
   });

   app.use("/items", itemsRouter);

   app.use((req, res) => {
     res.status(404).json({ error: "Route not found" });
   });

   const PORT = 3000;
   app.listen(PORT, () => {
     console.log(`Server is running on http://localhost:${PORT}`);
   });
   ```

3. Test your endpoints again in Postman/Insomnia to confirm everything still works.

### 3. Reflection (5–10 min)
In `notes-day6.txt`:
- How does splitting routes into a separate file make your project structure clearer?
- What other route groups might you have in a larger app (e.g., `/users`, `/auth`)?

---

## Day 7 – Consolidation, Small Enhancements & Review

**Objectives:**
- Add a small enhancement or two.
- Review and solidify core backend concepts.

### 1. Small enhancement (45–60 min)
Pick **one** of these (or invent your own):

**Option A – Additional item fields**
- Extend item model to:

  ```js
  { id, name, completed: false, createdAt: ... }
  ```

- When creating an item:
  - Set `completed: false`.
  - Set `createdAt: new Date().toISOString()`.
- Add a route to mark item as completed:
  - `PATCH /items/:id/complete` that sets `completed = true`.

**Option B – Filtering items**
- Support query parameter `?completed=true` or `?completed=false` on GET `/items`:
  ```js
  router.get("/", (req, res) => {
    const { completed } = req.query;
    let result = items;

    if (completed === "true") {
      result = items.filter((it) => it.completed === true);
    } else if (completed === "false") {
      result = items.filter((it) => it.completed === false);
    }

    res.json(result);
  });
  ```

Test with Postman.

### 2. Light cleanup & comments (20–25 min)
- Add clear comments at the top of `routes/items.js` and `index.js` describing their purpose.
- Check for:
  - Duplicate logic.
  - Inconsistent error messages.
  - Missing `return` after sending a response (you already handled this in some places).

If using Git:
- Initialize repo in `simple-api` and commit your work, or commit into your existing monorepo.

### 3. Weekly review (20–25 min)
In `notes-week6-summary.txt`, answer:
- What is an API in your own words?
- List all HTTP methods you used and what they represent.
- Do you understand:
  - How to create an Express app?
  - How to define routes and use `req.query`, `req.params`, `req.body`?
  - How to send JSON with `res.json()` and status codes with `res.status()`?
- What’s one thing about backend development that still feels unclear (e.g., auth, databases, environment variables)?

---

If you’d like, next I can create a **Week 7 day-by-day plan** focused on:
- Introducing MongoDB + Mongoose.
- Turning this in-memory items/notes API into a persistent CRUD API with a real database (the foundation for your later full-stack app).
