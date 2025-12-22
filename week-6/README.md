Here’s your **Week 6 (Days 1–7) plan**, focused on:

- `useEffect` and side effects in React  
- Fetching data inside React components  
- Handling loading/error states  
- Slightly richer state patterns in a small **“Users Dashboard”** React app

Assume ~2–3 hours/day.  
Each day: **Learn → Do → Reflect → Stretch**.  
You’ll reuse your Week 5 React project (Vite) and add new pages/components.

---

## Day 1 – Mental Model of `useEffect` (Side Effects)

**Goals:**
- Understand what a **side effect** is in React.
- Learn when and why to use `useEffect`.
- Implement a simple effect that runs on mount.

### 1. Learn (40–60 minutes)

**Concepts:**
- Component render vs side effect:
  - Render = pure calculation of UI from state/props.
  - Side effect = something that touches the “outside world”:
    - Fetching data
    - Reading/writing `localStorage`
    - Subscribing to events, etc.
- `useEffect` basic form:

  ```jsx
  useEffect(() => {
    // side effect code here
  }, []); // dependency array
  ```

- Dependency array:
  - `[]` → run once on mount.
  - `[someValue]` → run whenever `someValue` changes.

**Read:**
- React docs: “Using the Effect Hook” (react.dev/learn).
- Focus on:
  - Effects as “escape hatches”.
  - The dependency array concept (don’t worry yet about advanced details).

Write in your notes:
- Your own one-sentence definition of a “side effect”.
- What `useEffect(() => {...}, [])` means in plain language.

### 2. Do (60–90 minutes)

In your `week5-react` project, create a small example component.

1. **Create `EffectDemo.jsx`:**

   ```jsx
   import { useState, useEffect } from "react";

   function EffectDemo() {
     const [count, setCount] = useState(0);

     useEffect(() => {
       console.log("Effect ran. Current count:", count);
       document.title = `Count is ${count}`;
     }, [count]);

     return (
       <div>
         <p>Count: {count}</p>
         <button onClick={() => setCount(count + 1)}>Increment</button>
       </div>
     );
   }

   export default EffectDemo;
   ```

   - Render `<EffectDemo />` in `App.jsx`.

2. **Experiment:**
   - Watch the document title change as you click.
   - Add a `console.log("Render")` above `useEffect` to see the order of render vs effect.

3. **Try a “mount-only” effect:**
   - Add another `useEffect`:

     ```jsx
     useEffect(() => {
       console.log("Component mounted");
     }, []);
     ```

   - Notice it logs once on first render.

### 3. Reflect (10–15 minutes)

- In your notes:
  - When does the effect with `[count]` run?
  - When does the effect with `[]` run?
- Why shouldn’t you update state in a way that causes infinite loops in an effect (e.g. always calling `setCount` inside an effect with no conditions)?

### 4. Stretch (optional, 20–30 minutes)

- Add another state variable, e.g. `name`, and log when name changes using a separate effect with `[name]`.
- Try intentionally creating an infinite loop (set state *unconditionally* in an effect), see what happens, then fix it. This helps you internalize the pattern.

---

## Day 2 – Fetching Data with `useEffect` (GET Requests)

**Goals:**
- Use `useEffect` to fetch data from an API when a component mounts.
- Manage loading and error state in React.

### 1. Learn (40–60 minutes)

**Concepts:**
- Data fetching in React:
  - `useEffect` with empty dependency array: fetch once on mount.
- Basic state for remote data:
  - `loading`, `error`, and `data`.
- `async` functions inside `useEffect`:
  - You can define an async function *inside* the effect and call it.

**Read:**
- React docs: “You Might Not Need an Effect” (skim) and “Fetching Data” (react.dev/learn).
- Revisit MDN `fetch` if needed (you used it in Week 4).

Write down:
- Pseudocode for a component that:
  - Has `[users, setUsers]`, `[loading, setLoading]`, `[error, setError]`.
  - Fetches data on mount and sets those accordingly.

