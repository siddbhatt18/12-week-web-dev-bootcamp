**Week 9 Theme:** React + APIs – `useEffect`, data fetching from your Notes API, and basic client-side routing.  
Assume ~2 hours/day. Work inside your existing React app (e.g., `week8-react-app`) or create a new `week9-notes-frontend/` with Vite.

By the end of the week you’ll have a **React frontend talking to your Week 7 Notes API**.

---

## Before Week 9 Starts (quick prep)

Make sure you have:

- Your **Notes API** from Week 7 running (e.g., `http://localhost:4000`).
  - Test `GET http://localhost:4000/notes` in browser/Postman to confirm.
- Your React app able to start (`npm run dev`).

You’ll need the API base URL (e.g., `http://localhost:4000`).

---

## Day 1 – `useEffect` & Basic Data Fetching in React

**Objectives:**
- Understand `useEffect`: when and why it runs.
- Fetch data from a public API in a React component.

### 1. Concept (25–30 min)

Learn:

- `useEffect` syntax:

  ```jsx
  import { useEffect } from "react";

  useEffect(() => {
    // side effect: data fetching, subscriptions, etc.
  }, []); // empty deps = runs once after first render
  ```

- The **dependency array**:
  - `[]` → run once on mount.
  - `[someValue]` → run when `someValue` changes.
- Why use useEffect:
  - To perform side effects (like `fetch`) after render.

### 2. Practice: fetch from a public API (60–70 min)

In your React project, create `src/components/RandomQuote.jsx`:

```jsx
import { useEffect, useState } from "react";

function RandomQuote() {
  const [quote, setQuote] = useState(null);
  const [status, setStatus] = useState("idle"); // idle | loading | success | error
  const [error, setError] = useState(null);

  async function fetchQuote() {
    setStatus("loading");
    setError(null);

    try {
      const res = await fetch("https://api.quotable.io/random");
      if (!res.ok) {
        throw new Error("Network response was not ok");
      }
      const data = await res.json();
      setQuote(data);
      setStatus("success");
    } catch (err) {
      console.error(err);
      setError("Failed to load quote.");
      setStatus("error");
    }
  }

  useEffect(() => {
    fetchQuote();
  }, []);

  return (
    <div className="card">
      <h2>Random Quote</h2>

      {status === "loading" && <p>Loading...</p>}
      {status === "error" && <p style={{ color: "red" }}>{error}</p>}

      {status === "success" && quote && (
        <>
          <blockquote>{quote.content}</blockquote>
          <p>— {quote.author}</p>
        </>
      )}

      <button onClick={fetchQuote} disabled={status === "loading"}>
        {status === "loading" ? "Loading..." : "New Quote"}
      </button>
    </div>
  );
}

export default RandomQuote;
```

Add `<RandomQuote />` to `App.jsx` to verify it works.

### 3. Reflection (5–10 min)

In `notes-day1.txt`:

- When does the `useEffect` in `RandomQuote` run?
- Why don’t we call `fetchQuote()` directly in the component body?

---

## Day 2 – Planning the Notes Frontend & API Helper

**Objectives:**
- Design the basic UI for your Notes frontend.
- Create a small API helper module to manage HTTP calls.

### 1. Plan the Notes UI (20–30 min)

In `notes-day2.txt`, sketch:

- Overall structure for Notes app:

  - `App`
    - (later) `Router` with routes:
      - `/` – Notes list + create form
      - `/notes/:id` – Note detail/edit page (optional this week)
  - Components:
    - `NotesPage` – main page
      - `NotesList`
      - `NoteForm` (for creating)
    - (optional later) `NoteDetail`, `EditNoteForm`

- Features for Week 9:
  - Display notes from API (`GET /notes`).
  - Create new note (`POST /notes`).
  - Delete note (`DELETE /notes/:id`).
  - Show loading and error states.

### 2. Create API helper (`api.js`) (60–70 min)

In `src/`, create `api.js`:

```jsx
const API_BASE_URL = "http://localhost:4000"; // adjust if different

async function request(path, options = {}) {
  const url = `${API_BASE_URL}${path}`;

  const defaultHeaders = {
    "Content-Type": "application/json",
  };

  const config = {
    headers: { ...defaultHeaders, ...(options.headers || {}) },
    ...options,
  };

  try {
    const res = await fetch(url, config);
    const contentType = res.headers.get("Content-Type") || "";

    let data = null;
    if (contentType.includes("application/json")) {
      data = await res.json();
    }

    if (!res.ok) {
      const errorMessage = (data && data.error) || res.statusText || "Error";
      throw new Error(errorMessage);
    }

    return data;
  } catch (err) {
    console.error("API request error:", err);
    throw err;
  }
}

export function getNotes() {
  return request("/notes");
}

export function createNote(note) {
  return request("/notes", {
    method: "POST",
    body: JSON.stringify(note),
  });
}

export function deleteNote(id) {
  return request(`/notes/${id}`, {
    method: "DELETE",
  });
}

// You can add updateNote later
export function updateNote(id, note) {
  return request(`/notes/${id}`, {
    method: "PUT",
    body: JSON.stringify(note),
  });
}
```

