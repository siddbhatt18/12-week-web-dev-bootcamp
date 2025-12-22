Here’s your **Week 5 (Days 1–7) plan**, where you’ll start with **React** and build your first small React apps.  

Assume ~2–3 hours/day.  
Each day: **Learn → Do → Reflect → Stretch**.  
You’ll mainly use **Vite + React** (fast, modern). If you prefer `create-react-app`, you can swap it in.

By the end of Week 5 you should:
- Understand **components, JSX, props, state, and events**.
- Build a **React version of your To‑Do app** or a similar small app.
- Be able to think in **components** and manage simple local state.

---

## Before Day 1: One-Time Setup

If you haven’t yet:
- Install **Node.js** (LTS) from nodejs.org.
- In a terminal:  
  `node -v` and `npm -v` should both work.

---

## Day 1 – What is React? Setup & First Component

**Goals:**
- Understand what React is and why we use it.
- Set up a React app with Vite.
- Create and render your first simple component.

### 1. Learn (40–60 minutes)

**Concepts:**
- What React solves:
  - Manages complex UI state.
  - Component-based: small, reusable pieces.
- Core ideas:
  - Component = function that returns JSX.
  - JSX = HTML-like syntax inside JavaScript.
  - React DOM renders components into a root element.

**Read/Watch:**
- React docs: “Quick Start” (react.dev/learn).
- React docs: “UI as a Tree” (skim to get the idea).
- Optional: Short video “What is React and why use it?” (10–15 min).

In your notes, write:
- One-paragraph answer: “What is React and what problem does it solve?”
- A basic mental model: `Component → JSX → ReactDOM.render`.

### 2. Do (60–90 minutes)

1. **Create a React project with Vite:**

   In your terminal:

   ```bash
   npm create vite@latest week5-react -- --template react
   cd week5-react
   npm install
   npm run dev
   ```

   - Open the URL shown in the terminal (usually `http://127.0.0.1:5173`).

2. **Inspect the starter code:**
   - Open `main.jsx` and `App.jsx` (similar names depending on Vite version).
   - Understand:
     - Where `App` is imported.
     - Where `ReactDOM.createRoot(...).render(<App />)` is called.

3. **Create your own simple component:**
   - In `src`, open `App.jsx` and simplify it:

     ```jsx
     function App() {
       return (
         <div>
           <h1>Hello React</h1>
           <p>This is my first React app.</p>
         </div>
       );
     }

     export default App;
     ```

   - Confirm the browser updates.

4. **Add a second component:**
   - Create `src/Greeting.jsx`:

     ```jsx
     function Greeting() {
       return <p>Nice to meet you, future full-stack developer!</p>;
     }

     export default Greeting;
     ```

   - Use it in `App.jsx`:

     ```jsx
     import Greeting from "./Greeting";

     function App() {
       return (
         <div>
           <h1>Hello React</h1>
           <Greeting />
         </div>
       );
     }

     export default App;
     ```

### 3. Reflect (10–15 minutes)

- How is this different from adding `<script>` tags to an HTML file?
- What do you think JSX is under the hood (hint: it gets turned into JS function calls)?

### 4. Stretch (optional, 20–30 minutes)

- Add another component, e.g. `ProfileCard` with a name, role, and short text, and render it inside `App`.
- Change some JSX intentionally to break it (e.g. omit a closing tag) and read the error.

---

## Day 2 – JSX, Props & Component Composition

**Goals:**
- Get comfortable with JSX syntax rules.
- Pass data into components via **props**.
- Compose multiple components to build a small UI.

### 1. Learn (40–60 minutes)

**Concepts:**
- JSX basics:
  - Single parent element.
  - Using `{}` to embed JS expressions.
  - CamelCased attributes (`className`, `onClick`, etc.).
- Props:
  - Components receive data via props.
  - `function Card(props) { ... }` and `props.title`, `props.children`.

**Read:**
- React docs: “Describing the UI”.
- React docs: “Passing Props to a Component”.

Write down:
- Example JSX snippet and the JS expressions inside `{}`.
- A small component signature using props, e.g. `function UserCard({ name, email })`.

### 2. Do (60–90 minutes)

In `week5-react`:

