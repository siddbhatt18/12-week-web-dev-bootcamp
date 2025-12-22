Here’s your **Week 4 (Days 1–7) plan**, focused on **modern JavaScript** and **async code with APIs**, building on your Week 3 To‑Do app skills.

Assume ~2–3 hours/day.  
Each day: **Learn → Do → Reflect → Stretch**.

By the end of Week 4 you should:
- Use modern JS features: **destructuring, spread, map, filter, find**.
- Understand **promises, async/await**, and **fetching data from APIs**.
- Build a small **“Users Dashboard”** app that reads data from a public API.

---

## Day 1 – Modern JS Basics: Let/Const, Template Literals, Arrow Functions

**Goals:**
- Refresh `let`/`const`.
- Use template literals instead of string concatenation.
- Use arrow functions and understand when they’re convenient.

### 1. Learn (40–60 minutes)

**Concepts:**
- `let` vs `const`:
  - `const` for values that won’t be reassigned (arrays/objects can still be *mutated*).
  - `let` when you actually need to reassign.
- Template literals:
  - Backticks \` \`, `${expression}` interpolation.
- Arrow functions:
  - `const add = (a, b) => a + b;`
  - Differences from regular functions (mainly `this`, which you can ignore for now).

**Read:**
- MDN: “let” and “const”.
- MDN: “Template literals”.
- MDN: “Arrow function expressions” (read the intro and basic examples).

Write in your notes:
- One example of a string built with `+`.
- The same string written using template literals.
- One arrow function you understand.

### 2. Do (60–90 minutes)

Create `week4-modern/` with `index.html` and `modern.js`. Link `modern.js` from the HTML.

1. **Template literals practice:**

   ```js
   const name = "Alex";
   const todosCount = 5;
   const message = `${name} has ${todosCount} tasks remaining today.`;
   console.log(message);
   ```

   - Rewrite some of your Week 3 console messages using template literals.

2. **Convert to arrow functions:**
   - From Week 3, pick 2–3 simple functions (e.g. `sumArray`, `isAdult`) and rewrite:

     ```js
     function sumArray(numbers) {
       let sum = 0;
       for (const n of numbers) sum += n;
       return sum;
     }
     ```

     Becomes:

     ```js
     const sumArray = (numbers) => {
       let sum = 0;
       for (const n of numbers) sum += n;
       return sum;
     };
     ```

3. **Small exercises:**
   - Write arrow functions:
     - `double(x)` → returns `x * 2`.
     - `greet(name)` → returns `"Hello, ${name}!"`.
     - `isEven(n)` → returns `true` if `n` is even.

### 3. Reflect (10–15 minutes)

- When would you still prefer to use a normal `function` declaration (e.g. named functions for clarity)?
- Which syntax do you like more now and why?

### 4. Stretch (optional, 20–30 minutes)

- In your To‑Do app code, identify one or two small functions and convert them to arrow functions (careful: event handlers can also be arrow functions, that’s fine).
- Ensure behavior is unchanged.

---

## Day 2 – Destructuring & Spread/Rest (Working with Objects/Arrays Efficiently)

**Goals:**
- Get comfortable with destructuring objects and arrays.
- Use spread (`...`) to create new arrays/objects instead of mutating.

### 1. Learn (40–60 minutes)

**Concepts:**
- Object destructuring:

  ```js
  const user = { name: "Alex", age: 25 };
  const { name, age } = user;
  ```

- Array destructuring:

  ```js
  const coords = [10, 20];
  const [x, y] = coords;
  ```

- Spread operator:
  - Arrays:

    ```js
    const nums2 = [...nums1, 4, 5];
    ```

  - Objects:

    ```js
    const user2 = { ...user1, age: 30 };
    ```

- Rest parameters:

  ```js
  const sum = (...nums) => { /* nums is an array */ };
  ```

**Read:**
- MDN: “Destructuring assignment”.
- MDN: “Spread syntax (...)”.

Write down:
- A destructuring example for an object.
- One example of adding an item to an array with spread.

### 2. Do (60–90 minutes)

Use `modern.js` or a new `destructuring.js`.

1. **Object destructuring:**

   ```js
   const user = { name: "Alex", age: 25, city: "Berlin" };
   const { name, age } = user;
   console.log(`${name} is ${age} years old.`);
   ```

   - Add more properties and destructure only what you need.

2. **Array destructuring:**

   ```js
   const colors = ["red", "green", "blue", "yellow"];
   const [primary, secondary, ...others] = colors;
   console.log(primary, secondary, others);
   ```

3. **Spread with arrays:**
   - Start with:

     ```js
     const nums = [1, 2, 3];
     const moreNums = [...nums, 4, 5];
     console.log(moreNums);
     ```

   - Create a new array `numsWithoutFirst` that doesn’t include the first item (hint: slice or destructuring + spread).

4. **Spread with objects:**
   - Given:

     ```js
     const baseUser = { name: "Alex", role: "user" };
     const adminUser = { ...baseUser, role: "admin" };
     ```

   - Log both to see the difference.
   - Create a `profile` object with base info and create a `updatedProfile` that overrides `city`.

### 3. Reflect (10–15 minutes)

- How can spread make code safer than mutating arrays/objects in place?
- Where could you use spread or destructuring in your To‑Do app code?

### 4. Stretch (optional, 20–30 minutes)

- In your To‑Do app:
  - If you have a function that modifies the `tasks` array directly, try rewriting it to create a **new array** with spread (e.g. for delete or toggle complete).

---

## Day 3 – Array Methods: map, filter, find, some, every

**Goals:**
- Learn the “80/20” array methods you’ll use constantly.
- Refactor loops into these methods.

### 1. Learn (45–60 minutes)

**Concepts:**
- `.map()` – transform each element into a new array.
- `.filter()` – keep only elements that match a condition.
- `.find()` – return the **first** element that matches a condition.
- `.some()` – does **any** element satisfy a condition?
- `.every()` – do **all** elements satisfy a condition?

**Read:**
- MDN: “Array.prototype.map”.
- MDN: “Array.prototype.filter”.
- MDN: “Array.prototype.find”.
- Skim `.some` and `.every`.

Write down:
- A quick one-line description of each (map, filter, find).
- One example use-case for `filter` in a to-do app.

### 2. Do (60–90 minutes)

Use `array-methods.js`.

1. **map:**
   - Start with:

     ```js
     const numbers = [1, 2, 3, 4];
     const doubled = numbers.map((n) => n * 2);
     console.log(doubled);
     ```

   - Create an array of names, create a new array of greetings: `["Hello, Alice", "Hello, Bob", ...]`.

2. **filter:**
   - Given:

     ```js
     const scores = [90, 55, 70, 100, 45];
     const passing = scores.filter((score) => score >= 60);
     console.log(passing);
     ```

   - Create an array of objects `{ name, isAdmin }` and filter only admins.

3. **find:**
   - Given:

     ```js
     const users = [
       { id: 1, name: "Alice" },
       { id: 2, name: "Bob" },
       { id: 3, name: "Charlie" }
     ];
     ```

   - Use `find` to get the user with id 2.

4. **some / every:**
   - `some`:
     - Check if there’s any score < 50.
   - `every`:
     - Check if all scores ≥ 50.

5. **Refactor an existing loop:**
   - Take a loop from Week 3 (e.g. building a list of passing grades) and refactor it using `filter`.

### 3. Reflect (10–15 minutes)

- When would you still use a `for` loop instead of `map` or `filter`?
- Which array method felt immediately useful? Which was confusing?

### 4. Stretch (optional, 20–30 minutes)

- In your To‑Do app:
  - Use `filter` to implement delete:
    - Replace the task array with `tasks.filter(t => t.id !== idToDelete)`.
  - Use `find` to implement toggle-completed:
    - Get the task by id and flip `completed`.

---

## Day 4 – Intro to Async: Callbacks, Promises, and fetch()

**Goals:**
- Understand synchronous vs asynchronous operations.
- Learn the basic idea of **promises**.
- Use `fetch()` with `.then()` to call a public API.

### 1. Learn (45–60 minutes)

**Concepts:**
- Sync vs async:
  - Sync: code runs line by line, each step waits.
  - Async: some operations (like network requests) take time and return later.
- Callbacks (just the idea; you won’t use them much directly now).
- Promises:
  - A promise represents a value that isn’t available yet.
  - States: pending → fulfilled or rejected.
- `fetch(url)`:
  - Returns a Promise that resolves to a Response.
  - Need `response.json()` to parse JSON.

**Read/Watch:**
- MDN: “Introducing asynchronous JavaScript”.
- MDN: “Using fetch”.
- Optionally a short video explaining promises and `fetch`.

Write down:
- One real-world example of async behavior (e.g. loading posts from a server).
- The steps to fetch JSON: `fetch(url) → response.json() → data`.

### 2. Do (60–90 minutes)

Create `week4-async/` with `index.html` and `api.js`.

1. **Basic fetch:**

   In `index.html`:

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <title>API Practice</title>
     </head>
     <body>
       <h1>API Practice</h1>
       <script src="api.js"></script>
     </body>
   </html>
   ```

   In `api.js`:

   ```js
   const url = "https://jsonplaceholder.typicode.com/posts";

   fetch(url)
     .then((response) => {
       console.log("Response object:", response);
       return response.json();
     })
     .then((data) => {
       console.log("Data:", data);
     })
     .catch((error) => {
       console.error("Error fetching data:", error);
     });
   ```

   - Open in browser and check DevTools console.