This centralizes API details.

### 3. Reflection (5–10 min)

In `notes-day2.txt`:

- Why is it useful to have a central `api.js` instead of calling `fetch` everywhere?
- What base URL did you set for your API?

---

## Day 3 – Notes List: Fetch & Display from Your API

**Objectives:**
- Fetch notes from your own backend API.
- Display them in a list with loading/error states.

### 1. Concept (20–25 min)

Think about:

- Where to fetch notes:
  - In `NotesPage` (top-level notes container).
- State needed:
  - `notes`, `loading`, `error`.

### 2. Implement `NotesPage` (60–70 min)

Create `src/components/NotesPage.jsx`:

```jsx
import { useEffect, useState } from "react";
import { getNotes } from "../api";

function NotesPage() {
  const [notes, setNotes] = useState([]);
  const [status, setStatus] = useState("idle"); // idle | loading | success | error
  const [error, setError] = useState(null);

  useEffect(() => {
    async function loadNotes() {
      setStatus("loading");
      setError(null);

      try {
        const data = await getNotes();
        setNotes(data);
        setStatus("success");
      } catch (err) {
        setError(err.message || "Failed to load notes");
        setStatus("error");
      }
    }

    loadNotes();
  }, []);

  return (
    <div className="card">
      <h2>Notes</h2>

      {status === "loading" && <p>Loading notes...</p>}
      {status === "error" && (
        <p style={{ color: "red" }}>Error: {error}</p>
      )}

      {status === "success" && notes.length === 0 && <p>No notes yet.</p>}

      {status === "success" && notes.length > 0 && (
        <ul>
          {notes.map((note) => (
            <li key={note._id}>
              <strong>{note.title}</strong>
              {note.content && <p>{note.content}</p>}
              <small>
                Created: {new Date(note.createdAt).toLocaleString()}
              </small>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}

export default NotesPage;
```

In `App.jsx`, temporarily replace your dashboard or add:

```jsx
import NotesPage from "./components/NotesPage";

function App() {
  return (
    <div className="app">
      <h1>Notes Frontend</h1>
      <NotesPage />
    </div>
  );
}

export default App;
```

Run both servers:

- Backend: `npm start` in `notes-api`.
- Frontend: `npm run dev` in React app.

Confirm notes load correctly.

### 3. Reflection (5–10 min)

In `notes-day3.txt`:

- How did you handle loading and errors in `NotesPage`?
- What happens if your backend is not running?

---

## Day 4 – Creating Notes from the Frontend

**Objectives:**
- Add a form to create new notes via `POST /notes`.
- Refresh the list after creating a note.

### 1. Concept (20–25 min)

Consider:

- Where should the form live?
  - In `NotesPage` (for now).
- Data flow:
  - User submits → call `createNote` → on success, update `notes` state.

### 2. Implement `NoteForm` & integrate with `NotesPage` (60–70 min)

Create `src/components/NoteForm.jsx`:

```jsx
import { useState } from "react";

function NoteForm({ onCreate }) {
  const [title, setTitle] = useState("");
  const [content, setContent] = useState("");
  const [submitting, setSubmitting] = useState(false);
  const [error, setError] = useState(null);

  async function handleSubmit(e) {
    e.preventDefault();
    const trimmedTitle = title.trim();
    const trimmedContent = content.trim();

    if (!trimmedTitle) {
      setError("Title is required.");
      return;
    }

    setSubmitting(true);
    setError(null);

    try {
      await onCreate({ title: trimmedTitle, content: trimmedContent });
      setTitle("");
      setContent("");
    } catch (err) {
      setError(err.message || "Failed to create note.");
    } finally {
      setSubmitting(false);
    }
  }

  return (
    <form onSubmit={handleSubmit} className="note-form">
      <h3>Create Note</h3>
      {error && <p style={{ color: "red" }}>{error}</p>}
      <div>
        <input
          type="text"
          placeholder="Title *"
          value={title}
          onChange={(e) => setTitle(e.target.value)}
          disabled={submitting}
        />
      </div>
      <div>
        <textarea
          placeholder="Content (optional)"
          value={content}
          onChange={(e) => setContent(e.target.value)}
          disabled={submitting}
        />
      </div>
      <button type="submit" disabled={submitting}>
        {submitting ? "Creating..." : "Add Note"}
      </button>
    </form>
  );
}

export default NoteForm;
```

