Below is your **Week 3 (Days 1–7) plan**, focused on **core JavaScript** and a small **Vanilla JS To‑Do app** by the end of the week.

Assume ~2–3 hours/day. Adjust as needed.  
Each day: **Learn → Do → Reflect → Stretch**.

Your goals for this week:
- Understand **variables, types, conditionals, loops, functions, arrays, objects**.
- Manipulate the **DOM** with JS.
- Build a **simple interactive app** (To‑Do List) with no frameworks.

---

## Day 1 – JavaScript Basics & Running Code

**Goals:**
- Understand what JavaScript is and where it runs.
- Learn how to run JS in the browser and with a `.js` file.
- Get comfortable with variables and basic types.

### 1. Learn (40–60 minutes)

**Concepts:**
- What JavaScript does: adds logic and interactivity in the browser.
- Where JS code runs:
  - Browser (in `<script>` tags or .js files).
  - Node (later in backend weeks).
- Data types (at a high level):
  - Number, String, Boolean, `null`, `undefined`.
- Variables:
  - `let`, `const` (don’t bother with `var` now).
  - Naming rules and conventions (camelCase).

**Read/Watch (pick 1–2 sources):**
- MDN: “JavaScript first steps” → “What is JavaScript?”, “Hello world”.
- Any short JS intro video (first ~20 minutes) that covers variables & types.

Write in your notes:
- What’s the difference between HTML, CSS, and JS in your own words.
- Example of valid variable names and one invalid (like starting with a number).

### 2. Do (60–90 minutes)

1. **Set up a playground:**
   - Create a folder `week3-js/`.
   - Create `index.html` with:

     ```html
     <!DOCTYPE html>
     <html lang="en">
       <head>
         <meta charset="UTF-8" />
         <title>JS Week 3</title>
       </head>
       <body>
         <h1>JavaScript Practice</h1>
         <script src="script.js"></script>
       </body>
     </html>
     ```

   - Create `script.js` in the same folder.

2. **Write & run simple JS:**
   - In `script.js`:

     ```js
     console.log("Hello from JavaScript!");

     const name = "Your Name";
     let age = 25; // or any number
     const isStudent = true;

     console.log(name, age, isStudent);
     ```

   - Open `index.html` in the browser.
   - Open DevTools → Console. Confirm the logs appear.

3. **Experiment with types:**
   - Add to `script.js`:

     ```js
     const greeting = "Hello";
     const times = 3;
     const result = greeting + " world " + times + " times";
     console.log(result);

     console.log(typeof greeting); // what does this print?
     console.log(typeof times);
     console.log(typeof isStudent);
     ```

   - Observe output in console.

### 3. Reflect (10–15 minutes)

In a `notes-week3.md` file or notebook:
- What is the **console** used for?
- What data types did you see? List them with an example each.

### 4. Stretch (optional, 20–30 minutes)

- Try arithmetic:

  ```js
  const a = 10;
  const b = 3;
  console.log("a + b =", a + b);
  console.log("a * b =", a * b);
  console.log("a / b =", a / b);
  console.log("a % b =", a % b);
  ```

- Predict the outputs before refreshing, then check.

---

## Day 2 – Conditionals & Basic Logic

**Goals:**
- Use `if`, `else if`, `else` blocks.
- Understand comparison operators.

### 1. Learn (40–60 minutes)

**Concepts:**
- Comparison operators:
  - `>`, `<`, `>=`, `<=`, `===`, `!==`
- Conditionals:
  - `if (condition) { ... } else { ... }`
  - `if...else if...else` chains.
- Boolean logic (at a basic level):
  - `&&` (and), `||` (or), `!` (not).

**Read:**
- MDN: “if...else” statement.
- MDN: “Comparison operators”.

Write down:
- Example of a condition that checks if age is ≥ 18.
- Example of combining two conditions with `&&`.

### 2. Do (60–90 minutes)

In `script.js` (you can clear old code or keep it and add new sections):

