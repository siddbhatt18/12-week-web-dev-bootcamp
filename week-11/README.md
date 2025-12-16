**Week 11 Theme:** Rounding out your mini SaaS app – features, UX, basic analytics, and refactoring.  
Assume ~2 hours/day. You’ll keep working in your existing **auth-enabled Notes (or Tasks) app**:  
- Backend: Node/Express/Mongo (with JWT auth from Week 10)  
- Frontend: React app (with routing + AuthContext)

By the end of the week you’ll have:
- A more polished UI
- Small “analytics” (stats/filters)
- Cleaner code structure (reusable hooks/components)

---

## Day 1 – Feature Audit & Improvement Plan

**Objectives:**
- Review what you have.
- Decide what to improve/extend.
- Create a small, realistic feature roadmap for Week 11.

### 1. Quick review (20–30 min)

Walk through your app as a user:

Backend:
- Auth: `/auth/register`, `/auth/login` work?
- Notes/tasks: `/notes` CRUD with `user` ownership, filters, etc.

Frontend:
- Can log in / log out?
- View notes?
- Create / delete (and maybe edit) notes?
- Navigation and error states?

Write in `week11/notes-day1.txt`:
- Current features:
  - Auth: yes/no
  - CRUD: which operations supported?
  - Filters/search: yes/no
  - Stats: yes/no
- Pain points:
  - UI layout, loading states, error messages, etc.

### 2. Choose 2–3 target improvements (30–40 min)

Pick from ideas like:

- **Feature:** Editing notes directly from UI (if not done).
- **Feature:** Search/filter UI for notes.
- **Analytics:** Show total notes, last updated time, maybe “notes this week”.
- **UX:** Better loading spinners, error banners, empty states.
- **Code quality:** Extract reusable components or create a custom hook for data fetching.

Write **Week 11 goals** in `notes-day1.txt`, e.g.:

- Goal 1: Add client-side search bar & filter for notes.
- Goal 2: Add simple stats (total notes, pinned vs unpinned).
- Goal 3: Clean up UI/layout and extract at least one reusable component.

### 3. Create a TODO list (20–30 min)

Make `week11/todo.md`:

- `[ ] Add search bar and filter UI to NotesPage`
- `[ ] Add stats component showing total notes and pinned count`
- `[ ] Improve styling of header / cards`
- `[ ] Extract reusable Button or Card component`
- `[ ] (Optional) Add edit-note functionality in the detail or list view`

You’ll chip away at these during the week.

---

## Day 2 – Client-Side Search/Filter UI

**Objectives:**
- Add a search box & basic filter controls on the frontend.
- Perform client-side filtering on your `notes` array.

*(You may already support `?search` on the backend; this day focuses on the UI and basic client-side behavior first.)*

### 1. Add search + filter controls (45–60 min)

In `NotesPage.jsx`:

- Add state:

```jsx
const [searchTerm, setSearchTerm] = useState("");
const [showPinnedOnly, setShowPinnedOnly] = useState(false);
```

- Above the notes list in the JSX, add controls:

```jsx
<div className="notes-controls">
  <input
    type="text"
    placeholder="Search notes by title..."
    value={searchTerm}
    onChange={(e) => setSearchTerm(e.target.value)}
  />
  <label>
    <input
      type="checkbox"
      checked={showPinnedOnly}
      onChange={(e) => setShowPinnedOnly(e.target.checked)}
    />
    Show pinned only
  </label>
</div>
```

### 2. Apply client-side filtering (45–60 min)

- Before you render `notes.map`, derive `filteredNotes`:

```jsx
const filteredNotes = notes.filter((note) => {
  const matchesSearch =
    !searchTerm ||
    note.title.toLowerCase().includes(searchTerm.toLowerCase());

  const matchesPinned = !showPinnedOnly || note.pinned;

  return matchesSearch && matchesPinned;
});
```

- Render `filteredNotes` instead of `notes`:

```jsx
{status === "success" && filteredNotes.length === 0 && (
  <p>No notes match your filters.</p>
)}

{status === "success" && filteredNotes.length > 0 && (
  <ul>
    {filteredNotes.map((note) => (
      // ...
    ))}
  </ul>
)}
```