1. **Create a `UserCard` component (`src/UserCard.jsx`):**

   ```jsx
   function UserCard({ name, role, bio }) {
     return (
       <div className="user-card">
         <h2>{name}</h2>
         <p>{role}</p>
         <p>{bio}</p>
       </div>
     );
   }

   export default UserCard;
   ```

2. **Use it with different props in `App.jsx`:**

   ```jsx
   import UserCard from "./UserCard";

   function App() {
     return (
       <div>
         <h1>Team</h1>
         <UserCard
           name="Alex"
           role="Frontend Developer"
           bio="Loves building interactive UIs."
         />
         <UserCard
           name="Sam"
           role="Backend Developer"
           bio="Enjoys working with databases and APIs."
         />
       </div>
     );
   }

   export default App;
   ```

3. **Add an array and render multiple cards with `.map()`:**
   - In `App.jsx`:

     ```jsx
     const team = [
       { id: 1, name: "Alex", role: "Frontend", bio: "..." },
       { id: 2, name: "Sam", role: "Backend", bio: "..." },
       { id: 3, name: "Taylor", role: "Full Stack", bio: "..." },
     ];

     function App() {
       return (
         <div>
           <h1>Team</h1>
           {team.map((member) => (
             <UserCard
               key={member.id}
               name={member.name}
               role={member.role}
               bio={member.bio}
             />
           ))}
         </div>
       );
     }
     ```

   - Note the `key` prop: helps React track list items.

### 3. Reflect (10–15 minutes)

- How is mapping over an array in React similar to how you used `map` before?
- Why is a `key` needed in lists (even if you don’t fully understand React’s internals yet)?

### 4. Stretch (optional, 20–30 minutes)

- Add a `photoUrl` prop and show an `<img>` in `UserCard`.
- Add inline conditional display:
  - If `bio` is missing, show “No bio available”.

---

## Day 3 – State with useState & Handling Events

**Goals:**
- Use **state** to track dynamic values.
- Handle events like `onClick` and `onChange`.
- Build a simple counter and a basic input-driven component.

### 1. Learn (40–60 minutes)

**Concepts:**
- State:
  - Data that changes over time and triggers re-render.
- `useState` hook:
  - `const [count, setCount] = useState(0);`
- Event handling in React:
  - `onClick`, `onChange`, `onSubmit`.
  - Passing functions as handlers.

**Read:**
- React docs: “Adding Interactivity”.
- React docs: “State: A Component’s Memory”.

Write down:
- A simple example of `useState`.
- What happens when you call the state setter function (e.g. `setCount(count + 1)`).

### 2. Do (60–90 minutes)

1. **Counter component (`src/Counter.jsx`):**

   ```jsx
   import { useState } from "react";

   function Counter() {
     const [count, setCount] = useState(0);

     function handleIncrement() {
       setCount(count + 1);
     }

     function handleDecrement() {
       setCount(count - 1);
     }

     return (
       <div>
         <p>Count: {count}</p>
         <button onClick={handleDecrement}>-</button>
         <button onClick={handleIncrement}>+</button>
       </div>
     );
   }

   export default Counter;
   ```

   - Render `<Counter />` in `App.jsx`.

2. **Controlled input example (`src/NameForm.jsx`):**

   ```jsx
   import { useState } from "react";

   function NameForm() {
     const [name, setName] = useState("");

     function handleChange(event) {
       setName(event.target.value);
     }

     return (
       <div>
         <input
           type="text"
           placeholder="Enter your name"
           value={name}
           onChange={handleChange}
         />
         <p>Hello, {name || "stranger"}!</p>
       </div>
     );
   }

   export default NameForm;
   ```

   - Render `<NameForm />` in `App.jsx`.

3. **Experiment:**
   - Add two counters side by side to see that they each manage their own state.

### 3. Reflect (10–15 minutes)

- How is React state different from just using variables in plain JS?
- Why must you call `setState` (`setCount`) instead of directly changing `count`?

### 4. Stretch (optional, 20–30 minutes)

- Extend `Counter` to also have a “Reset” button.
- Add a second state variable, e.g. `step`, and allow changing how much the counter increments.

---

## Day 4 – Thinking in Components: Small React App (Static Data)

**Goals:**
- Break a UI into **components**.
- Manage state at the appropriate level (parent vs child).
- Build a small “Task List” or “Notes List” with static data.