1. **Age checker:**
   - Write code that:
     - Asks for an age via `prompt` (simplest input).
     - Converts it to a number using `Number()`.
     - Logs if the user is:
       - Under 13: “You are a child”
       - 13–17: “You are a teenager”
       - 18 or older: “You are an adult”

   Example (hint):

   ```js
   const input = prompt("Enter your age:");
   const age = Number(input);

   if (Number.isNaN(age)) {
     console.log("That is not a valid number.");
   } else if (age < 13) {
     console.log("You are a child.");
   } else if (age < 18) {
     console.log("You are a teenager.");
   } else {
     console.log("You are an adult.");
   }
   ```

   Try not to copy; attempt yourself, then check.

2. **Score to grade converter:**
   - Given a score (0–100) in a variable, log a letter grade:
     - ≥ 90: A
     - ≥ 80: B
     - ≥ 70: C
     - ≥ 60: D
     - Else: F

3. **Practice:**
   - Create a variable `isRaining` (true/false).
   - If `isRaining` is true, log “Take an umbrella”; else log “No umbrella needed”.

### 3. Reflect (10–15 minutes)

- When do you use `===` versus `==`? (Look it up if unsure.)
- What’s an example of a real-world situation where conditionals are used in web apps?

### 4. Stretch (optional, 20–30 minutes)

- Adjust grade converter to:
  - Log “Invalid score” if score < 0 or > 100.
- Write a small piece of code that:
  - Asks two yes/no questions via `prompt` (e.g. “Do you like cats?”, “Do you like dogs?”).
  - Logs a message based on combinations of answers (both yes, one yes, both no).

---

## Day 3 – Loops & Arrays

**Goals:**
- Understand arrays and for-loops.
- Use loops to process lists of data.

### 1. Learn (40–60 minutes)

**Concepts:**
- Arrays: ordered list of values:
  - `const numbers = [1, 2, 3];`
  - Access by index: `numbers[0]`.
  - `.length` property.
- Loops:
  - `for` loop: `for (let i = 0; i < array.length; i++) { ... }`
  - `for...of` loop: `for (const item of array) { ... }`

**Read:**
- MDN: “Arrays” (intro + basic methods).
- MDN: “for” statement (examples).
- MDN: “for...of”.

Write down:
- An example of an array of 3 strings.
- The general structure of a `for` loop in pseudocode.

### 2. Do (60–90 minutes)

Use a new file `arrays-loops.js` and link it from `index.html` or just switch scripts for this day.

1. **Create arrays:**

   ```js
   const numbers = [1, 5, 10, 20];
   const fruits = ["apple", "banana", "orange"];
   console.log(numbers.length);
   console.log(fruits[0], fruits[1]);
   ```

2. **Loop over arrays:**
   - Use a classic `for` loop to log each fruit:

     ```js
     for (let i = 0; i < fruits.length; i++) {
       console.log("Fruit at index", i, "is", fruits[i]);
     }
     ```

   - Then rewrite the same using `for...of`.

3. **Sum of numbers:**
   - Use a loop to calculate the sum of `numbers`.
   - Hint:

     ```js
     let sum = 0;
     for (const n of numbers) {
       sum = sum + n; // or sum += n;
     }
     console.log("Total:", sum);
     ```

4. **Practice:**
   - Create an array `tasks = ["learn JS", "build a project", "get a job"];`
   - Loop over `tasks` and log: `Task 1: learn JS`, etc. (use `i + 1` for numbering).

### 3. Reflect (10–15 minutes)

- When would you use a loop in a web app (real-world examples)?
- Which felt more natural: `for` with index, or `for...of`?

### 4. Stretch (optional, 20–30 minutes)

- Create an array of test scores, e.g. `[95, 82, 67, 49, 100]`.
  - Loop and count how many are passing (≥ 60).
- Create an array of names and build a new array that only includes names starting with “A” (just log the filter result for now; we’ll use `.filter` later).

---

## Day 4 – Functions & Basic Problem-Solving

**Goals:**
- Write reusable functions.
- Understand parameters and return values.

### 1. Learn (40–60 minutes)

**Concepts:**
- Function declaration:

  ```js
  function add(a, b) {
    return a + b;
  }
  ```

