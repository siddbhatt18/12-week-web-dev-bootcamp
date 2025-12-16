**Week 7 Theme:** MongoDB + Mongoose + REST API – build a real persistent CRUD API (Notes API prototype for P4).  
Assume ~2 hours/day. Work in a `week7/` folder.

You’ll end the week with an Express API that stores **Notes** in MongoDB instead of memory.

---

## Prerequisites

- Week 6 done (you can define routes, use `req.body`, `req.params`, `res.json`).
- Node + npm installed.
- MongoDB:
  - EITHER local MongoDB installed  
  - OR (recommended) a free **MongoDB Atlas** cluster.

I’ll assume **MongoDB Atlas**; adapt if you’re using local MongoDB.

---

## Day 1 – MongoDB & Mongoose Mental Model

**Objectives:**
- Understand what MongoDB is and how it differs from SQL.
- Setup a new project with Express + Mongoose.

### 1. Concept (25–30 min)

Learn (read/watch, short notes):

- **MongoDB basics:**
  - NoSQL document database.
  - Data stored as **collections** of **documents** (JSON-like).
  - Each document has an `_id` and arbitrary fields (e.g., `title`, `content`).
- Compare to SQL (very briefly):
  - SQL: tables, rows, columns.
  - MongoDB: collections, documents, flexible schema.
- **Mongoose:**
  - ODM (Object Data Modeling) library for MongoDB + Node.
  - You define **schemas** → Mongoose enforces structure & gives helper methods.

Key idea: You’ll model **Note** documents in a `notes` collection.

### 2. Project setup (45–60 min)

In `week7/`:

```bash
mkdir notes-api
cd notes-api
npm init -y
npm install express mongoose dotenv
```

Create basic structure:

```text
notes-api/
  index.js
  models/
    Note.js
  .env        (you'll fill later)
```

In `index.js`:

```js
require("dotenv").config();
const express = require("express");
const mongoose = require("mongoose");

const app = express();
app.use(express.json());

const PORT = process.env.PORT || 4000;

// Simple test route
app.get("/", (req, res) => {
  res.send("Notes API - Week 7");
});

// Connect to MongoDB (we'll fill MONGODB_URI tomorrow)
mongoose
  .connect(process.env.MONGODB_URI)
  .then(() => {
    console.log("Connected to MongoDB");
    app.listen(PORT, () => {
      console.log(`Server listening on http://localhost:${PORT}`);
    });
  })
  .catch((err) => {
    console.error("MongoDB connection error:", err);
  });
```

Don’t worry if it fails right now; you haven’t set `MONGODB_URI` yet.

### 3. Reflection (5–10 min)

In `notes-day1.txt`:

- In your own words, what is a “collection” and what is a “document” in MongoDB?
- Why are we using Mongoose instead of talking to MongoDB directly?

---

## Day 2 – MongoDB Atlas Setup & First Connection

**Objectives:**
- Create a MongoDB Atlas cluster & database.
- Connect your Node app to it.
- Confirm you can start the server successfully.

### 1. Create MongoDB Atlas cluster (30–40 min)

1. Go to https://www.mongodb.com/atlas and create a free account.
2. Create a free cluster (Shared / Free tier).
3. When prompted:
   - Create a **database user** (username/password).
   - Allow access from your IP (or “allow from anywhere” for learning).
4. Once cluster is ready, click “Connect” → “Connect your application.”
5. Copy the connection string, it will look like:

   ```
   mongodb+srv://<username>:<password>@<cluster-name>.mongodb.net/?retryWrites=true&w=majority
   ```

   You’ll modify it to specify a DB name, e.g.:

   ```
   mongodb+srv://<username>:<password>@<cluster-name>.mongodb.net/notesdb?retryWrites=true&w=majority
   ```

### 2. Add `.env` and connect (30–40 min)

In `notes-api/.env`:

```env
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/notesdb?retryWrites=true&w=majority
PORT=4000
```

**Important:** replace `<username>`, `<password>`, `<cluster>` with your actual values.

In `index.js`:
- Already calling `require("dotenv").config();` and using `process.env.MONGODB_URI`.

Run:

```bash
npm start
```

You should see in the console:

- “Connected to MongoDB”
- “Server listening on http://localhost:4000”

Visit `http://localhost:4000/` in the browser – you should see `"Notes API - Week 7"`.