2. **Show first 5 titles in console:**
   - After you get `data` (array of posts), log the titles of the first 5 posts.

3. **Add a simple error case:**
   - Try changing the URL to something wrong (e.g. `/postsss`) and see the error.

### 3. Reflect (10–15 minutes)

- What part of `.then().then().catch()` chain feels confusing?
- Why do we need to call `response.json()`?

### 4. Stretch (optional, 20–30 minutes)

- Add a `<ul id="posts">` to `index.html`.
- In `api.js`, loop through the first 5 posts and create `<li>` elements with their titles, append to the `<ul>`.

---

## Day 5 – Async/Await & Rendering Fetched Data in the DOM

**Goals:**
- Use `async/await` instead of `.then()` chains.
- Build a small UI to display fetched data on the page.

### 1. Learn (40–60 minutes)

**Concepts:**
- `async` functions:
  - `async function fetchData() { ... }`
- `await`:
  - Waits for a promise to resolve.
- `try { ... } catch (error) { ... }` for error handling in async functions.

**Read:**
- MDN: “async function”.
- MDN: “await”.

Write down:
- Rewrite a basic `fetch().then().then()` in pseudocode using async/await.
- Where you’d use `try/catch`.

### 2. Do (60–90 minutes)

Continue in `week4-async/`, but create `users.html` and `users.js`.