- Optionally style `.notes-controls` in your CSS (spacing, layout).

### 3. Reflection (5–10 min)

In `notes-day2.txt`:
- How does changing `searchTerm` or `showPinnedOnly` affect the rendered list?
- What’s the difference between client-side filtering and server-side filtering?

---

## Day 3 – Simple Stats/Analytics Component

**Objectives:**
- Compute simple derived stats from the notes array.
- Display them in a separate, reusable component.

### 1. Decide on stats (15–20 min)

Ideas:
- Total number of notes.
- Number of pinned notes.
- Last created note’s date/time.
- (Optional) Notes created today/this week (simple approximation).

Write chosen stats in `notes-day3.txt`.

### 2. Implement `NotesStats` component (45–60 min)

Create `src/components/NotesStats.jsx`:

```jsx
function NotesStats({ notes }) {
  const total = notes.length;
  const pinnedCount = notes.filter((n) => n.pinned).length;

  let lastCreated = null;
  if (notes.length > 0) {
    const sorted = [...notes].sort(
      (a, b) => new Date(b.createdAt) - new Date(a.createdAt)
    );
    lastCreated = sorted[0].createdAt;
  }

  return (
    <div className="card">
      <h3>Notes Stats</h3>
      <p>Total notes: {total}</p>
      <p>Pinned notes: {pinnedCount}</p>
      {lastCreated && (
        <p>
          Last note created:{" "}
          {new Date(lastCreated).toLocaleString()}
        </p>
      )}
      {total === 0 && <p>No data yet. Create your first note!</p>}
    </div>
  );
}

export default NotesStats;
```

In `NotesPage.jsx`, import and render it:

```jsx
import NotesStats from "./NotesStats";

function NotesPage() {
  // ...
  return (
    <div className="notes-page">
      <div className="card">
        <h2>Notes</h2>
        <NoteForm onCreate={handleCreate} />
        {/* controls + list */}
      </div>

      <NotesStats notes={notes} />
    </div>
  );
}
```

Consider layout: maybe `.notes-page` is a grid or flex container with main notes area + sidebar stats.

### 3. Optional: stats based on filters (15–20 min)

If you want, pass `filteredNotes` instead of all `notes` into `NotesStats` to show stats for the **current view**.

### 4. Reflection (5–10 min)

In `notes-day3.txt`:
- What derived values are you computing?  
- Why did you not store these stats in state?

---

## Day 4 – UI Polish & Component Reuse

**Objectives:**
- Improve the look & feel of your app.
- Extract reusable UI components (e.g., `Card`, `Button`).

### 1. Extract a `Card` component (30–40 min)

Create `src/components/ui/Card.jsx`:

```jsx
function Card({ children, className = "" }) {
  return <div className={`card ${className}`}>{children}</div>;
}

export default Card;
```

Update components (`NotesPage`, `NotesStats`, `LoginPage`, etc.) to use `<Card>`:

Example in `NotesStats`:

```jsx
import Card from "./ui/Card";

function NotesStats({ notes }) {
  // ...
  return (
    <Card>
      <h3>Notes Stats</h3>
      {/* ... */}
    </Card>
  );
}
```

This centralizes card styling and keeps components cleaner.

### 2. Improve layout & typography (40–50 min)

In your main CSS (e.g., `index.css`):

- Ensure consistent font and colors.
- Make `.app-main` or `.notes-page` use a **responsive layout**:

```css
.app-main {
  max-width: 1000px;
  margin: 0 auto;
  padding: 1rem;
}

.notes-page {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 1rem;
}

@media (max-width: 768px) {
  .notes-page {
    grid-template-columns: 1fr;
  }
}
```

- Style buttons consistently:

```css
button {
  padding: 0.4rem 0.8rem;
  border-radius: 4px;
  border: none;
  cursor: pointer;
}

button:hover {
  opacity: 0.9;
}

button.danger {
  background-color: #e74c3c;
  color: white;
}
```

- Add `.notes-controls` CSS for spacing.

### 3. Reflection (5–10 min)

In `notes-day4.txt`:
- What did extracting `Card` (and possibly button styling) do for your code readability?
- Do you now have a recognizable “design system” (even a tiny one)?