### 1. Learn (30–45 minutes)

Revisit:
- Component hierarchy:
  - Parent passes data + callbacks to children via props.
- Lifting state up:
  - State lives in the closest common parent that needs it.

Read:
- React docs: “Sharing State Between Components”.
- Skim “Thinking in React” (even if it’s a bit dense, focus on ideas).

Write down:
- A simple component tree for a “Task List” app:
  - `App` → `TaskList` → `TaskItem`
- Which component should own the tasks array state?

### 2. Do (90–120 minutes)

In `week5-react`, create a simple “Notes” app with static initial data (no backend yet).

1. **Plan structure:**
   - Components:
     - `App` – top-level.
     - `NotesApp` – manages notes state.
     - `NoteList` – displays list of notes.
     - `NoteItem` – single note.
     - `AddNoteForm` – input + button to add note.

2. **Implement notes state in `NotesApp.jsx`:**

   ```jsx
   import { useState } from "react";
   import NoteList from "./NoteList";
   import AddNoteForm from "./AddNoteForm";

   const initialNotes = [
     { id: 1, text: "Learn React basics" },
     { id: 2, text: "Build a small app" },
   ];

   function NotesApp() {
     const [notes, setNotes] = useState(initialNotes);

     function handleAddNote(text) {
       const newNote = {
         id: Date.now(),
         text,
       };
       setNotes([...notes, newNote]);
     }

     return (
       <div>
         <h1>Notes</h1>
         <AddNoteForm onAddNote={handleAddNote} />
         <NoteList notes={notes} />
       </div>
     );
   }

   export default NotesApp;
   ```

3. **Create `AddNoteForm.jsx`:**

   ```jsx
   import { useState } from "react";

   function AddNoteForm({ onAddNote }) {
     const [text, setText] = useState("");

     function handleSubmit(event) {
       event.preventDefault();
       const trimmed = text.trim();
       if (!trimmed) return;
       onAddNote(trimmed);
       setText("");
     }

     return (
       <form onSubmit={handleSubmit}>
         <input
           type="text"
           placeholder="New note..."
           value={text}
           onChange={(e) => setText(e.target.value)}
         />
         <button type="submit">Add</button>
       </form>
     );
   }

   export default AddNoteForm;
   ```

4. **Create `NoteList.jsx` and `NoteItem.jsx`:**

   ```jsx
   import NoteItem from "./NoteItem";

   function NoteList({ notes }) {
     if (notes.length === 0) {
       return <p>No notes yet.</p>;
     }

     return (
       <ul>
         {notes.map((note) => (
           <NoteItem key={note.id} note={note} />
         ))}
       </ul>
     );
   }

   export default NoteList;
   ```

   ```jsx
   function NoteItem({ note }) {
     return <li>{note.text}</li>;
   }

   export default NoteItem;
   ```

5. **Use `NotesApp` in `App.jsx`:**

   ```jsx
   import NotesApp from "./NotesApp";

   function App() {
     return (
       <div>
         <NotesApp />
       </div>
     );
   }

   export default App;
   ```

### 3. Reflect (10–15 minutes)

- Which component owns the notes state and why?
- How do child components “talk back” to the parent (hint: callback props)?

### 4. Stretch (optional, 20–30 minutes)

- Add a delete button to each `NoteItem`:
  - Pass `onDeleteNote` callback down from `NotesApp`.
- Add a note counter: “You have X notes”.

---

## Day 5 – Reactifying Your Vanilla To‑Do App (State & Lists)

**Goals:**
- Translate your **vanilla JS To‑Do app** into React.
- Use state for tasks and controlled inputs for new tasks.

### 1. Learn (30–45 minutes)

Think about:
- What you did in vanilla JS:
  - You had `tasks` array, rendered `<li>`s, added event listeners.
- In React:
  - `tasks` lives in state.
  - Rendering is done declaratively with JSX and `.map()`.
  - Event handlers directly update state, React re-renders.

Write down a plan:
- Components you’ll have (similar to Notes):
  - `TodoApp`, `TodoList`, `TodoItem`, `AddTodoForm`.
- What state shape you’ll use for a todo item:
  - `{ id, text, completed }`.

### 2. Do (90–120 minutes)