1. **HTML structure:**

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>Users Dashboard</title>
     </head>
     <body>
       <main>
         <h1>Users Dashboard</h1>
         <button id="load-btn">Load Users</button>
         <p id="status"></p>
         <ul id="users-list"></ul>
       </main>
       <script src="users.js"></script>
     </body>
   </html>
   ```

2. **Fetch users with async/await (users.js):**

   ```js
   const btn = document.querySelector("#load-btn");
   const statusEl = document.querySelector("#status");
   const listEl = document.querySelector("#users-list");

   async function loadUsers() {
     statusEl.textContent = "Loading...";
     listEl.innerHTML = "";

     try {
       const response = await fetch("https://jsonplaceholder.typicode.com/users");

       if (!response.ok) {
         throw new Error(`HTTP error! status: ${response.status}`);
       }

       const users = await response.json();

       statusEl.textContent = `Loaded ${users.length} users.`;

       for (const user of users) {
         const li = document.createElement("li");
         li.textContent = `${user.name} (${user.email})`;
         listEl.appendChild(li);
       }
     } catch (error) {
       console.error(error);
       statusEl.textContent = "Failed to load users.";
     }
   }

   btn.addEventListener("click", loadUsers);
   ```

3. **Test behavior:**
   - Click “Load Users”.
   - See “Loading…” then the list.
   - Temporarily break the URL to test error state.

### 3. Reflect (10–15 minutes)

- Does `async/await` feel easier to read than `.then()` chains? Why/why not?
- How would you explain what `await` does in 1–2 sentences?

### 4. Stretch (optional, 20–30 minutes)

- Auto-load users when the page loads:
  - Call `loadUsers()` once at the bottom of `users.js`.
- Add a CSS file and style the list a bit.

---

## Day 6 – Building a Simple “Users Dashboard” with Search/Filter

**Goals:**
- Combine modern JS + async to build a small interactive app.
- Add **search/filter** on client-side using `filter()`.

### 1. Learn (30–45 minutes)

You’ve seen most core concepts already; focus today on **structuring** your code:

- Separating concerns:
  - One function to fetch data.
  - One function to render the list.
  - One function to handle search/filter.

Review:
- `.filter()`
- DOM `input` events: `input.addEventListener("input", ...)`

Write down:
- Rough plan for:
  - `let allUsers = []` (store data)
  - `renderUsers(users)` (render list)
  - `handleSearch()` (reads search term, calls `renderUsers` with filtered data)

### 2. Do (90–120 minutes)

Extend `users.html` and `users.js` into a small dashboard.

1. **Update HTML:**

   ```html
   <main>
     <h1>Users Dashboard</h1>

     <div>
       <button id="load-btn">Reload Users</button>
       <input
         id="search-input"
         type="text"
         placeholder="Search by name or email..."
       />
     </div>

     <p id="status"></p>

     <ul id="users-list"></ul>
   </main>
   ```

2. **JS structure (users.js):**

   ```js
   const btn = document.querySelector("#load-btn");
   const statusEl = document.querySelector("#status");
   const listEl = document.querySelector("#users-list");
   const searchInput = document.querySelector("#search-input");

   let allUsers = [];

   async function loadUsers() {
     statusEl.textContent = "Loading...";
     listEl.innerHTML = "";

     try {
       const response = await fetch("https://jsonplaceholder.typicode.com/users");
       if (!response.ok) throw new Error("Network response was not ok");
       const users = await response.json();
       allUsers = users;
       statusEl.textContent = `Loaded ${users.length} users.`;
       renderUsers(allUsers);
     } catch (error) {
       console.error(error);
       statusEl.textContent = "Failed to load users.";
     }
   }

   function renderUsers(users) {
     listEl.innerHTML = "";

     if (users.length === 0) {
       const li = document.createElement("li");
       li.textContent = "No users match your search.";
       listEl.appendChild(li);
       return;
     }

     for (const user of users) {
       const li = document.createElement("li");
       li.innerHTML = `<strong>${user.name}</strong> (${user.email}) - ${user.company.name}`;
       listEl.appendChild(li);
     }
   }

   function handleSearch() {
     const term = searchInput.value.toLowerCase();
     const filtered = allUsers.filter((user) => {
       const name = user.name.toLowerCase();
       const email = user.email.toLowerCase();
       return name.includes(term) || email.includes(term);
     });
     renderUsers(filtered);
   }

   btn.addEventListener("click", loadUsers);
   searchInput.addEventListener("input", handleSearch);

   // Initial load
   loadUsers();
   ```

   Try to write this from your mental model first, then compare.

3. **Test:**
   - Reload users.
   - Type in the search bar.
   - Check behavior when no results.

### 3. Reflect (10–15 minutes)

- Which part of this small app feels similar to your To‑Do app? Which is new?
- How does having `allUsers` as a source of truth help?

### 4. Stretch (optional, 20–30 minutes)

- Add a filter by company name with a `<select>` dropdown.
- Add a “clear search” button that empties the input and calls `renderUsers(allUsers)`.

---

## Day 7 – Consolidation Project & Review

**Goals:**
- Consolidate Week 4 concepts into a small project.
- Reflect on async/modern JS and your mental model.

You’ll create a **“Mini Posts Explorer”** using a public API.

### 1. Plan (20–30 minutes)

Decide on a simple app using JSONPlaceholder posts or another public JSON API.

Suggested features:
- Fetch a list of items from an API (`/posts`, `/photos`, etc.).
- Render them in a list or card layout.
- Add a search/filter input.
- Maybe a detail view (click item → show more info above/below).

Sketch or outline:
- What data you’ll show (title, body, author, etc.).
- Which elements you need: `input`, `button`, `ul`/`div` container.

Write down:
- The API endpoint you’ll use.
- The functions you think you’ll need (e.g. `loadPosts`, `renderPosts`, `handleSearch`).

### 2. Do – Build the Mini Project (90–120 minutes)

Create `posts-app/` with:

- `index.html`
- `style.css`
- `app.js`

1. **HTML skeleton:**

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>Posts Explorer</title>
       <link rel="stylesheet" href="style.css" />
     </head>
     <body>
       <main class="container">
         <h1>Posts Explorer</h1>

         <div class="controls">
           <button id="reload-btn">Reload Posts</button>
           <input
             id="search-input"
             type="text"
             placeholder="Search posts by title..."
           />
         </div>

         <p id="status"></p>

         <ul id="posts-list"></ul>
       </main>

       <script src="app.js"></script>
     </body>
   </html>
   ```