### 2. Do (60–90 minutes)

In `week5-react`, create a new component `UsersPage.jsx`.

1. **Setup:**

   ```jsx
   import { useState, useEffect } from "react";

   function UsersPage() {
     const [users, setUsers] = useState([]);
     const [loading, setLoading] = useState(false);
     const [error, setError] = useState(null);

     useEffect(() => {
       async function fetchUsers() {
         try {
           setLoading(true);
           setError(null);
           const response = await fetch(
             "https://jsonplaceholder.typicode.com/users"
           );
           if (!response.ok) {
             throw new Error(`HTTP error: ${response.status}`);
           }
           const data = await response.json();
           setUsers(data);
         } catch (err) {
           console.error(err);
           setError(err.message);
         } finally {
           setLoading(false);
         }
       }

       fetchUsers();
     }, []);

     if (loading) {
       return <p>Loading users...</p>;
     }

     if (error) {
       return <p>Error: {error}</p>;
     }

     return (
       <div>
         <h1>Users</h1>
         <ul>
           {users.map((user) => (
             <li key={user.id}>
               {user.name} ({user.email})
             </li>
           ))}
         </ul>
       </div>
     );
   }

   export default UsersPage;
   ```

   - Render `<UsersPage />` in `App.jsx` temporarily.

2. **Experiment:**
   - Break the URL to see the error state.
   - Add console logs to see when the effect runs.

### 3. Reflect (10–15 minutes)

- What’s the role of `loading` and `error` states?
- Why is `setLoading(false)` done in `finally`?

### 4. Stretch (optional, 20–30 minutes)

- Add a “Reload” button that triggers the same fetch logic (can move it into a reusable `loadUsers` function).
- Show a count: “Loaded X users”.

---

## Day 3 – Adding Search & Derived State in React

**Goals:**
- Apply **client-side filtering** in React using `filter()` and `useState`.
- Understand derived state (data calculated from other state instead of stored separately).

### 1. Learn (30–45 minutes)

**Concepts:**
- Source of truth:
  - Keep the original data (`users`) in state.
  - Derive filtered results from `users` + `searchTerm`.
- `searchTerm` state:
  - Controlled input: `value` + `onChange`.

Review:
- Array `.filter()` usage from Week 4.
- How you built search in the vanilla JS dashboard.

Write down:
- A simple plan:
  - `const [searchTerm, setSearchTerm] = useState("");`
  - `const filteredUsers = users.filter(...)`.

### 2. Do (60–90 minutes)

Extend `UsersPage.jsx`:

1. **Add search state & input:**

   ```jsx
   const [searchTerm, setSearchTerm] = useState("");

   // inside return (when not loading/error)
   return (
     <div>
       <h1>Users</h1>

       <input
         type="text"
         placeholder="Search by name or email..."
         value={searchTerm}
         onChange={(e) => setSearchTerm(e.target.value)}
       />

       <ul>
         {filteredUsers.map(/* ... */)}
       </ul>
     </div>
   );
   ```

2. **Compute `filteredUsers`:**

   ```jsx
   const filteredUsers = users.filter((user) => {
     const term = searchTerm.toLowerCase();
     return (
       user.name.toLowerCase().includes(term) ||
       user.email.toLowerCase().includes(term)
     );
   });
   ```

3. **Handle “no results” case:**
   - If `filteredUsers.length === 0`, show a message: “No users match your search”.

### 3. Reflect (10–15 minutes)

- Why don’t you create a separate `filteredUsers` state with `useState`?
- How does this pattern avoid bugs compared to storing multiple copies of data in state?

### 4. Stretch (optional, 20–30 minutes)

- Add a dropdown (`<select>`) to filter by company:
  - Build a list of unique companies from `users`.
  - Use another state `selectedCompany` and filter by it in addition to `searchTerm`.

