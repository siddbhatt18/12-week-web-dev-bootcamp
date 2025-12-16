**Week 4 Theme:** DOM manipulation, events, `localStorage`, and building a small app (TODO list).  
Assume ~2 hours/day. Work in a `week4/` folder.

You’ll end the week with a working **Vanilla JS TODO App (P2 prototype)**.

---

## Day 1 – DOM Selection & Creating/Removing Elements

**Objectives:**
- Get comfortable selecting elements.
- Dynamically create and remove elements with JS.

### 1. Concept (25–30 min)
Review/learn:
- Selecting elements:
  ```js
  document.querySelector("h1");
  document.querySelector("#idName");
  document.querySelectorAll(".className");
  ```
- Creating elements:
  ```js
  const li = document.createElement("li");
  li.textContent = "New item";
  parent.appendChild(li);
  ```
- Removing elements:
  ```js
  element.remove();
  // or parent.removeChild(child) (older way)
  ```

### 2. Practice: dynamic list (60–70 min)
Create `day1-dom-create.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Week 4 - Day 1</title>
  </head>
  <body>
    <h1>Favorite Foods</h1>
    <ul id="food-list">
      <li>Pizza</li>
      <li>Burgers</li>
    </ul>

    <button id="add-food-btn">Add Food</button>
    <button id="clear-foods-btn">Clear All</button>

    <script src="day1.js"></script>
  </body>
</html>
```

In `day1.js`:
- Select the list and buttons:
  ```js
  const foodList = document.querySelector("#food-list");
  const addBtn = document.querySelector("#add-food-btn");
  const clearBtn = document.querySelector("#clear-foods-btn");
  ```
- On `addBtn` click:
  - Create a new `<li>` with text `"New food X"` (increment X with a counter).
  - Append it to the list.
- On `clearBtn` click:
  - Remove all `<li>` children from the list (e.g., `foodList.innerHTML = "";` or loop and remove).

### 3. Reflection (5–10 min)
In `notes-day1.txt`:
- What are two ways to remove elements from the DOM?

---

## Day 2 – Forms, Inputs & Basic Validation

**Objectives:**
- Read user input from a form.
- Prevent default form submission and handle it with JS.
- Do simple “validation” checks.

### 1. Concept (25–30 min)
Learn:
- Handling forms:
  ```js
  form.addEventListener("submit", (event) => {
    event.preventDefault(); // stop page reload
    const value = input.value;
  });
  ```
- Input elements: `value` property.
- Basic validation:
  - Check if string is empty or too short.
  - Provide feedback to the user (message on page).

### 2. Practice: simple task form (60–70 min)
Create `day2-form.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Week 4 - Day 2</title>
  </head>
  <body>
    <h1>Add a Task</h1>
    <form id="task-form">
      <input id="task-input" type="text" placeholder="Enter a task" />
      <button type="submit">Add</button>
    </form>

    <p id="error" style="color: red;"></p>

    <ul id="task-list"></ul>

    <script src="day2.js"></script>
  </body>
</html>
```

In `day2.js`:
- Select form, input, error paragraph, and task list.
- On `submit`:
  - `event.preventDefault()`.
  - Read `taskInput.value`.
  - If empty or too short, set error text: `"Please enter a task with at least 3 characters."`
  - Else:
    - Clear error.
    - Create an `<li>` with the task text.
    - Append to `task-list`.
    - Clear input (`taskInput.value = ""`).

### 3. Reflection (5–10 min)
In `notes-day2.txt`:
- Why do we use `event.preventDefault()` on forms in JS apps?

---

## Day 3 – Event Delegation & Basic App Structure

**Objectives:**
- Learn how to handle events for many dynamic items using event delegation.
- Start structuring your code into logical parts.

### 1. Concept (30–35 min)
Learn:
- **Event delegation**:
  - Instead of adding a click listener to every `<li>`, listen on the parent `<ul>` and check `event.target`.
- Benefits:
  - Works for new elements added later.
  - Less code and better performance for many items.

Pattern:

```js
list.addEventListener("click", (event) => {
  if (event.target.matches(".delete-btn")) {
    // handle delete
  }
});
```

### 2. Practice: deletable tasks (60–70 min)
Copy `day2-form.html` → `day3-tasks.html` and `day2.js` → `day3.js`.  
Modify `day3-tasks.html` to include a delete button for each item:

When creating an `<li>`:

```js
const li = document.createElement("li");
li.innerHTML = `
  <span>${taskText}</span>
  <button class="delete-btn">Delete</button>
`;
```

In `day3.js`:
- Add a `click` listener to `task-list` (`<ul>`).
- In the handler:
  - Check `if (event.target.matches(".delete-btn")) { ... }`
  - If yes:
    - Find the parent `<li>` (e.g., `event.target.closest("li")`) and `remove()` it.

Also:
- Extract logic into smaller functions where possible, e.g.:
  - `addTask(taskText)`
  - `createTaskElement(taskText)`

### 3. Reflection (5–10 min)
In `notes-day3.txt`:
- Explain event delegation in your own words and why it’s helpful in dynamic lists.

---

## Day 4 – Local Storage Basics (Saving & Loading Data)

**Objectives:**
- Learn how to persist data in the browser using `localStorage`.
- Save a small array of tasks and reload it.

### 1. Concept (30–35 min)
Learn:
- `localStorage`:
  - Key-value store (only strings).
  - `localStorage.setItem("key", "value")`
  - `localStorage.getItem("key")`
  - `localStorage.removeItem("key")`
- Using JSON:
  - Convert JS → String: `JSON.stringify(data)`
  - Convert String → JS: `JSON.parse(data)`

Pattern:

```js
const tasks = [{ text: "Learn JS", completed: false }];

localStorage.setItem("tasks", JSON.stringify(tasks));

const stored = localStorage.getItem("tasks");
const parsed = stored ? JSON.parse(stored) : [];
```

### 2. Practice: save and load tasks (60–70 min)
Copy `day3-tasks.html` → `day4-storage.html`, `day3.js` → `day4.js`.

In `day4.js`:
- Maintain a `let tasks = []` array in JS.
- When adding a task:
  - Push a new object `{ id: Date.now(), text: taskText }` to `tasks`.
  - Call a function `saveTasks()` that does:
    ```js
    localStorage.setItem("tasks", JSON.stringify(tasks));
    ```
- When deleting a task:
  - Use the task’s `id` to remove it from the `tasks` array.
  - Then call `saveTasks()` again.

- On page load:
  - Read from `localStorage`:
    ```js
    const storedTasks = localStorage.getItem("tasks");
    tasks = storedTasks ? JSON.parse(storedTasks) : [];
    ```
  - Loop through `tasks` and render each one to the page.

### 3. Reflection (5–10 min)
In `notes-day4.txt`:
- What happens to your data when you close the tab or browser and reopen it?
- Why do we use `JSON.stringify` and `JSON.parse`?

---

## Day 5 – P2 TODO App (v1): Basic Version

**Objectives:**
- Start the “real” TODO app project (P2).
- Build a clean, minimal UI and hook up add/delete + persistence.

### 1. Plan & Setup (20–30 min)
Create a folder `week4/todo-app/`.

Create:
- `index.html`
- `styles.css`
- `app.js`

Plan features for **v1**:
- Add tasks (text only).
- List tasks.
- Delete tasks.
- Persist tasks in `localStorage`.

### 2. Build HTML & CSS skeleton (40–50 min)
In `index.html`, structure:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>TODO App</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <main class="app">
      <h1>My TODO List</h1>
      <form id="todo-form">
        <input id="todo-input" type="text" placeholder="What do you need to do?" />
        <button type="submit">Add</button>
      </form>

      <ul id="todo-list"></ul>
    </main>

    <script src="app.js"></script>
  </body>