- Parameters vs arguments.
- Return values.
- Why functions help: reusability, organization.

**Read:**
- MDN: “Functions” (focus on declarations and calling functions).

Write down:
- The generic template for a function declaration.
- Example of a function name that describes **what it does** (e.g. `calculateTotal`).

### 2. Do (60–90 minutes)

Use `functions.js`.

1. **Simple functions:**
   - Write a function `greet(name)` that returns a greeting string (e.g. `"Hello, Alice!"`).
   - Call it with different names and `console.log` the results.

2. **Math functions:**
   - Write `square(number)` that returns the square.
   - Write `isAdult(age)` that returns `true` if age ≥ 18, else `false`.

3. **Working with arrays:**
   - Write a function `sumArray(numbers)` that:
     - Takes an array of numbers.
     - Uses a loop to calculate and return the sum.
   - Test with multiple arrays.

4. **Slightly more complex:**
   - Write `getPassingGrades(grades)` that:
     - Takes an array of numbers (0–100).
     - Returns a **new array** containing only grades ≥ 60.
   - Hint: create an empty array, loop, `push` passing grades.

### 3. Reflect (10–15 minutes)

- How did breaking problems into functions help or not help?
- Which function did you find hardest to write? Why?

### 4. Stretch (optional, 20–30 minutes)

- Refactor an earlier script (like grade calculation) into functions.
- Think of one mini problem and write a function for it, e.g.:
  - `convertCelsiusToFahrenheit(c)`.

---

## Day 5 – Objects & Intro to DOM Manipulation

**Goals:**
- Understand objects as collections of related data.
- Learn how to select and modify HTML elements with JavaScript (DOM).

### 1. Learn (45–60 minutes)

**Concepts:**
- Objects:

  ```js
  const user = {
    name: "Alice",
    age: 25,
    isStudent: false
  };
  ```

  - Access: `user.name`, `user["age"]`.
- Arrays of objects (very common in apps).
- DOM (Document Object Model):
  - The browser turns HTML into a tree.
  - We can select elements via JS and change them.

**Read:**
- MDN: “Working with objects” (intro).
- MDN: “Introduction to the DOM”.
- MDN: “Document.querySelector()”.

Write down:
- Example of a `user` object with at least 3 properties.
- The method you’ll use to select an element by class (e.g. `.querySelector(".className")`).

### 2. Do (60–90 minutes)

1. **Objects & arrays of objects (in `objects.js`):**
   - Create a `user` object with `name`, `age`, `email`.
   - Log a sentence using these properties:  
     `"Alice is 25 years old. You can email her at alice@example.com."`
   - Create an array `users` with 3 user objects.
   - Loop over `users` and log each user’s name.

2. **Basic DOM manipulation:**
   - Create `dom-practice.html`:

     ```html
     <!DOCTYPE html>
     <html lang="en">
       <head>
         <meta charset="UTF-8" />
         <title>DOM Practice</title>
       </head>
       <body>
         <h1 id="title">Original Title</h1>
         <p class="description">This is a description.</p>
         <button id="change-btn">Change Text</button>

         <script src="dom.js"></script>
       </body>
     </html>
     ```

   - Create `dom.js`:

     ```js
     const titleEl = document.querySelector("#title");
     const descEl = document.querySelector(".description");
     const buttonEl = document.querySelector("#change-btn");

     console.log(titleEl.textContent);

     buttonEl.addEventListener("click", function () {
       titleEl.textContent = "Title Changed!";
       descEl.textContent = "The text has been updated by JavaScript.";
     });
     ```

   - Open in browser, click the button, and observe.

3. **Experiment:**
   - Change `style` via JS:

     ```js
     titleEl.style.color = "red";
     ```

   - Add another button that makes the description text bigger or smaller.

### 3. Reflect (10–15 minutes)

- How is an array of objects useful (think about lists of users, tasks, products)?
- What part of DOM manipulation felt most surprising?

### 4. Stretch (optional, 20–30 minutes)

