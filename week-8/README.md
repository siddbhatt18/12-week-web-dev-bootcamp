**Week 8 Theme:** React fundamentals – components, props, state, events, and basic data flow.  
Assume ~2 hours/day. Work in a `week8/` folder. You’ll finish with a small multi-component React app (no backend yet).

Tech choice: **React + Vite** (fast, modern). You can use Create React App if you prefer; I’ll show Vite.

---

## Day 1 – React Mental Model & Project Setup

**Objectives:**
- Understand what React is and why it’s used.
- Set up your first React project with Vite.
- Render your first component.

### 1. Concept (25–30 min)

Learn (read/watch briefly, take notes):

- What React is:
  - A library for building user interfaces.
  - Component-based, declarative.
- Key ideas:
  - **Component** = a function that returns JSX.
  - **JSX** = HTML-like syntax in JavaScript.
  - React renders a **virtual DOM** and updates only what changes.
- One-way data flow: parent → child via **props**.

Write in `notes-day1.txt`:
- “A React component is…” in your own words.
- One difference between React and vanilla DOM manipulation.

### 2. Setup with Vite (45–60 min)

In terminal (from your main dev folder):

```bash
npm create vite@latest week8-react-app -- --template react
cd week8-react-app
npm install
npm run dev
```

- Open the URL shown (usually `http://localhost:5173`).
- You should see the starter page.

Open the project in your editor:
- `src/main.jsx` (entry point).
- `src/App.jsx` (main component).

Simplify `App.jsx` to something like:

```jsx
function App() {
  return (
    <div>
      <h1>My First React App</h1>
      <p>Week 8: Learning React fundamentals.</p>
    </div>
  );
}

export default App;
```

Make sure the UI updates in the browser.

### 3. Reflection (5–10 min)

In `notes-day1.txt`:
- What files seem most important so far (`main.jsx`, `App.jsx`)?
- How do you start the dev server?

---

## Day 2 – Components & Props

**Objectives:**
- Create multiple components.
- Pass data via props.

### 1. Concept (25–30 min)

Learn:
- Function components:

  ```jsx
  function Greeting(props) {
    return <h2>Hello, {props.name}</h2>;
  }
  ```

- Destructuring props:

  ```jsx
  function Greeting({ name }) {
    return <h2>Hello, {name}</h2>;
  }
  ```

- Component composition: nesting components inside `App`.

### 2. Practice: small profile card (60–70 min)

In `src/`, create `ProfileCard.jsx`:

```jsx
function ProfileCard({ name, role, bio }) {
  return (
    <div className="profile-card">
      <h2>{name}</h2>
      <h3>{role}</h3>
      <p>{bio}</p>
    </div>
  );
}

export default ProfileCard;
```

In `App.jsx`:

```jsx
import ProfileCard from "./ProfileCard";

function App() {
  return (
    <div>
      <h1>Team Profiles</h1>
      <ProfileCard
        name="Alex Developer"
        role="Full Stack Learner"
        bio="Learning React and Node to build full stack apps."
      />
      <ProfileCard
        name="Sam Designer"
        role="UI/UX Designer"
        bio="Loves clean interfaces and user-centered design."
      />
    </div>
  );
}

export default App;
```

Style quickly in `src/index.css` or `App.css` (if present):
- Add `.profile-card` with border, padding, margin.

Experiment:
- Add a `skills` prop (array) and render it in a list inside `ProfileCard`.

### 3. Reflection (5–10 min)

In `notes-day2.txt`:
- How do you pass data from a parent to a child component?
- How does JSX differ from plain HTML (e.g., `className` vs `class`)?

---

## Day 3 – State & Event Handling

**Objectives:**
- Use `useState` to track component state.
- Handle events like `onClick`.

### 1. Concept (25–30 min)

Learn:
- `useState` hook:

  ```jsx
  import { useState } from "react";

  function Counter() {
    const [count, setCount] = useState(0);

    return (
      <div>
        <p>Count: {count}</p>
        <button onClick={() => setCount(count + 1)}>Increment</button>
      </div>
    );
  }
  ```