In `week5-react`, create a React To‑Do app (if you prefer, you can replace the Notes app with To‑Do, or keep both).

1. **`TodoApp.jsx`:**

   ```jsx
   import { useState } from "react";
   import AddTodoForm from "./AddTodoForm";
   import TodoList from "./TodoList";

   const initialTodos = [
     { id: 1, text: "Learn React", completed: false },
     { id: 2, text: "Rewrite To-Do app in React", completed: false },
   ];

   function TodoApp() {
     const [todos, setTodos] = useState(initialTodos);

     function handleAddTodo(text) {
       const newTodo = { id: Date.now(), text, completed: false };
       setTodos([...todos, newTodo]);
     }

     function handleToggleTodo(id) {
       setTodos(
         todos.map((todo) =>
           todo.id === id ? { ...todo, completed: !todo.completed } : todo
         )
       );
     }

     function handleDeleteTodo(id) {
       setTodos(todos.filter((todo) => todo.id !== id));
     }

     return (
       <div>
         <h1>My To-Do List</h1>
         <AddTodoForm onAddTodo={handleAddTodo} />
         <TodoList
           todos={todos}
           onToggleTodo={handleToggleTodo}
           onDeleteTodo={handleDeleteTodo}
         />
       </div>
     );
   }

   export default TodoApp;
   ```

2. **`AddTodoForm.jsx`:** (very similar to `AddNoteForm`)

   ```jsx
   import { useState } from "react";

   function AddTodoForm({ onAddTodo }) {
     const [text, setText] = useState("");

     function handleSubmit(event) {
       event.preventDefault();
       const trimmed = text.trim();
       if (!trimmed) return;
       onAddTodo(trimmed);
       setText("");
     }

     return (
       <form onSubmit={handleSubmit}>
         <input
           type="text"
           placeholder="New task..."
           value={text}
           onChange={(e) => setText(e.target.value)}
         />
         <button type="submit">Add</button>
       </form>
     );
   }

   export default AddTodoForm;
   ```

3. **`TodoList.jsx` and `TodoItem.jsx`:**

   ```jsx
   import TodoItem from "./TodoItem";

   function TodoList({ todos, onToggleTodo, onDeleteTodo }) {
     if (todos.length === 0) {
       return <p>No tasks yet.</p>;
     }

     return (
       <ul>
         {todos.map((todo) => (
           <TodoItem
             key={todo.id}
             todo={todo}
             onToggleTodo={onToggleTodo}
             onDeleteTodo={onDeleteTodo}
           />
         ))}
       </ul>
     );
   }

   export default TodoList;
   ```

   ```jsx
   function TodoItem({ todo, onToggleTodo, onDeleteTodo }) {
     return (
       <li>
         <label>
           <input
             type="checkbox"
             checked={todo.completed}
             onChange={() => onToggleTodo(todo.id)}
           />
           <span
             style={{
               textDecoration: todo.completed ? "line-through" : "none",
               color: todo.completed ? "#888" : "inherit",
             }}
           >
             {todo.text}
           </span>
         </label>
         <button onClick={() => onDeleteTodo(todo.id)}>Delete</button>
       </li>
     );
   }

   export default TodoItem;
   ```

4. **Use in `App.jsx`:**

   ```jsx
   import TodoApp from "./TodoApp";

   function App() {
     return (
       <div>
         <TodoApp />
       </div>
     );
   }

   export default App;
   ```

### 3. Reflect (10–15 minutes)

- Compare your vanilla To‑Do app and the React version:
  - What is simpler now?
  - What feels more complex?
- Where does the main application state live?

### 4. Stretch (optional, 20–30 minutes)

- Add a filter at the top: buttons for “All / Active / Completed”.
  - Keep a `filter` state and derive `filteredTodos` before rendering.
- Add a small summary: “X tasks, Y completed”.

---

## Day 6 – Styling & UX: Making Your React App Feel Polished

**Goals:**
- Add basic styling to your React To‑Do app.
- Improve user experience: empty states, disabled states, focus management.

### 1. Learn (30–45 minutes)

**Concepts:**
- Styling in React:
  - Regular CSS files imported into components or at the root.
  - Class names (`className`).
- Simple UX improvements:
  - Visual feedback on actions.
  - Making forms more intuitive.