- Add an `<ul>` with 3 `<li>` items to `dom-practice.html`.
- In JS, select the list and:
  - Change the text of one item.
  - Create a new `<li>` with `document.createElement("li")` and `appendChild` it.

---

## Day 6 – Building the To‑Do App (Core Interactions)

**Goals:**
- Start building a **Vanilla JS To‑Do List**.
- Add new tasks and display them on the page.

### 1. Learn (30–45 minutes)

You’ll learn more by building today than reading, but review:

- DOM methods:
  - `querySelector`, `addEventListener`, `value`, `textContent`.
- Arrays + DOM:
  - Store data in an array.
  - Re-render a list from that array.

Skim:
- MDN: “Element.addEventListener()”.
- MDN: “Manipulating documents” (creating elements).

### 2. Do (90–120 minutes)

Create a folder `todo-app/` with:

- `index.html`
- `style.css`
- `app.js`

1. **HTML structure (index.html):**

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>To-Do App</title>
       <link rel="stylesheet" href="style.css" />
     </head>
     <body>
       <main class="container">
         <h1>My To-Do List</h1>
         <form id="todo-form">
           <input
             id="todo-input"
             type="text"
             placeholder="What do you need to do?"
             required
           />
           <button type="submit">Add</button>
         </form>

         <ul id="todo-list"></ul>
       </main>
       <script src="app.js"></script>
     </body>
   </html>
   ```

2. **Basic styling (style.css)** – keep simple so you can focus on JS:

   ```css
   body {
     font-family: system-ui, sans-serif;
     background-color: #f5f5f5;
     margin: 0;
     padding: 0;
   }

   .container {
     max-width: 500px;
     margin: 40px auto;
     background-color: #fff;
     padding: 16px;
     border-radius: 8px;
     box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
   }

   form {
     display: flex;
     gap: 8px;
     margin-bottom: 16px;
   }

   input {
     flex: 1;
     padding: 8px;
   }

   li {
     padding: 8px 0;
     border-bottom: 1px solid #eee;
   }
   ```

3. **Core JS logic (app.js):**
   - Steps:
     1. Select form, input, list (`querySelector` / `getElementById`).
     2. Create an empty `tasks` array.
     3. On form submit:
        - Prevent default behavior (`event.preventDefault()`).
        - Get input value.
        - Push a new task object into `tasks` (e.g. `{ text: 'Buy milk' }`).
        - Clear input.
        - Call a function `renderTasks()` to update the list UI.

   Example structure (don’t just copy; try to write your own then compare):

   ```js
   const form = document.querySelector("#todo-form");
   const input = document.querySelector("#todo-input");
   const list = document.querySelector("#todo-list");

   const tasks = [];

   function renderTasks() {
     list.innerHTML = "";

     for (const task of tasks) {
       const li = document.createElement("li");
       li.textContent = task.text;
       list.appendChild(li);
     }
   }

   form.addEventListener("submit", function (event) {
     event.preventDefault();
     const text = input.value.trim();

     if (text === "") {
       return;
     }

     tasks.push({ text: text });
     input.value = "";
     renderTasks();
   });
   ```

4. **Test:**
   - Add some tasks and ensure they appear.

### 3. Reflect (10–15 minutes)

- Which part was hardest: event handling, arrays, or DOM?
- How did separating `renderTasks()` help structure your code?

### 4. Stretch (optional, 20–30 minutes)

- Show a message if there are no tasks (e.g. “No tasks yet!”):
  - If `tasks.length === 0`, maybe show a special `<li>` or a paragraph.
- Add a timestamp to each task object (e.g. `createdAt: new Date().toLocaleString()`), and display it.

---

## Day 7 – To‑Do App: Complete/Delete & Local Storage

**Goals:**
- Add ability to mark tasks complete and delete them.
- Persist tasks between page reloads using `localStorage`.

### 1. Learn (40–60 minutes)

**Concepts:**
- Event delegation (basic idea): handling events for dynamic lists.
- Data attributes (e.g. `data-id`).
- `localStorage`:
  - `localStorage.setItem(key, value)` (string only).
  - `localStorage.getItem(key)`.
  - Using `JSON.stringify` and `JSON.parse`.

**Read:**
- MDN: “Window.localStorage”.
- Skim an article on “event delegation JavaScript list” (just grasp the idea, you can click directly on buttons in each `<li>` too if easier).

Write down:
- How you would save an array of tasks in localStorage (hint: stringify).
- How you would load tasks at page startup.

### 2. Do (90–120 minutes)

Continue working on `todo-app/`.

1. **Extend task structure:**
   - Use IDs and completion status:

     ```js
     let nextId = 1;
     const tasks = [];
     ```

     When adding a task:

     ```js
     tasks.push({
       id: nextId++,
       text: text,
       completed: false
     });
     ```

2. **Update `renderTasks()` to include buttons & completed style:**

   - In `renderTasks()`:

     ```js
     function renderTasks() {
       list.innerHTML = "";

       for (const task of tasks) {
         const li = document.createElement("li");

         const span = document.createElement("span");
         span.textContent = task.text;
         if (task.completed) {
           span.style.textDecoration = "line-through";
           span.style.color = "#888";
         }

         const completeButton = document.createElement("button");
         completeButton.textContent = task.completed ? "Undo" : "Complete";
         completeButton.dataset.id = task.id;

         const deleteButton = document.createElement("button");
         deleteButton.textContent = "Delete";
         deleteButton.dataset.id = task.id;

         li.appendChild(span);
         li.appendChild(completeButton);
         li.appendChild(deleteButton);

         list.appendChild(li);
       }
     }
     ```

   - Style buttons in `style.css` if needed.

3. **Add event listeners for complete/delete:**
   - Easiest way: add `click` listeners on each button inside the loop:
     - But a more efficient pattern is event delegation: attach one listener to `list` and check `event.target`.
   - For now, you can pick either:
     - Simple approach: add listeners in `renderTasks()` after creating buttons.
     - Or delegation:

       ```js
       list.addEventListener("click", function (event) {
         const target = event.target;
         const id = Number(target.dataset.id);
         if (target.textContent === "Delete") {
           // remove task with this id
         } else if (target.textContent === "Complete" || target.textContent === "Undo") {
           // toggle completed for this id
         }
       });
       ```

   - Implement delete:
     - Find index with `findIndex` or filter tasks array.
   - Implement complete/undo:
     - Find task by id and toggle `task.completed`.

4. **Add localStorage persistence:**
   - After every change to `tasks`, call `saveTasks()`:

     ```js
     function saveTasks() {
       localStorage.setItem("tasks", JSON.stringify(tasks));
       localStorage.setItem("nextId", String(nextId));
     }
     ```

   - On page load, before adding event listeners:

     ```js
     function loadTasks() {
       const tasksJSON = localStorage.getItem("tasks");
       const nextIdStr = localStorage.getItem("nextId");

       if (tasksJSON) {
         const parsed = JSON.parse(tasksJSON);
         tasks.push(...parsed);
       }

       if (nextIdStr) {
         nextId = Number(nextIdStr);
       }
     }

     loadTasks();
     renderTasks();
     ```

   - Ensure:
     - Adding, completing, deleting tasks updates localStorage.
     - Refreshing the page keeps your tasks.

### 3. Reflect (10–20 minutes)

Write down:
- What you now understand about how data flows in a simple app:
  - Input → tasks array → render → user actions → update array → re-render.
- Which parts of the To‑Do app you can explain clearly to someone else.
- Which part still feels fuzzy (e.g. event delegation, localStorage, loops, etc.).

### 4. Stretch (optional, 30–45 minutes)

- Add **filtering**:
  - Buttons: “All”, “Active”, “Completed”.
  - A variable `currentFilter = "all"` that affects what `renderTasks()` shows.
- Add a **task count**:
  - Show “3 tasks remaining” at the top.

---

If you’d like next:
- I can create a **Week 4 daily plan** (modern JS features like `map/filter`, async/await with `fetch`), or  
- Help you **review your To‑Do app structure** and suggest improvements/refactors.