- Key ideas:
  - State is **internal data** that can change over time.
  - Changing state re-renders the component.

### 2. Practice: Counter & Toggle components (60–70 min)

In `src/Counter.jsx`:

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  function increment() {
    setCount(count + 1);
  }

  function decrement() {
    setCount(count - 1);
  }

  function reset() {
    setCount(0);
  }

  return (
    <div className="card">
      <h2>Counter</h2>
      <p>Current count: {count}</p>
      <button onClick={decrement}>-</button>
      <button onClick={increment}>+</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}

export default Counter;
```

In `src/ToggleMessage.jsx`:

```jsx
import { useState } from "react";

function ToggleMessage() {
  const [isVisible, setIsVisible] = useState(true);

  function toggle() {
    setIsVisible(!isVisible);
  }

  return (
    <div className="card">
      <h2>Toggle Message</h2>
      <button onClick={toggle}>
        {isVisible ? "Hide message" : "Show message"}
      </button>
      {isVisible && <p>This message can be toggled.</p>}
    </div>
  );
}

export default ToggleMessage;
```

Update `App.jsx`:

```jsx
import Counter from "./Counter";
import ToggleMessage from "./ToggleMessage";
import ProfileCard from "./ProfileCard";

function App() {
  return (
    <div>
      <h1>React Basics Playground</h1>
      <Counter />
      <ToggleMessage />
      <ProfileCard
        name="You"
        role="React Beginner"
        bio="Practicing state and events."
      />
    </div>
  );
}

export default App;
```

### 3. Reflection (5–10 min)

In `notes-day3.txt`:
- What is state used for in React?
- When does React re-render a component?

---

## Day 4 – Controlled Forms & Lists

**Objectives:**
- Build a controlled input (React manages the value).
- Render lists of items from state and arrays.

### 1. Concept (25–30 min)

Learn:
- Controlled components:

  ```jsx
  const [text, setText] = useState("");

  <input value={text} onChange={(e) => setText(e.target.value)} />
  ```

- Rendering lists with `.map`:

  ```jsx
  const items = ["a", "b", "c"];
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
  ```

- Keys: use something stable (like id) when possible.

### 2. Practice: simple notes input (60–70 min)

Create `src/NotesList.jsx`:

```jsx
import { useState } from "react";

function NotesList() {
  const [notes, setNotes] = useState([]);
  const [input, setInput] = useState("");

  function handleSubmit(e) {
    e.preventDefault();
    const trimmed = input.trim();
    if (!trimmed) return;

    const newNote = {
      id: Date.now(),
      text: trimmed,
    };
    setNotes([newNote, ...notes]); // newest on top
    setInput("");
  }

  function handleDelete(id) {
    setNotes(notes.filter((note) => note.id !== id));
  }

  return (
    <div className="card">
      <h2>Local Notes (Frontend Only)</h2>
      <form onSubmit={handleSubmit}>
        <input
          placeholder="Write a note..."
          value={input}
          onChange={(e) => setInput(e.target.value)}
        />
        <button type="submit">Add</button>
      </form>

      <ul>
        {notes.map((note) => (
          <li key={note.id}>
            {note.text}{" "}
            <button onClick={() => handleDelete(note.id)}>Delete</button>
          </li>
        ))}
      </ul>

      {notes.length === 0 && <p>No notes yet.</p>}
    </div>
  );
}

export default NotesList;
```

Add to `App.jsx`:

```jsx
import NotesList from "./NotesList";

