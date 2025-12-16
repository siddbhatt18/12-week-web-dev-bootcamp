**Week 3 Theme:** JavaScript fundamentals + first small interactions in the browser.  
Assume ~2 hours/day. Work in a `week3/` folder but feel free to link some scripts to your Week 2 portfolio too.

---

## Day 1 – JavaScript Basics: Values, Variables, and Expressions

**Objectives:**
- Understand what JavaScript is used for.
- Learn variables, basic types, and expressions.

### 1. Concept (30–40 min)
Read/learn:
- Where JS runs:
  - In the browser (we’ll use this now).
- Linking JS to HTML:
  ```html
  <script src="script.js"></script>
  ```
- Basic concepts:
  - Values and types: number, string, boolean, `null`, `undefined`
  - Variables with `let` and `const`
  - Simple expressions and operations (`+`, `-`, `*`, `/`, `%`)
  - String concatenation and template literals:

    ```js
    const name = "Alex";
    console.log(`Hello, ${name}!`);
    ```

### 2. Practice: simple scripts (60–70 min)
Create `week3/day1.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>JS Basics - Day 1</title>
  </head>
  <body>
    <h1>Open the console</h1>
    <script src="day1.js"></script>
  </body>
</html>
```

Create `day1.js`:
- Declare a few variables:

  ```js
  const firstName = "YourName";
  let age = 20; // or your age
  const isStudent = true;
  ```

- Log them:

  ```js
  console.log("Name:", firstName);
  console.log("Age:", age);
  console.log("Is student:", isStudent);
  ```

- Perform operations:
  - Create `const yearOfBirth = 2025 - age;`
  - Log a sentence using template literals:  
    `"Hi, I'm YourName and I was born in 2005."` (or whatever fits).

- Try changing values and reloading the browser.

### 3. Reflection (5–10 min)
Create `notes-day1.txt`:
- In your own words: What is a variable? What’s the difference between `let` and `const` at a high level?

---

## Day 2 – Conditionals and Basic Logic

**Objectives:**
- Use `if/else` to add decision-making logic.
- Write small “logic snippets.”

### 1. Concept (30–40 min)
Learn:
- Comparison operators: `>`, `<`, `>=`, `<=`, `===`, `!==`
- Logical operators: `&&`, `||`, `!`
- `if`, `else if`, `else` structure:

  ```js
  if (condition) {
    // ...
  } else if (otherCondition) {
    // ...
  } else {
    // ...
  }
  ```

### 2. Practice: simple decision programs (60–70 min)
Create `day2.html` + `day2.js` (similar structure to Day 1).

In `day2.js`:
- Example 1 – Age check:

  ```js
  const age = 17;

  if (age >= 18) {
    console.log("You are an adult.");
  } else {
    console.log("You are a minor.");
  }
  ```

- Example 2 – Grade checker:
  - Create a `score` variable (0–100).
  - Use if/else to print `"A"`, `"B"`, `"C"`, `"D"`, `"F"` based on the score.
- Example 3 – Discount logic:
  - Variables: `isMember`, `cartTotal`.
  - If `isMember` is true and `cartTotal > 50`, log `"You get a discount!"`, else `"No discount"`.

Experiment:
- Change values and see different outputs.
- Add one more scenario of your choice (e.g., “time of day” greeting).

### 3. Reflection (5–10 min)
In `notes-day2.txt`:
- What’s a real-world action in a website that might use `if/else` (e.g., showing logged-in vs logged-out view)?

---

## Day 3 – Functions and Reusability

**Objectives:**
- Understand what functions are and why they’re useful.
- Write and call simple functions.

### 1. Concept (30–40 min)
Learn:
- Declaring functions:

  ```js
  function greet(name) {
    console.log(`Hello, ${name}!`);
  }
  ```

- Parameters vs arguments.
- Return values:

  ```js
  function add(a, b) {
    return a + b;
  }
  const sum = add(2, 3);
  ```

- Function naming: make names describe what they do.

### 2. Practice: utility functions (60–70 min)
Create `day3.html` + `day3.js`.

In `day3.js`:
- Function 1 – `calculateRectangleArea(width, height)`:
  - Return the area.
  - Log several calls with different values.
- Function 2 – `isAdult(age)`:
  - Return `true` if age >= 18, else `false`.
- Function 3 – `formatGreeting(name, language)`:
  - If language is `"en"`, return `"Hello, <name>!"`
  - If `"es"`, return `"Hola, <name>!"`
  - Else, return `"<name>, I don't know your language."`
- Call these functions with multiple inputs.

Optional:
- Write a `calculateDiscount(price, isMember)` function.

### 3. Reflection (5–10 min)
In `notes-day3.txt`:
- When would you use a function instead of repeating code?

---

## Day 4 – Arrays and Loops

**Objectives:**
- Store lists of data in arrays.
- Iterate over arrays with loops.

### 1. Concept (30–40 min)
Learn:
- Arrays:
  ```js
  const numbers = [10, 20, 30];
  const fruits = ["apple", "banana", "orange"];
  ```
- Access by index (`numbers[0]`).
- Array length: `.length`.
- `for` loop:

  ```js
  for (let i = 0; i < fruits.length; i++) {
    console.log(fruits[i]);
  }
  ```

- Basic methods:
  - `push`, `pop`, `shift`, `unshift` (you can focus on `push` for now).

### 2. Practice: list operations (60–70 min)
Create `day4.html` + `day4.js`.

In `day4.js`:
- Create an array of your 5 favorite movies or books.
- Use a `for` loop to log each one with a number:
  - `"1. MovieName"`, `"2. MovieName"`, etc.
- Create an array of numbers and:
  - Use a loop to compute the sum and average.