If there’s an error:
- Double-check the connection string and credentials.
- Check IP access in Atlas.

### 3. Reflection (5–10 min)

In `notes-day2.txt`:

- Where do we store secrets like DB password, and why?
- What did you have to change to get MongoDB connected?

---

## Day 3 – Defining a Note Model with Mongoose

**Objectives:**
- Create a Mongoose schema and model for `Note`.
- Add basic fields and validation rules.

### 1. Concept (25–30 min)

Learn:

- **Schema & Model:**

  ```js
  const noteSchema = new mongoose.Schema({
    title: { type: String, required: true },
    content: { type: String },
  });

  const Note = mongoose.model("Note", noteSchema);
  ```

- Mongoose automatically creates a `notes` collection (pluralized).
- Timestamps option:

  ```js
  new mongoose.Schema({...}, { timestamps: true });
  ```

  Adds `createdAt` and `updatedAt` automatically.

### 2. Implement `Note` model (45–60 min)

In `models/Note.js`:

```js
const mongoose = require("mongoose");

const noteSchema = new mongoose.Schema(
  {
    title: {
      type: String,
      required: true,
      trim: true,
    },
    content: {
      type: String,
      trim: true,
    },
  },
  { timestamps: true }
);

const Note = mongoose.model("Note", noteSchema);

module.exports = Note;
```

In `index.js`, import the model just to ensure it loads (top of file):

```js
const Note = require("./models/Note");
```

Add a **temporary test route** to create a note (you’ll delete or refactor later):

```js
app.get("/test-create-note", async (req, res) => {
  try {
    const note = await Note.create({
      title: "Test Note",
      content: "Created from /test-create-note route",
    });
    res.json(note);
  } catch (err) {
    console.error(err);
    res.status(500).json({ error: "Failed to create test note" });
  }
});
```

Restart server and visit `http://localhost:4000/test-create-note`.  
Check if a JSON note comes back with `_id`, `createdAt`, etc.

You can also open Atlas → your database → `notes` collection to see the new document.

### 3. Reflection (5–10 min)

In `notes-day3.txt`:

- What fields did you define on the Note model?
- What does the `{ timestamps: true }` option do?

---

## Day 4 – CRUD Operations: Create & Read Notes

**Objectives:**
- Implement `POST /notes` to create a note.
- Implement `GET /notes` and `GET /notes/:id` to read notes.

### 1. Concept (20–25 min)

Design your API (these will match P4 later):

- `POST /notes` – create note
- `GET /notes` – list all notes
- `GET /notes/:id` – get single note by ID

Think through:

- What fields do you require in the request body? (At least `title`.)
- Status codes:
  - `201` for created.
  - `400` for validation error.
  - `404` for not found.
  - `500` for unexpected errors.

### 2. Implement routes (60–70 min)

For better structure, create `routes/notes.js`.

`routes/notes.js`:

```js
const express = require("express");
const Note = require("../models/Note");

const router = express.Router();

// CREATE note - POST /notes
router.post("/", async (req, res) => {
  try {
    const { title, content } = req.body;

    if (!title || typeof title !== "string") {
      return res
        .status(400)
        .json({ error: "Title is required and must be a string" });
    }

    const note = await Note.create({ title, content });
    res.status(201).json(note);
  } catch (err) {
    console.error("Error creating note:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});

// GET all notes - GET /notes
router.get("/", async (req, res) => {
  try {
    const notes = await Note.find().sort({ createdAt: -1 });
    res.json(notes);
  } catch (err) {
    console.error("Error fetching notes:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});

// GET single note by id - GET /notes/:id
router.get("/:id", async (req, res) => {
  try {
    const { id } = req.params;

    // basic validation: check if id is a valid ObjectId
    if (!id.match(/^[0-9a-fA-F]{24}$/)) {
      return res.status(400).json({ error: "Invalid note ID format" });
    }

    const note = await Note.findById(id);
    if (!note) {
      return res.status(404).json({ error: "Note not found" });
    }

    res.json(note);
  } catch (err) {
    console.error("Error fetching note:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});

module.exports = router;
```