2. **Basic styling (style.css)** – reuse ideas from earlier weeks:

   - Make `.container` centered and limited width.
   - Style `.controls` as a flex row.
   - Style `li` posts nicely.

3. **JS logic (app.js):**

   - Similar pattern to the Users Dashboard:

     ```js
     const reloadBtn = document.querySelector("#reload-btn");
     const searchInput = document.querySelector("#search-input");
     const statusEl = document.querySelector("#status");
     const listEl = document.querySelector("#posts-list");

     let allPosts = [];

     async function loadPosts() {
       statusEl.textContent = "Loading posts...";
       listEl.innerHTML = "";

       try {
         const response = await fetch("https://jsonplaceholder.typicode.com/posts");
         if (!response.ok) throw new Error("Network error");
         const posts = await response.json();
         allPosts = posts.slice(0, 50); // limit for readability
         statusEl.textContent = `Loaded ${allPosts.length} posts.`;
         renderPosts(allPosts);
       } catch (error) {
         console.error(error);
         statusEl.textContent = "Failed to load posts.";
       }
     }

     function renderPosts(posts) {
       listEl.innerHTML = "";

       if (posts.length === 0) {
         const li = document.createElement("li");
         li.textContent = "No posts match your search.";
         listEl.appendChild(li);
         return;
       }

       for (const post of posts) {
         const li = document.createElement("li");
         li.innerHTML = `
           <h2>${post.title}</h2>
           <p>${post.body}</p>
         `;
         listEl.appendChild(li);
       }
     }

     function handleSearch() {
       const term = searchInput.value.toLowerCase();
       const filtered = allPosts.filter((post) =>
         post.title.toLowerCase().includes(term)
       );
       renderPosts(filtered);
     }

     reloadBtn.addEventListener("click", loadPosts);
     searchInput.addEventListener("input", handleSearch);

     loadPosts();
     ```

   - Try to implement from your own understanding first, *then* compare.