- Practice `push`:
  - Start with an empty `const tasks = [];`
  - `tasks.push("Learn JS"); tasks.push("Build project");`
  - Loop through and log `"Task: <task>"`.

Optional:
- Create a function `printArray(arr)` that logs all elements of any array.

### 3. Reflection (5–10 min)
In `notes-day4.txt`:
- Describe a real list on a website that could be represented as an array (e.g., products, comments).

---

## Day 5 – Objects and Basic Data Modeling

**Objectives:**
- Use objects to group related data.
- Combine arrays and objects.

### 1. Concept (30–40 min)
Learn:
- Objects:

  ```js
  const user = {
    name: "Alex",
    age: 25,
    isStudent: true,
  };
  ```

- Accessing properties: `user.name`, `user["age"]`.
- Adding/modifying properties: `user.country = "USA";`.

### 2. Practice: modeling data (60–70 min)
Create `day5.html` + `day5.js`.

In `day5.js`:
- Create a `user` object with:
  - `name`, `age`, `email`, `skills` (array), `isLookingForJob` (boolean).
- Log a formatted string like:
  - `"Alex (25) - Email: alex@example.com. Skills: HTML, CSS, JS"`.
- Add a method to the object (optional but good practice):

  ```js
  const user = {
    name: "Alex",
    age: 25,
    greet() {
      console.log(`Hi, I'm ${this.name} and I'm ${this.age} years old.`);
    }
  };

  user.greet();
  ```

- Create an array of `project` objects:
  ```js
  const projects = [
    { title: "Portfolio", tech: ["HTML", "CSS"], completed: true },
    { title: "Todo App", tech: ["JS"], completed: false },
  ];
  ```
- Loop through `projects` and log each project’s title and technologies.

### 3. Reflection (5–10 min)
In `notes-day5.txt`:
- Why might objects and arrays together be useful when modeling real app data?

---

## Day 6 – DOM Basics: Connecting JS to the Page

**Objectives:**
- Select HTML elements with JS.
- Change text and styles via the DOM.

### 1. Concept (30–40 min)
Learn:
- DOM = Document Object Model (JS view of the HTML page).
- Selecting elements:
  ```js
  const heading = document.querySelector("h1");
  const btn = document.querySelector("#myButton");
  const items = document.querySelectorAll(".item");
  ```
- Changing content:
  - `element.textContent = "New text";`
- Changing styles:
  - `element.style.color = "red";`

### 2. Practice: simple DOM manipulations (60–70 min)
Create `day6-dom.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>DOM Basics - Day 6</title>
  </head>
  <body>
    <h1 id="main-title">Original Title</h1>
    <p class="description">This is a description.</p>

    <ul id="item-list">
      <li class="item">Item 1</li>
      <li class="item">Item 2</li>
      <li class="item">Item 3</li>
    </ul>

    <script src="day6.js"></script>
  </body>
</html>
```

In `day6.js`:
- Select the title and change its text:

  ```js
  const title = document.querySelector("#main-title");
  title.textContent = "Updated Title from JavaScript";
  ```

- Change description text and color.
- Select all `.item` elements with `querySelectorAll` and:
  - Loop through them and append `" (updated)"` to each text.
  - Optionally change their background color.

### 3. Reflection (5–10 min)
In `notes-day6.txt`:
- What’s the DOM, in your own words?
- How do you select an element by class? By ID?

---

## Day 7 – DOM Events + Simple Interaction on Your Portfolio

**Objectives:**
- Respond to user events (clicks).
- Add a small interactive feature to your portfolio.

### 1. Concept (30–40 min)
Learn:
- Event listeners:
  ```js
  const button = document.querySelector("button");
  button.addEventListener("click", () => {
    console.log("Button clicked!");
  });
  ```
- Common events:
  - `click`, `submit`, `input`, `change`.
- Basic pattern:
  - Select element → `addEventListener` → define handler function.

### 2. Practice: small interactive demo (45–60 min)
Create `day7-events.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Events - Day 7</title>
  </head>
  <body>
    <h1>Click the button</h1>
    <button id="color-btn">Change Background</button>
    <p id="status">Background is white.</p>

    <script src="day7.js"></script>
  </body>
</html>
```

In `day7.js`:
- Select the button and paragraph.
- On click:
  - Toggle the page background between white and a color.
  - Update the status text accordingly.

Example:

```js
const btn = document.querySelector("#color-btn");
const statusText = document.querySelector("#status");
let isWhite = true;

btn.addEventListener("click", () => {
  if (isWhite) {
    document.body.style.backgroundColor = "#f0f8ff";
    statusText.textContent = "Background is light blue.";
  } else {
    document.body.style.backgroundColor = "white";
    statusText.textContent = "Background is white.";
  }
  isWhite = !isWhite;
});
```

### 3. Apply to your portfolio (optional but recommended) (20–30 min)
- Open your Week 2 `portfolio.html`.
- Add a button or link, e.g., “Toggle Dark Mode” or “Show More About Me.”
- Link a new script file, e.g.:

  ```html
  <script src="portfolio.js"></script>
  ```

- In `portfolio.js`, add:
  - An event listener that toggles a CSS class on `<body>` (like `.dark-mode`).
  - In your CSS, define `.dark-mode` styles (different background/text colors).

This gives you your **first real interactive feature** on a real page.

### 4. Weekly reflection (10–15 min)
In `notes-week3-summary.txt`:
- What parts of JS do you feel okay with now (variables, functions, arrays, basic DOM)?
- What still feels confusing (e.g., loops, objects, event handling)?
- One specific goal for Week 4 (e.g., “Get comfortable manipulating the DOM more,” or “Understand localStorage”).

---

If you’d like, next I can create a **Week 4 day-by-day plan** focused on deeper DOM work, building a small vanilla JS project (like a TODO app), and starting to use `localStorage` and simple APIs.