Update `NotesPage.jsx`:

```jsx
import { useEffect, useState } from "react";
import { getNotes, createNote, deleteNote } from "../api"; // deleteNote later
import NoteForm from "./NoteForm";

function NotesPage() {
  const [notes, setNotes] = useState([]);
  const [status, setStatus] = useState("idle");
  const [error, setError] = useState(null);

  async function loadNotes() {
    setStatus("loading");
    setError(null);

    try {
      const data = await getNotes();
      setNotes(data);
      setStatus("success");
    } catch (err) {
      setError(err.message || "Failed to load notes");
      setStatus("error");
    }
  }

  useEffect(() => {
    loadNotes();
  }, []);

  async function handleCreate(noteData) {
    const newNote = await createNote(noteData);
    // Prepend new note
    setNotes((prev) => [newNote, ...prev]);
  }

  return (
    <div className="card">
      <h2>Notes</h2>
      <NoteForm onCreate={handleCreate} />

      {status === "loading" && <p>Loading notes...</p>}
      {status === "error" && (
        <p style={{ color: "red" }}>Error: {error}</p>
      )}

      {status === "success" && notes.length === 0 && <p>No notes yet.</p>}

      {status === "success" && notes.length > 0 && (
        <ul>
          {notes.map((note) => (
            <li key={note._id}>
              <strong>{note.title}</strong>
              {note.content && <p>{note.content}</p>}
              <small>
                Created: {new Date(note.createdAt).toLocaleString()}
              </small>
            </li>
          ))}
        </ul>
      )}
    </div>
  );
}

export default NotesPage;
```

Test: create some notes and see the list update immediately.

### 3. Reflection (5–10 min)

In `notes-day4.txt`:

- Why does `handleCreate` live in `NotesPage` instead of inside `NoteForm`?
- What happens if the `createNote` API call fails?

---

## Day 5 – Deleting Notes & Basic UX Improvements

**Objectives:**
- Add delete functionality via `DELETE /notes/:id`.
- Improve UX (confirm delete, disabled buttons states).

### 1. Concept (20–25 min)

Think about:

- Event handler pattern:
  - Pass a callback to each list item.
- Mutating notes state:
  - Filter out deleted note by `_id`.

### 2. Implement delete (60–70 min)

In `NotesPage.jsx`, add a delete handler:

```jsx
import { getNotes, createNote, deleteNote } from "../api";
// ...

function NotesPage() {
  // existing state/hooks

  async function handleDelete(id) {
    // Optional: confirm
    const ok = window.confirm("Delete this note?");
    if (!ok) return;

    try {
      await deleteNote(id);
      setNotes((prev) => prev.filter((note) => note._id !== id));
    } catch (err) {
      alert(err.message || "Failed to delete note.");
    }
  }

  // in JSX where you map notes:
  {status === "success" && notes.length > 0 && (
    <ul>
      {notes.map((note) => (
        <li key={note._id}>
          <strong>{note.title}</strong>
          {note.content && <p>{note.content}</p>}
          <small>
            Created: {new Date(note.createdAt).toLocaleString()}
          </small>
          <div>
            <button onClick={() => handleDelete(note._id)}>
              Delete
            </button>
          </div>
        </li>
      ))}
    </ul>
  )}
}
```

Test deleting notes and confirm they disappear.

### 3. Small UX tweaks (20–25 min)

- Add simple CSS:
  - Space between list items.
  - Style delete button (e.g., red).
  - Distinguish the form section with a border or background.

- Consider:
  - Show “Deleting…” or disable delete button while request is running (optional).

### 4. Reflection (5–10 min)

In `notes-day5.txt`:

- Describe the flow for deleting a note from click to updated UI.
- How did you update state after a delete?

---

## Day 6 – React Router: Multi-Page Feel (List + Detail)

**Objectives:**
- Add basic client-side routing with `react-router-dom`.
- Create a simple detail page for a note (`/notes/:id`).

### 1. Install React Router (10–15 min)

In your React project:

```bash
npm install react-router-dom
```

### 2. Setup routing (45–60 min)

Update `main.jsx`:

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { BrowserRouter } from "react-router-dom";
import App from "./App";
import "./index.css";

ReactDOM.createRoot(document.getElementById("root")).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
);
```

Update `App.jsx`:

```jsx
import { Routes, Route, Link } from "react-router-dom";
import NotesPage from "./components/NotesPage";
import RandomQuote from "./components/RandomQuote"; // or any other component
import NoteDetailPage from "./components/NoteDetailPage"; // you'll create this