---

## Day 4 – Local Storage in React with `useEffect`

**Goals:**
- Persist React state to `localStorage`.
- Load initial state from `localStorage` when the component mounts.

### 1. Learn (40–60 minutes)

**Concepts:**
- Local storage:
  - `localStorage.setItem(key, JSON.stringify(value))`
  - `JSON.parse(localStorage.getItem(key) || "[]")`
- Pattern in React:
  - Initialize state from `localStorage` **once**.
  - Use an effect to save whenever state changes.

**Read:**
- MDN: “Window.localStorage” (refresh).
- Search “React useEffect localStorage pattern” and skim one article (don’t copy directly, understand the idea).

Write down:
- Pseudocode to:
  - On mount: load todos from `localStorage` if present.
  - On state change: save todos to `localStorage`.

### 2. Do (60–90 minutes)

Use your **React To‑Do app** from Week 5 (`TodoApp.jsx`).

1. **Initialize state from localStorage:**

   In `TodoApp.jsx`, change:

   ```jsx
   const [todos, setTodos] = useState(initialTodos);
   ```

   to something like:

   ```jsx
   function getInitialTodos() {
     const stored = localStorage.getItem("todos");
     if (!stored) return initialTodos;
     try {
       return JSON.parse(stored);
     } catch {
       return initialTodos;
     }
   }

   const [todos, setTodos] = useState(getInitialTodos);
   ```

   Note: Passing a function to `useState` ensures it runs only once (lazy initialization).

2. **Save todos on change using `useEffect`:**

   ```jsx
   useEffect(() => {
     localStorage.setItem("todos", JSON.stringify(todos));
   }, [todos]);
   ```

3. **Test:**
   - Add/remove todos.
   - Refresh page: tasks should persist.

### 3. Reflect (10–15 minutes)

- Why is it useful to have a function (`getInitialTodos`) passed to `useState`?
- How is this pattern different from the vanilla JS approach?

### 4. Stretch (optional, 20–30 minutes)

- Add a second piece of persisted state (e.g., a `filter` or `theme`) with its own `useEffect`.
- Consider: Are you overusing effects? Could some logic be done without an effect (derived state)?

---

## Day 5 – Small React “Users Dashboard” App (Multi-Component)

**Goals:**
- Combine `useEffect` (fetch), `useState` (filters, loading), and component composition.
- Build a slightly more organized **Users Dashboard** inside React.

### 1. Learn (30–45 minutes)

Concepts to focus on:
- Splitting a page into components:
  - `UsersPage` (state + fetching).
  - `SearchBar` (search input UI).
  - `UsersList` (renders list of users).
  - `UserCard` (single user).
- Passing data + callbacks via props.

Sketch in your notes:
- A component tree for your Users Dashboard.
- What props each child component will need.

### 2. Do (90–120 minutes)

In `week5-react`:

1. **Refactor `UsersPage.jsx` into multiple components:**

   - `SearchBar.jsx`:

     ```jsx
     function SearchBar({ searchTerm, onSearchChange }) {
       return (
         <input
           type="text"
           placeholder="Search by name or email..."
           value={searchTerm}
           onChange={(e) => onSearchChange(e.target.value)}
         />
       );
     }

     export default SearchBar;
     ```

   - `UserCard.jsx`:

     ```jsx
     function UserCard({ user }) {
       return (
         <li className="user-card">
           <h2>{user.name}</h2>
           <p>{user.email}</p>
           <p>{user.company.name}</p>
           <p>{user.address.city}</p>
         </li>
       );
     }

     export default UserCard;
     ```

   - `UsersList.jsx`:

     ```jsx
     import UserCard from "./UserCard";

     function UsersList({ users }) {
       if (users.length === 0) {
         return <p>No users match your search.</p>;
       }

       return (
         <ul>
           {users.map((user) => (
             <UserCard key={user.id} user={user} />
           ))}
         </ul>
       );
     }

     export default UsersList;
     ```