### 3. Self-Review Checklist (20–30 minutes)

Go through:

- JS features:
  - [ ] Did you use `let`/`const` appropriately?
  - [ ] Do you use arrow functions where helpful?
  - [ ] Did you use `map`/`filter` (at least filter for search)?

- Async:
  - [ ] Do you use `async/await` correctly?
  - [ ] Do you handle errors with `try/catch`?
  - [ ] Do you show loading and error messages to the user?

- Structure:
  - [ ] Is data stored in a single source of truth (`allPosts`)?
  - [ ] Do you have a clear `renderPosts()` function?
  - [ ] Is the code split into small functions with clear responsibilities?

Write 3 things you understand well now and 2 concepts you still find tricky.

### 4. Reflect (15–20 minutes)

In your notes:
- How has your mental model of “data flow” in an app changed since Week 3?
- Describe in your own words what happens when:
  - You open `posts-app/index.html`.
  - `loadPosts()` runs.
  - You type in the search input.

Also, note:
- Which concept this week was hardest (destructuring? async/await? fetch?).
- A small plan to revisit that concept (e.g. “I’ll re-implement the Users Dashboard next week without looking at my code”).

### 5. Stretch (optional, 30–45 minutes)

- Add a “view details” feature:
  - When you click a post title, show its full content in a separate `<section id="details">` above or below the list.
- Add a **loading spinner** (CSS animation or simple “...” animation).
- Experiment with another public API (e.g. a free Pokemon API, countries API, etc.) and adapt your app.

---

If you’d like next, I can:
- Create a **Week 5 daily plan** to start React, or  
- Help you refactor the Users Dashboard / Posts Explorer to cleaner, more reusable code before moving into React.