function App() {
  return (
    <div className="app">
      <header className="app-header">
        <h1>Notes App</h1>
        <nav>
          <Link to="/">Notes</Link>{" "}
          <Link to="/quote">Random Quote</Link>
        </nav>
      </header>

      <main className="app-main">
        <Routes>
          <Route path="/" element={<NotesPage />} />
          <Route path="/quote" element={<RandomQuote />} />
          <Route path="/notes/:id" element={<NoteDetailPage />} />
        </Routes>
      </main>
    </div>
  );
}

export default App;
```

### 3. Note Detail Page (basic) (30–40 min)

In `src/components/NoteDetailPage.jsx`:

```jsx
import { useEffect, useState } from "react";
import { useParams, Link } from "react-router-dom";
import { getNoteById, updateNote } from "../api";

function NoteDetailPage() {
  const { id } = useParams();
  const [note, setNote] = useState(null);
  const [status, setStatus] = useState("idle");
  const [error, setError] = useState(null);

  useEffect(() => {
    async function load() {
      setStatus("loading");
      setError(null);
      try {
        const data = await getNoteById(id);
        setNote(data);
        setStatus("success");
      } catch (err) {
        setError(err.message || "Failed to load note.");
        setStatus("error");
      }
    }
    load();
  }, [id]);

  if (status === "loading") return <p>Loading note...</p>;
  if (status === "error")
    return (
      <div>
        <p style={{ color: "red" }}>Error: {error}</p>
        <Link to="/">Back to notes</Link>
      </div>
    );

  if (!note) return null;

  return (
    <div className="card">
      <h2>{note.title}</h2>
      {note.content && <p>{note.content}</p>}
      <small>
        Created: {new Date(note.createdAt).toLocaleString()}
      </small>
      <div style={{ marginTop: "1rem" }}>
        <Link to="/">← Back to notes</Link>
      </div>
    </div>
  );
}

export default NoteDetailPage;
```

Add helper functions in `api.js`:

```jsx
export function getNoteById(id) {
  return request(`/notes/${id}`);
}
```

In `NotesPage`, wrap title with a `Link`:

```jsx
import { Link } from "react-router-dom";
// ...
<li key={note._id}>
  <strong>
    <Link to={`/notes/${note._id}`}>{note.title}</Link>
  </strong>
  {/* rest */}
</li>
```

Test:
- Click a note title → should navigate to detail page, show note, and link back.

### 4. Reflection (5–10 min)

In `notes-day6.txt`:

- How does `BrowserRouter` + `Routes` + `Route` work conceptually?
- What hook did you use to read the URL param (`id`)?

---

## Day 7 – Cleanup, Comments, & Review

**Objectives:**
- Clean up, comment key parts of your notes frontend.
- Reflect on React + API integration and routing.

### 1. Code cleanup & comments (25–30 min)

- In `api.js`, `NotesPage.jsx`, `NoteForm.jsx`, `NoteDetailPage.jsx`:
  - Add short comments explaining the main responsibility of each file.
- Check for:
  - Duplicate logic (e.g., error handling) and see if you could simplify later.
  - Unused imports or variables.
- Make sure your UI:
  - Shows clear messages for loading and errors.
  - Has basic but consistent styling.

If using Git:

```bash
git add .
git commit -m "Connect React notes frontend to Notes API with routing"
```

### 2. Manual end-to-end test (20–25 min)

With backend and frontend running:

- Load `/`:
  - See list of notes (or “No notes yet”).
- Create new note:
  - Appears immediately in list.
  - Persists after page refresh.
- Click note title:
  - Navigates to `/notes/:id`.
  - Shows correct details.
- Delete note:
  - Disappears from list.
  - Confirm via backend (GET `/notes` in Postman or browser).
- Navigate between `/` and `/quote` using navbar.

Note any bugs or rough edges in a `bugs-or-todos.txt` file.

### 3. Weekly reflection (20–25 min)

In `notes-week9-summary.txt`, answer:

- Do you understand:
  - How to use `useEffect` for data fetching?
  - How to integrate a React frontend with a REST API?
  - Basic routing with `react-router-dom` (routes, `Link`, `useParams`)?
- What parts are still confusing (e.g., dependency arrays, handling multiple async calls, routing configuration)?
- One clear goal for Week 10:
  - e.g., “Add authentication to my backend and protect some routes,”
  - “Learn how to manage auth state in React and call protected endpoints,”
  - or “Improve error handling and show global notifications.”

---

If you’d like next, I can create a **Week 10 day-by-day plan** focused on authentication (JWT), protected backend routes, and managing auth + protected pages in React, moving toward your full-stack mini SaaS app.