2. **Update `UsersPage.jsx`:**

   ```jsx
   import { useState, useEffect } from "react";
   import SearchBar from "./SearchBar";
   import UsersList from "./UsersList";

   function UsersPage() {
     const [users, setUsers] = useState([]);
     const [loading, setLoading] = useState(false);
     const [error, setError] = useState(null);
     const [searchTerm, setSearchTerm] = useState("");

     useEffect(() => {
       async function fetchUsers() {
         try {
           setLoading(true);
           setError(null);
           const res = await fetch("https://jsonplaceholder.typicode.com/users");
           if (!res.ok) throw new Error(`HTTP error: ${res.status}`);
           const data = await res.json();
           setUsers(data);
         } catch (err) {
           setError(err.message);
         } finally {
           setLoading(false);
         }
       }

       fetchUsers();
     }, []);

     const filteredUsers = users.filter((user) => {
       const term = searchTerm.toLowerCase();
       return (
         user.name.toLowerCase().includes(term) ||
         user.email.toLowerCase().includes(term)
       );
     });

     return (
       <div>
         <h1>Users Dashboard</h1>

         <SearchBar searchTerm={searchTerm} onSearchChange={setSearchTerm} />

         {loading && <p>Loading...</p>}
         {error && <p>Error: {error}</p>}

         {!loading && !error && <UsersList users={filteredUsers} />}
       </div>
     );
   }

   export default UsersPage;
   ```

3. **Use in `App.jsx`:**

   ```jsx
   import UsersPage from "./UsersPage";

   function App() {
     return <UsersPage />;
   }

   export default App;
   ```

### 3. Reflect (10–15 minutes)

- How does splitting the UI into multiple components help?
- Which component owns what state, and why is that reasonable?

### 4. Stretch (optional, 20–30 minutes)

- Add a simple “sort by name” toggle:
  - State `sortAsc`, and a button that flips it.
  - Sort `filteredUsers` before rendering.
- Add some basic styling (cards, layout) via CSS.

---

## Day 6 – Error Handling, Edge Cases & Cleanup

**Goals:**
- Handle edge cases in data fetching apps.
- Learn basics of **cleanup** in `useEffect`.
- Make your Users Dashboard more robust.

### 1. Learn (40–60 minutes)

**Concepts:**
- Edge cases:
  - Slow network → loading state for longer.
  - Request cancelled/unmounted component.
- Cleanup in `useEffect`:
  - Returning a cleanup function to cancel subscriptions, timeouts, etc.
  - For basic fetches you might not strictly need it, but you should know what it does.

Read:
- React docs: “Synchronizing with Effects” (focus on cleanup).
- Skim an article: “AbortController for fetch” (just understand that you *can* cancel in-flight requests).

Write down:
- What a cleanup function in `useEffect` looks like.
- A scenario where you’d need cleanup (e.g. event listeners, intervals).

### 2. Do (60–90 minutes)

1. **Add a simple cleanup-style pattern (not strictly required, but good practice):**
   - In `UsersPage`, guard against state updates after unmount:

     ```jsx
     useEffect(() => {
       let isCancelled = false;

       async function fetchUsers() {
         try {
           setLoading(true);
           setError(null);
           const res = await fetch("https://jsonplaceholder.typicode.com/users");
           if (!res.ok) throw new Error(`HTTP error: ${res.status}`);
           const data = await res.json();
           if (!isCancelled) {
             setUsers(data);
           }
         } catch (err) {
           if (!isCancelled) {
             setError(err.message);
           }
         } finally {
           if (!isCancelled) {
             setLoading(false);
           }
         }
       }

       fetchUsers();

       return () => {
         isCancelled = true;
       };
     }, []);
     ```

   - This is a pattern to avoid calling `setState` on unmounted components.