In `index.js`, mount the router:

```js
const express = require("express");
const mongoose = require("mongoose");
require("dotenv").config();

const Note = require("./models/Note");
const notesRouter = require("./routes/notes");

const app = express();
app.use(express.json());

const PORT = process.env.PORT || 4000;

app.get("/", (req, res) => {
  res.send("Notes API - Week 7");
});

app.use("/notes", notesRouter);

// 404 fallback
app.use((req, res) => {
  res.status(404).json({ error: "Route not found" });
});

mongoose
  .connect(process.env.MONGODB_URI)
  .then(() => {
    console.log("Connected to MongoDB");
    app.listen(PORT, () => {
      console.log(`Server listening on http://localhost:${PORT}`);
    });
  })
  .catch((err) => {
    console.error("MongoDB connection error:", err);
  });
```

Test with Postman:

- `POST /notes` with JSON body:

  ```json
  { "title": "My first note", "content": "Week 7 is going well." }
  ```

- `GET /notes` – should return a list including your new note.
- `GET /notes/<id>` – use `_id` from previous response.

### 3. Reflection (5–10 min)

In `notes-day4.txt`:

- What happens if you try to `GET /notes/someBadId`?
- What status codes did you use for:
  - Successful create
  - Not found
  - Invalid ID

---

## Day 5 – CRUD Operations: Update & Delete Notes

**Objectives:**
- Implement `PUT` (or `PATCH`) to update a note.
- Implement `DELETE` to delete a note.

### 1. Concept (20–25 min)

Decide:

- Use `PUT /notes/:id` to replace (or mostly replace) fields.
- You can treat `PUT` as “update title/content if provided” for simplicity.

Validation thoughts:

- Check if ID is valid (same regex as before).
- Check `title` is string if provided.

### 2. Implement update & delete (60–70 min)

In `routes/notes.js`, add below existing routes:

**Update note – PUT /notes/:id**

```js
router.put("/:id", async (req, res) => {
  try {
    const { id } = req.params;

    if (!id.match(/^[0-9a-fA-F]{24}$/)) {
      return res.status(400).json({ error: "Invalid note ID format" });
    }

    const { title, content } = req.body;

    if (title !== undefined && typeof title !== "string") {
      return res
        .status(400)
        .json({ error: "Title must be a string if provided" });
    }
    if (content !== undefined && typeof content !== "string") {
      return res
        .status(400)
        .json({ error: "Content must be a string if provided" });
    }

    const updatedNote = await Note.findByIdAndUpdate(
      id,
      { title, content },
      { new: true, runValidators: true }
    );

    if (!updatedNote) {
      return res.status(404).json({ error: "Note not found" });
    }

    res.json(updatedNote);
  } catch (err) {
    console.error("Error updating note:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});
```

**Delete note – DELETE /notes/:id**

```js
router.delete("/:id", async (req, res) => {
  try {
    const { id } = req.params;

    if (!id.match(/^[0-9a-fA-F]{24}$/)) {
      return res.status(400).json({ error: "Invalid note ID format" });
    }

    const deletedNote = await Note.findByIdAndDelete(id);

    if (!deletedNote) {
      return res.status(404).json({ error: "Note not found" });
    }

    res.json({ message: "Note deleted", note: deletedNote });
  } catch (err) {
    console.error("Error deleting note:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});
```

Test with Postman:

- `PUT /notes/:id` with JSON body:

  ```json
  { "title": "Updated title", "content": "Updated content" }
  ```

- `DELETE /notes/:id` – then verify with `GET /notes`.

Try edge cases:

- Update / delete with a non-existent but valid ID (24-hex string).
- Provide wrong types (`title: 42`) to see validation error.

### 3. Reflection (5–10 min)

In `notes-day5.txt`:

- How did you handle invalid IDs vs non-existing notes?
- What Mongoose methods did you use to:
  - Find one by ID?
  - Update?
  - Delete?

---

## Day 6 – Querying, Filtering & Minor Enhancements

**Objectives:**
- Add simple filtering (e.g., search by title).
- Return notes in a useful sorted order.
- Optionally add a “pinned” or “important” field.

### 1. Concept (20–25 min)

Think about enhancements:

- Sort notes by `createdAt` descending (newest first) – you already did `sort({ createdAt: -1 })`.
- Add simple filter:
  - E.g., `GET /notes?search=keyword` – return notes whose title contains the keyword.
- Optional field:
  - `pinned: Boolean` default `false`; filter pinned notes.

### 2. Implement search filter (45–60 min)

Update `GET /notes` route in `routes/notes.js`:

```js
router.get("/", async (req, res) => {
  try {
    const { search } = req.query;
    const query = {};

    if (search) {
      // case-insensitive partial match on title
      query.title = { $regex: search, $options: "i" };
    }

    const notes = await Note.find(query).sort({ createdAt: -1 });
    res.json(notes);
  } catch (err) {
    console.error("Error fetching notes:", err);
    res.status(500).json({ error: "Internal server error" });
  }
});
```

Test:

- `GET /notes` – all notes.
- `GET /notes?search=first` – only notes whose title includes “first” (case insensitive).

### 3. Optional: add `pinned` field (20–30 min)

In `models/Note.js` schema:

```js
pinned: {
  type: Boolean,
  default: false,
},
```

Then you could:

- Support `pinned` in POST/PUT bodies.
- Add filter `GET /notes?pinned=true`.

```js
if (req.query.pinned === "true") {
  query.pinned = true;
} else if (req.query.pinned === "false") {
  query.pinned = false;
}
```

(You can combine with `search` if you like.)

### 4. Reflection (5–10 min)

In `notes-day6.txt`:

- How does `search` change the behavior of `GET /notes`?
- Why might filters like this be important for a real app?

---

## Day 7 – Cleanup, Documentation & Review

**Objectives:**
- Clean and comment your code.
- Document your Notes API.
- Reflect on MongoDB + Mongoose.

### 1. Code cleanup (20–30 min)

Go through `index.js`, `models/Note.js`, `routes/notes.js`:

- Add concise comments at the top of each file.

  Example in `routes/notes.js`:

  ```js
  // Routes for CRUD operations on Note documents.
  ```

- Ensure consistent error messages and status codes.
- Remove any unused routes (like `/test-create-note`) if still present.
- Check that all `try` blocks have `catch` with `console.error` and a `500` response.

If using Git:

```bash
git init
git add .
git commit -m "Notes API with MongoDB and Mongoose CRUD"
```

### 2. API documentation (30–40 min)

Create `README.md` (or `api-docs.md`) in `notes-api/`:

Document each endpoint:

- `POST /notes`
  - Body: `{ "title": "string (required)", "content": "string (optional)", "pinned": "boolean (optional)" }`
  - Responses:
    - `201` – created note.
    - `400` – validation error.

- `GET /notes`
  - Query params:
    - `search` (optional)
    - `pinned` (optional true/false)
  - Responses:
    - `200` – array of notes.

- `GET /notes/:id`
  - Responses:
    - `200` – note.
    - `400` – invalid ID format.
    - `404` – not found.

- `PUT /notes/:id`
  - Body: `{ "title": "...", "content": "...", "pinned": true/false }` (any subset).
  - Responses: `200`, `400`, `404`.

- `DELETE /notes/:id`
  - Responses: `200`, `400`, `404`.

Also write short “How to run” instructions:

```md
1. Clone repo or copy folder.
2. Create `.env` with `MONGODB_URI` and `PORT`.
3. Run `npm install`.
4. Run `npm start`.
5. Use Postman to hit `http://localhost:4000/notes`.
```

### 3. Weekly reflection (20–25 min)

In `notes-week7-summary.txt`:

- Do you understand:
  - How Mongoose schemas and models work?
  - How to perform basic CRUD with Mongoose (`create`, `find`, `findById`, `findByIdAndUpdate`, `findByIdAndDelete`)?
  - How to connect to MongoDB with a connection string?
- What was hardest this week:
  - Setting up Atlas?
  - Understanding ObjectId / ID formats?
  - Handling errors?
- One concrete improvement for next time:
  - More validation, better error messages, pagination for `GET /notes`, etc.

---

Next logical step (Week 8–9 in your overall plan):

- Learn React fundamentals and then build a simple React frontend that **consumes this Notes API** (list/create/edit/delete notes), preparing for your fully integrated full-stack project later.