Read:
- React docs: “Referencing Values with Refs” (skim; you may not need refs yet, but know they exist).
- Brief CSS article on form/button styling (you already know CSS, focus on how to integrate with React).

### 2. Do (60–90 minutes)

1. **Add a CSS file:**
   - Create `src/App.css` and import it in `App.jsx`:

     ```jsx
     import "./App.css";
     ```

2. **Style main layout:**
   - Wrap main content in a container with max width, center it, and add some spacing.
   - Make tasks list look clean (use similar styling to your vanilla To‑Do app, but now from CSS).

3. **Improve user feedback:**
   - Disable “Add” button when input is empty:
     - `disabled={text.trim().length === 0}`
     - Add CSS for disabled button state.
   - Show a friendly message when there are no todos:
     - Already done via conditional in `TodoList`, but style it.

4. **Minor UX enhancement:**
   - After adding a todo, keep the input focused:
     - Optional: use a `ref` (stretch) or just rely on browser default.
   - Scroll behavior if list gets long (set a max height and `overflow-y: auto`).

### 3. Reflect (10–15 minutes)

- How does it feel to have CSS + JSX together compared to HTML + CSS?
- What small UI change made the biggest difference in perceived quality?

### 4. Stretch (optional, 20–30 minutes)

- Add a light/dark mode toggle:
  - A piece of state `theme` in `App`, a toggle button, and conditional class names on a wrapper `<div className={theme}>`.
- Extract a reusable `Button` component with consistent styling.

---

## Day 7 – Review, Small Refactor & Self-Assessment

**Goals:**
- Review what you’ve learned about React fundamentals.
- Refactor and clean up your To‑Do or Notes app.
- Identify gaps before moving on to more advanced React (effects, API calls in React).

### 1. Review (30–45 minutes)

Skim back through:
- React docs sections you visited:
  - Quick Start
  - Describing the UI
  - Adding Interactivity
  - State & props
- Skim your own code:
  - `TodoApp`, `NotesApp`, `Counter`, etc.

In your notes, answer:
- What is a **component** in your own words?
- What are **props**, and how are they different from **state**?
- How do you **lift state up**?

### 2. Do – Refactor & Clean Up (60–90 minutes)

Pick your main React project from this week (To‑Do or Notes) and:

1. **Clean up component structure:**
   - Ensure each file has **one main component**.
   - Ensure component names are clear.
   - Remove unused imports or variables.

2. **Improve code organization:**
   - Group components into a folder like `src/components/` if it helps.
   - Use consistent naming: `TodoApp`, `TodoList`, `TodoItem`, `AddTodoForm`.

3. **Check for repeated logic:**
   - Are there helpers you can extract into functions?
   - Are props named clearly (`onAddTodo`, `onDeleteTodo` vs `onClick` everywhere)?

4. **Run through the app as a user:**
   - Add tasks, toggle, delete.
   - Confirm no runtime errors in the console.

### 3. Self-Assessment Checklist (20–30 minutes)

For each item, mark ✅ or ❌ and add a note if ❌:

- Fundamentals:
  - [ ] I can explain what JSX is.
  - [ ] I can create a component that takes props and displays them.
  - [ ] I can use `useState` to manage simple state (count, input text).

- Lists & events:
  - [ ] I can render a list with `.map` and `key`.
  - [ ] I can handle events like `onClick` and `onChange`.
  - [ ] I can pass callback props from parent to child and use them.

- App structure:
  - [ ] I can decide which component should own certain state.
  - [ ] I can break a small app into at least 3+ meaningful components.

Write a short paragraph:
- What are you most confident about in React so far?
- What is the **one** concept you want to reinforce in Week 6 (likely `useEffect` and data fetching in React)?

### 4. Stretch (optional, 30–45 minutes)

- Add **localStorage** persistence to your React To‑Do app (similar logic as your vanilla JS version, but adapted to React with `useEffect`—if you haven’t learned `useEffect` yet, you can just sketch or experiment).
- Or: Implement a “simple filter” on your Notes app (search by text using `filter` and extra state).

---

If you’d like next, I can:
- Create a **Week 6 daily plan** focused on `useEffect`, fetching data in React, and slightly more complex state patterns, or  
- Review (conceptually) your current React To‑Do app structure and suggest next improvements (like prop drilling vs context).