function App() {
  return (
    <div>
      <h1>React Basics Playground</h1>
      <Counter />
      <ToggleMessage />
      <NotesList />
      {/* ProfileCard... */}
    </div>
  );
}
```

### 3. Reflection (5–10 min)

In `notes-day4.txt`:
- What is a “controlled input”?
- How do you render arrays of items in React?

---

## Day 5 – App Structure & Simple “Mini Dashboard” Design

**Objectives:**
- Organize components logically.
- Plan and build a small “React mini dashboard” app (single page, multiple sections).

### 1. Plan mini dashboard (20–30 min)

You’ll create a **small React dashboard** with 3–4 sections (components) under `App`:

Possible sections:
- Counter widget
- Local notes widget
- Simple user info/profile widget
- Theme toggle or greeting widget

In `notes-day5.txt`, outline:
- Components as boxes:
  - `App`
    - `Header`
    - `Dashboard`
      - `CounterWidget`
      - `NotesWidget`
      - `ProfileWidget`
      - (optional) `ThemeToggle`
- What props each child might receive from `App` (e.g., user name).

### 2. Reorganize files (60–70 min)

Create folders:

```text
src/
  components/
    Header.jsx
    CounterWidget.jsx
    ToggleMessage.jsx
    NotesWidget.jsx
    ProfileCard.jsx
  App.jsx
  main.jsx
  index.css
```

Rename/move:
- Move existing `Counter` → `CounterWidget.jsx`.
- Move `ToggleMessage` → `ToggleMessage.jsx` in `components` folder.
- Move `NotesList` → `NotesWidget.jsx`.

Example `Header.jsx`:

```jsx
function Header({ title }) {
  return (
    <header className="app-header">
      <h1>{title}</h1>
    </header>
  );
}

export default Header;
```

Update `App.jsx`:

```jsx
import Header from "./components/Header";
import CounterWidget from "./components/CounterWidget";
import ToggleMessage from "./components/ToggleMessage";
import NotesWidget from "./components/NotesWidget";
import ProfileCard from "./components/ProfileCard";

function App() {
  const user = {
    name: "Your Name",
    role: "Aspiring Full Stack Developer",
    bio: "Learning React, Node, and Mongo to build cool apps.",
  };

  return (
    <div className="app">
      <Header title="React Mini Dashboard" />
      <main className="dashboard">
        <section>
          <CounterWidget />
        </section>
        <section>
          <ToggleMessage />
        </section>
        <section>
          <NotesWidget />
        </section>
        <section>
          <ProfileCard
            name={user.name}
            role={user.role}
            bio={user.bio}
          />
        </section>
      </main>
    </div>
  );
}