---

## Day 5 – Edit/Update Feature (If Not Done) or Custom Hook

**Objectives (choose path A or B):**

- **Path A:** Implement note editing on the frontend using your existing `PUT /notes/:id` backend.  
- **Path B:** If editing is already implemented, create a custom React hook for data fetching (`useNotes`) to clean up `NotesPage`.

### Path A – Implement edit/update (60–80 min)

1. **Decide edit UX:**
   - Inline editing in the list?  
   - Or navigate to `NoteDetailPage` with an edit form?

2. **Simple inline editing idea in `NotesPage`:**
   - Add state:

   ```jsx
   const [editingId, setEditingId] = useState(null);
   const [editTitle, setEditTitle] = useState("");
   const [editContent, setEditContent] = useState("");
   ```

   - When clicking “Edit” on a note, set these states and show inputs:

   ```jsx
   function startEditing(note) {
     setEditingId(note._id);
     setEditTitle(note.title);
     setEditContent(note.content || "");
   }
   ```

3. **Render logic inside `notes.map`:**

   ```jsx
   {notes.map((note) => (
     <li key={note._id}>
       {editingId === note._id ? (
         <>
           <input
             value={editTitle}
             onChange={(e) => setEditTitle(e.target.value)}
           />
           <textarea
             value={editContent}
             onChange={(e) => setEditContent(e.target.value)}
           />
           <button onClick={() => saveEdit(note._id)}>Save</button>
           <button onClick={() => setEditingId(null)}>Cancel</button>
         </>
       ) : (
         <>
           <strong>{note.title}</strong>
           {note.content && <p>{note.content}</p>}
           <button onClick={() => startEditing(note)}>Edit</button>
           <button
             className="danger"
             onClick={() => handleDelete(note._id)}
           >
             Delete
           </button>
         </>
       )}
     </li>
   ))}
   ```

4. **Implement `saveEdit` using `updateNote` from `api.js`:**

   ```jsx
   async function saveEdit(id) {
     const trimmedTitle = editTitle.trim();
     if (!trimmedTitle) {
       alert("Title is required");
       return;
     }

     try {
       const updated = await updateNote(
         id,
         { title: trimmedTitle, content: editContent.trim() },
         token
       );
       setNotes((prev) =>
         prev.map((note) => (note._id === id ? updated : note))
       );
       setEditingId(null);
     } catch (err) {
       alert(err.message || "Failed to update note");
     }
   }
   ```

5. Test: edit, save, confirm backend data and UI sync.

---

### Path B – Create `useNotes` hook (if edit already done) (60–80 min)

Create `src/hooks/useNotes.js`:

```jsx
import { useEffect, useState } from "react";
import { getNotes, createNote, deleteNote, updateNote } from "../api";
import { useAuth } from "../AuthContext";

export function useNotes() {
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

    async function load() {
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
    load();
  }, [token, isAuthenticated]);

  async function create(noteData) {
    const newNote = await createNote(noteData, token);
    setNotes((prev) => [newNote, ...prev]);
  }

  async function remove(id) {
    await deleteNote(id, token);
    setNotes((prev) => prev.filter((n) => n._id !== id));
  }

  async function update(id, noteData) {
    const updated = await updateNote(id, noteData, token);
    setNotes((prev) => prev.map((n) => (n._id === id ? updated : n)));
  }

  return {
    notes,
    status,
    error,
    create,
    remove,
    update,
  };
}
```

Then in `NotesPage.jsx`:

```jsx
import { useNotes } from "../hooks/useNotes";

function NotesPage() {
  const { notes, status, error, create, remove, update } = useNotes();
  // drop local notes/status/error
  // call create/remove/update instead of handleCreate/handleDelete etc.
}
```

This simplifies `NotesPage` and centralizes logic.

---

### Reflection (5–10 min)

In `notes-day5.txt`:
- If you did edit: what was hardest about keeping UI state in sync with API?  
- If you did hook: how did `useNotes` reduce duplication?

---

## Day 6 – Error Handling & Empty/Edge States

**Objectives:**
- Improve user feedback for network/API errors.
- Ensure clean behavior for empty data, invalid routes, and auth issues.