</html>
```

In `styles.css`:
- Basic centered layout, simple fonts, some padding.
- Style the `form` and list items for readability (no need to polish yet).

### 3. JS: add + render tasks (40–50 min)
In `app.js`:
- Use code patterns from Days 2–4:
  - `let todos = [];`
  - On load, `loadTodos()` from `localStorage`.
  - `renderTodos()` to update the `<ul>`.
  - `addTodo(text)` to push into `todos` and re-render + save.
  - `deleteTodo(id)` to filter out and re-render + save.

Focus on:
- Getting a minimal working version:
  - Add tasks.
  - They show on page.
  - They persist after reload.
  - Delete works.

### 4. Reflection (5–10 min)
In `todo-app/notes-v1.txt`:
- Which part felt hardest: form handling, DOM updates, or `localStorage`?

---

## Day 6 – P2 TODO App (v2): Mark Complete & Basic UI Improvements

**Objectives:**
- Add “mark as completed” feature.
- Improve the UI slightly.

### 1. Concept (20–30 min)
Think through:
- Task structure now:
  ```js
  { id, text, completed: false }
  ```
- How to represent completed state visually:
  - e.g., line-through text, lighter color.
- How to toggle `completed` when a checkbox or button is clicked.

### 2. Implementation (60–70 min)
In `app.js`:
- Update task model to include `completed: false` when creating.
- When rendering a task:
  - Include a checkbox or button, e.g.:

    ```js
    li.innerHTML = `
      <label>
        <input type="checkbox" class="toggle-completed" ${todo.completed ? "checked" : ""}>
        <span class="${todo.completed ? "completed" : ""}">${todo.text}</span>
      </label>
      <button class="delete-btn">Delete</button>
    `;
    ```

- Add **event delegation** on `#todo-list`:
  - If `event.target.matches(".delete-btn")` → delete.
  - If `event.target.matches(".toggle-completed")` → find the related todo by id, flip `completed`, save + re-render.

In `styles.css`:
- Add `.completed` class:
  ```css
  .completed {
    text-decoration: line-through;
    color: #888;
  }
  ```

### 3. Small UI polish (20–30 min)
- Add some spacing/margins between tasks.
- Style buttons (background color, border radius).
- Make input full-width on small screens using a media query.

### 4. Reflection (5–10 min)
In `todo-app/notes-v2.txt`:
- What new issue did you face when adding the `completed` state?
- How did you solve it (or what’s your plan to improve)?

---

## Day 7 – P2 TODO App (v3): Filtering, Cleanup & Git

**Objectives:**
- Add a small extra feature (filter or counter).
- Clean up the code.
- Put the project under Git and commit.

### 1. Choose one extra feature (15–20 min)
Pick **one** of these to add:

**Option A – Counter:**
- Show how many tasks total and how many are completed.

**Option B – Filter:**
- Buttons: “All”, “Active”, “Completed”.
- Filter which tasks are shown in the list (without deleting them).

### 2. Implement the feature (60–70 min)

**For Option A (Counter):**
- In `index.html`, add:
  ```html
  <p id="stats"></p>
  ```
- In `renderTodos()`:
  - After rendering list, compute counts:
    ```js
    const total = todos.length;
    const completed = todos.filter(t => t.completed).length;
    statsElement.textContent = `Total: ${total} | Completed: ${completed}`;
    ```

**For Option B (Filter):**
- In `index.html`, add:
  ```html
  <div id="filters">
    <button data-filter="all">All</button>
    <button data-filter="active">Active</button>
    <button data-filter="completed">Completed</button>
  </div>
  ```
- In `app.js`:
  - Track a `let currentFilter = "all";`
  - When rendering, compute `filteredTodos` based on `currentFilter`.
  - Add event listener to `#filters` and update `currentFilter` on button click, then re-render.

### 3. Code cleanup (20–25 min)
- Make sure you:
  - Have small, focused functions: `addTodo`, `deleteTodo`, `toggleCompleted`, `saveTodos`, `loadTodos`, `renderTodos`.
  - Use clear names for variables and functions.
  - Remove `console.log` calls that you no longer need (or keep only important ones).

### 4. Git init & commit (15–20 min)
Inside `week4/todo-app/`:
- Initialize Git if not already:
  ```bash
  git init
  git status
  git add .
  git commit -m "Initial TODO app with add/delete and persistence"
  ```
- Make a small change, then:
  ```bash
  git add .
  git commit -m "Add completed state and basic stats/filter"
  ```

If you want, you can create a GitHub repo and push (same as Week 2 process).

### 5. Weekly reflection (10–15 min)
In `week4/notes-week4-summary.txt`:
- What can you now do in JavaScript that you couldn’t do a week ago?
- Which parts are still confusing (e.g., event delegation, `this`, organizing code)?
- Are you comfortable with:
  - Selecting and manipulating DOM elements?
  - Handling form submissions?
  - Using `localStorage` for simple data?
- One specific goal for Week 5 (e.g., “Get comfortable with fetch and APIs,” or “Practice more with small JS utilities”).

---

If you’d like, next I can create a **Week 5 day-by-day plan** focused on asynchronous JavaScript, fetching data from public APIs, and building your **API-powered dashboard (P3)**.