export default App;
```

Style lightly in `index.css`:
- `.app`, `.app-header`, `.dashboard`, `section` (use Flexbox/Grid for layout).

### 3. Reflection (5–10 min)

In `notes-day5.txt`:
- How does splitting components into a `components/` folder help?
- What data did you choose to put in `App` versus child components?

---

## Day 6 – Derived State, Simple “Lifting State Up”

**Objectives:**
- Derive simple values from state (e.g., counts).
- Practice lifting state up to a common parent.

### 1. Concept (25–30 min)

Learn:
- **Derived state**: values computed from existing state instead of storing separately.
  - e.g., `completedCount = todos.filter(t => t.completed).length`.
- **Lifting state up**:
  - When two siblings need to share data, move state to their parent and pass it via props.

### 2. Practice: notes stats + simple name input (60–70 min)

a) **Notes stats** (derived state)  
In `NotesWidget.jsx`:
- After `notes` is defined, compute:

  ```jsx
  const noteCount = notes.length;
  ```

- Display:

  ```jsx
  <p>Total notes: {noteCount}</p>
  ```

If you want: show characters count, etc.

b) **Lifting state up – user name**

Goal: `App` holds the user’s name; a child component edits it; another child displays it.

1. In `App.jsx`:

   ```jsx
   import { useState } from "react";
   import Header from "./components/Header";
   import NameEditor from "./components/NameEditor";
   import ProfileCard from "./components/ProfileCard";
   // ...other imports

   function App() {
     const [userName, setUserName] = useState("Your Name");

     const user = {
       name: userName,
       role: "Aspiring Full Stack Developer",
       bio: "Learning full stack development.",
     };

     return (
       <div className="app">
         <Header title="React Mini Dashboard" />
         <main className="dashboard">
           <section>
             <NameEditor name={userName} onNameChange={setUserName} />
           </section>
           <section>
             <ProfileCard
               name={user.name}
               role={user.role}
               bio={user.bio}
             />
           </section>
           {/* other sections (Counter, Notes, etc.) */}
         </main>
       </div>
     );
   }

   export default App;
   ```

2. Create `components/NameEditor.jsx`:

   ```jsx
   function NameEditor({ name, onNameChange }) {
     function handleChange(e) {
       onNameChange(e.target.value);
     }

     return (
       <div className="card">
         <h2>Edit User Name</h2>
         <input value={name} onChange={handleChange} />
         <p>Preview: {name}</p>
       </div>
     );
   }

   export default NameEditor;
   ```

Now, editing the input in `NameEditor` will update the name in `App` and thus the `ProfileCard`.

### 3. Reflection (5–10 min)

In `notes-day6.txt`:
- Why did the state for `userName` live in `App` and not in `NameEditor`?
- What is derived state, and why is it often better than storing computed values separately?

---

## Day 7 – Polish, Review, and Small Challenge

**Objectives:**
- Clean up the mini dashboard.
- Review main React concepts.
- Do a small challenge without directly copying earlier code.

### 1. UI polish (30–40 min)

In `index.css` (or create `App.css` and import in `App.jsx`):
- Make the header visually distinct (background color, padding).
- Use a simple responsive layout for `.dashboard` (cards in grid on desktop, stacked on mobile).
- Style `.card` class for all components:

  ```css
  .card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 1rem;
    margin: 0.5rem;
    background-color: #fff;
  }
  ```

- Ensure spacing is consistent and fonts are readable.

### 2. Small challenge: new widget from scratch (30–40 min)

Create a **new component** *without looking at older code initially* (try from memory, then fix):

Example: `MoodTracker.jsx`:
- State: `mood` (string), default `"🙂"`.
- UI:
  - Heading “Mood Tracker”
  - Buttons: “Happy”, “Neutral”, “Sad”
  - When clicked, update `mood` to `"😄"`, `"😐"`, `"😢"` (or just text faces if you don’t want emojis).
  - Display a message depending on mood.

Implementation idea:

```jsx
import { useState } from "react";

function MoodTracker() {
  const [mood, setMood] = useState("neutral");

  function handleSetMood(newMood) {
    setMood(newMood);
  }

  let message;
  if (mood === "happy") message = "You're feeling great!";
  else if (mood === "sad") message = "Hope things get better soon.";
  else message = "You're feeling okay.";

  return (
    <div className="card">
      <h2>Mood Tracker</h2>
      <button onClick={() => handleSetMood("happy")}>Happy</button>
      <button onClick={() => handleSetMood("neutral")}>Neutral</button>
      <button onClick={() => handleSetMood("sad")}>Sad</button>
      <p>Current mood: {mood}</p>
      <p>{message}</p>
    </div>
  );
}

export default MoodTracker;
```

Add it to `App.jsx` inside a `<section>`.

### 3. Review & self-assessment (20–25 min)

In `notes-week8-summary.txt`, write:

- Concepts you now feel comfortable with:
  - Components & props?
  - `useState` & event handling?
  - Controlled inputs & lists?
  - Basic component structure and folders?
- Concepts still fuzzy:
  - When to put state in which component?
  - How to avoid prop-drilling? (This will come later with context or state libraries.)
- One goal for Week 9:
  - e.g., “Learn `useEffect` and fetch data from my Notes API,” or
  - “Hook this React app to the backend I built in Weeks 6–7.”

---

If you want next, I can generate a **Week 9 day-by-day plan** focused on:
- `useEffect`, data fetching from your Notes API,
- basic client-side routing with `react-router`,
- and moving toward your first true full-stack integration.