### 1. Global error patterns (25–30 min)

Walk through the app and identify:

- Where do you show errors? Only in small inline text? Alerts?  
- What happens if:
  - Backend is down?
  - Token is invalid or expired (backend returns 401)?
  - No notes exist?

Decide improvements, e.g.:

- A simple `ErrorMessage` component.
- Handling 401s by logging out and redirecting to login.

### 2. Implement `ErrorMessage` component (30–40 min)

Create `src/components/ui/ErrorMessage.jsx`:

```jsx
function ErrorMessage({ message }) {
  if (!message) return null;
  return (
    <div className="error-message">
      {message}
    </div>
  );
}

export default ErrorMessage;
```

CSS:

```css
.error-message {
  background-color: #fdecea;
  color: #c0392b;
  padding: 0.5rem 0.75rem;
  border-radius: 4px;
  margin-bottom: 0.5rem;
}
```

Use it in `NotesPage`, `LoginPage`, `NoteForm` instead of raw `<p style={{ color: "red" }}>`.

### 3. Optional: centralized 401 handling (20–25 min)

In `api.js`, when a request throws an error, you might:

- Check if error message or status code indicates 401, and then:
  - Optionally expose a way to log out globally (this is more advanced; you could defer).

For now, just note in `notes-day6.txt` that 401s may require better UX later.

### 4. Reflection (5–10 min)

In `notes-day6.txt`:
- How does having a dedicated `ErrorMessage` component help?
- What remaining edge cases do you see in your app?

---

## Day 7 – Light Refactor, Documentation & Next Steps

**Objectives:**
- Do a quick refactor pass.
- Document your app’s features and architecture.
- Reflect on what you’ve built.

### 1. Code cleanup/refactor pass (30–40 min)

Go through key files:

- Backend:
  - Check route structure, middleware, models.
  - Ensure no unused imports, stray debug `console.log`s.
- Frontend:
  - `App.jsx`, `AuthContext.jsx`, `NotesPage.jsx`, `NoteForm.jsx`, `NotesStats.jsx`, `LoginPage.jsx`, `RandomQuote.jsx`.
  - Look for:
    - Very long components that could be split.
    - Repetitive code for input fields or buttons.
    - Inconsistent naming.

Make 1–2 small refactor improvements only; avoid major rewrites.

If using Git:

```bash
git add .
git commit -m "Week 11 polish: filters, stats, UI polish, refactor"
```

### 2. Write a short technical overview (30–40 min)

Create `week11/architecture-notes.md` (or extend your repo README):

Document:

- **Tech stack:**
  - Frontend: React, React Router, Context, etc.
  - Backend: Node, Express, MongoDB, Mongoose, JWT.
- **Features:**
  - Auth flow (register/login, JWT, protected routes).
  - Notes CRUD + user-specific ownership.
  - Search, filters, pinned notes (if any).
  - Stats panel.
- **Structure:**
  - Backend folders: `models/`, `routes/`, `middleware/`.
  - Frontend folders: `components/`, `hooks/`, `context/` (or similar).
- **How to run:**
  - Backend: `npm install`, `npm start` with `.env`.
  - Frontend: `npm install`, `npm run dev`, base API URL.

This will be useful for yourself and for any future portfolio.

### 3. Weekly reflection & prep for Week 12 (20–25 min)

In `notes-week11-summary.txt`:

- What did you add/improve this week?
- What parts of your app now feel:
  - **Solid** (you can easily explain/modify).
  - **Fragile/unclear** (you’re not fully confident).
- Are you comfortable with:
  - Extending React components with new features?
  - Creating derived data and basic analytics?
  - Extracting reusable components/hooks?
- For Week 12 (Deployment & final polish), define 2–3 clear tasks:
  - e.g., “Deploy backend to Render/Railway,”
  - “Deploy frontend to Netlify/Vercel and connect to backend,”
  - “Write a polished README with screenshots and live demo link.”

---

If you’d like next, I can generate a **Week 12 day‑by‑day plan** focused on:

- Deploying backend + frontend,
- Handling environment variables in production,
- Final polish and preparing this project as a portfolio piece.