2. **Improve error UI:**
   - Show a “Retry” button when there’s an error.
   - Extract the fetch logic into a `loadUsers` function and call it from the button and from the effect.

3. **Handle empty data:**
   - Temporarily set `setUsers([])` to see how your app behaves.
   - Ensure it shows a meaningful “No users found” message.

### 3. Reflect (10–15 minutes)

- What are the main “loading phases” of your Users Dashboard?
- Why might calling `setState` on an unmounted component be a problem?

### 4. Stretch (optional, 20–30 minutes)

- Try adding a small delay with `setTimeout` to simulate slow loading and see your loading UI more clearly.
- Read more deeply on `AbortController` and optionally implement cancellation of fetch on unmount.

---

## Day 7 – Consolidation: Mini React “Data App” & Review

**Goals:**
- Build a small React app using `useState` + `useEffect` + fetch + filters from scratch.
- Reflect on your understanding of React side effects and data fetching.

### 1. Plan (20–30 minutes)

Decide on a small “data explorer” app:

Ideas:
- **Posts Explorer** using `https://jsonplaceholder.typicode.com/posts`
- **Countries Explorer** using a REST Countries API
- **Pokemon Browser** using PokeAPI (if you like)

Features:
- Fetch data on mount.
- Display list of items.
- Search/filter input.
- Loading + error states.

Write down:
- Data source (API endpoint).
- Data model (which fields to show from each item).
- Components (e.g. `App`, `SearchBar`, `ItemList`, `ItemCard`).

### 2. Do – Build the Mini App (90–120 minutes)

Create a new folder inside your Vite project or a new Vite project (your choice).

1. **Set up components:**
   - `DataPage` (main page with state and effects).
   - `SearchBar`, `ItemList`, `ItemCard`.

2. **Implement fetching in `DataPage`:**
   - `items`, `loading`, `error`, `searchTerm`.
   - `useEffect` to fetch items on mount.
   - Derived `filteredItems` based on `searchTerm`.

3. **Implement UI:**
   - Show loading / error / no-results messages appropriately.
   - Render items list with `.map`.

4. **Polish:**
   - Add basic CSS.
   - Add item count: “Showing X of Y items”.

### 3. Self-Review (20–30 minutes)

Go through:

- `useEffect`:
  - [ ] I understand when to use it (for side effects, not for simple derivations).
  - [ ] I can fetch data in a `useEffect` and handle loading/error.
  - [ ] I can explain what the dependency array does in simple cases.

- State patterns:
  - [ ] I can manage multiple pieces of state (data, loading, error, searchTerm).
  - [ ] I can derive filtered lists from a base array in state.

- App behavior:
  - [ ] My app handles slow loading gracefully (shows a loading message).
  - [ ] My app recovers from errors (retry button, etc.).
  - [ ] My app behaves sensibly with an empty dataset.

Write 3 bullet points:
- 2 things you now feel solid on (e.g. `useState`, basic `useEffect`, mapping lists in JSX).
- 1 thing that still feels fuzzy or complex (e.g. cleanup, advanced dependency arrays, or prop drilling).

### 4. Reflect (15–20 minutes)

In your notes:
- Describe, step by step, what happens when:
  1. Your data app mounts.
  2. `useEffect` runs and fetches data.
  3. The user types into the search input.

- How does this mental model prepare you for:
  - Connecting to your **own backend API** in future weeks?
  - Implementing authentication and handling user data?

### 5. Stretch (optional, 30–45 minutes)

- Add **pagination or “load more”**:
  - Keep track of a `page` or `visibleCount` state.
  - Show only first N items, with a button to load more.
- Or: Add a simple **detail view**:
  - When clicking an item, show extra info in a detail panel.

---

If you want next, I can:

- Create a **Week 7** plan that transitions you into Node.js + Express (backend),  
- Or help you sketch the architecture for your first full-stack React + Node project (frontend consumes your own API).
