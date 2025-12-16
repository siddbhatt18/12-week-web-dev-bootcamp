**Week 5 Theme:** Asynchronous JavaScript, `fetch`, working with APIs, and building your API‑powered dashboard (P3).  
Assume ~2 hours/day. Work in a `week5/` folder.

You’ll end the week with **P3 – API‑Powered Dashboard (frontend + public API)**.

---

## Day 1 – Understanding Async JS & `fetch`

**Objectives:**
- Understand why async code exists.
- Learn the basics of Promises and `fetch`.

### 1. Concept (30–40 min)
Study:
- Why async? (network calls take time; JS is single-threaded)
- Call stack & the idea of “doing other work while waiting”
- Promises (high level):
  - Promise states: pending, fulfilled, rejected
- `fetch` basics:
  ```js
  fetch("https://api.example.com/data")
    .then(response => response.json())
    .then(data => {
      console.log(data);
    })
    .catch(error => {
      console.error("Error:", error);
    });
  ```

- `async/await` as syntactic sugar:
  ```js
  async function loadData() {
    try {
      const response = await fetch("https://api.example.com/data");
      const data = await response.json();
      console.log(data);
    } catch (error) {
      console.error("Error:", error);
    }
  }
  ```

### 2. Practice: first `fetch` call (45–60 min)
Create `day1-fetch.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Week 5 - Day 1</title>
  </head>
  <body>
    <h1>Check the console for API data</h1>
    <script src="day1.js"></script>
  </body>
</html>
```

Create `day1.js`:
- Use a simple public API (no auth) such as:
  - https://jsonplaceholder.typicode.com/posts/1
  - https://api.quotable.io/random (quotes)
- Implement with `async/await`:

  ```js
  async function fetchPost() {
    try {
      const response = await fetch("https://jsonplaceholder.typicode.com/posts/1");
      if (!response.ok) {
        throw new Error("Network response was not ok");
      }
      const data = await response.json();
      console.log("Post data:", data);
    } catch (error) {
      console.error("Fetch error:", error);
    }
  }

  fetchPost();
  ```

- Change the URL to a wrong one once to see an error in the console.

### 3. Reflection (5–10 min)
In `notes-day1.txt`:
- Why is async behavior important for network requests?
- What does `await` actually “wait” for?

---

## Day 2 – Displaying API Data in the DOM

**Objectives:**
- Take fetched data and show it on the page (not just in console).
- Handle loading state and basic error display.

### 1. Concept (20–30 min)
Focus on:
- Pattern: “loading → success or error”
- DOM updates based on async data:
  - Set `textContent` or build elements when data arrives.
- Simple loading feedback:
  - e.g., text “Loading…” before data arrives, clear when done.

### 2. Practice: random quote viewer (60–70 min)
Create `day2-quote.html`:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Random Quote</title>
  </head>
  <body>
    <main>
      <h1>Random Quote</h1>
      <p id="status">Click the button to load a quote.</p>
      <blockquote id="quote"></blockquote>
      <p id="author"></p>
      <button id="load-quote-btn">Load Quote</button>
    </main>

    <script src="day2.js"></script>
  </body>
</html>
```

Create `day2.js` using the Quotable API:

```js
const statusEl = document.querySelector("#status");
const quoteEl = document.querySelector("#quote");
const authorEl = document.querySelector("#author");
const button = document.querySelector("#load-quote-btn");

async function loadQuote() {
  statusEl.textContent = "Loading...";
  quoteEl.textContent = "";
  authorEl.textContent = "";

  try {
    const response = await fetch("https://api.quotable.io/random");
    if (!response.ok) {
      throw new Error("Network response was not ok");
    }
    const data = await response.json();
    quoteEl.textContent = data.content;
    authorEl.textContent = `— ${data.author}`;
    statusEl.textContent = "Here is your quote:";
  } catch (error) {
    console.error(error);
    statusEl.textContent = "Error loading quote. Please try again.";
  }
}

button.addEventListener("click", loadQuote);
```

### 3. Reflection (5–10 min)
In `notes-day2.txt`:
- What user feedback is important when loading data from an API?
- How did you handle errors?

---

## Day 3 – Working with URL Parameters & User Input

**Objectives:**
- Use user input (e.g., a text field) to build a dynamic API request.
- Practice reading API docs and forming URLs.

### 1. Concept (25–30 min)
Learn:
- URL query parameters:
  - Example: `https://api.example.com/search?query=javascript&limit=5`
- Taking user input and building the URL string.
- Encoding user input safely with `encodeURIComponent` (basic introduction):

  ```js
  const term = encodeURIComponent(userInput);
  const url = `https://api.example.com/search?q=${term}`;
  ```

### 2. Practice: simple search UI (weather or quotes) (60–70 min)
Pick one:

**Option A – Weather (OpenWeatherMap, requires free API key)**  
If you don’t want to register yet, use Option B.

**Option B – Quotable search (no auth)**  
Docs: https://github.com/lukePeavey/quotable#list-quotes

Example endpoint:  
`https://api.quotable.io/quotes?author=Albert%20Einstein`

Create `day3-search.html` (example with author search):

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Quote Search</title>
  </head>
  <body>
    <h1>Search Quotes by Author</h1>
    <form id="search-form">
      <input id="author-input" type="text" placeholder="Enter author name" />
      <button type="submit">Search</button>
    </form>

    <p id="status"></p>
    <ul id="results"></ul>

    <script src="day3.js"></script>
  </body>
</html>
```

In `day3.js`:
- On form submit:
  - `preventDefault`.
  - Read `author-input` value.
  - Build URL:  
    ```js
    const author = encodeURIComponent(authorInput.value.trim());
    const url = `https://api.quotable.io/quotes?author=${author}`;
    ```
- Set `status` to “Loading…”.
- Fetch data.
- On success, render a list of quotes.
  - If no results, show “No quotes found.”
- On error, show a user-friendly message.

### 3. Reflection (5–10 min)
In `notes-day3.txt`:
- What part of reading the API docs was tricky?
- How did you handle empty input from the user?

---

## Day 4 – Structuring a Small “Dashboard” UI

**Objectives:**
- Plan your API-powered dashboard (P3).
- Build the static UI and layout with HTML/CSS.

### 1. Plan P3 dashboard (20–30 min)
Create `week5/notes-day4.txt` and decide:
- What API(s) you’ll use. Good beginner options:
  - **Weather** (OpenWeatherMap – requires signup; or another free weather API)
  - **Quotes** (Quotable)
  - **News** (NewsAPI – free tier with key, or another similar)
  - **Crypto prices** (CoinGecko – no key needed)
- Example idea:
  - Left card: Weather for a city.
  - Right card: Random quote of the day.
  - Optional: Another card with some fun API (e.g., cat facts, joke).

Define:
- Which inputs user can provide (city, keyword, etc.).
- What you’ll display in each “card.”

### 2. Build static dashboard layout (60–70 min)
Create `dashboard.html` + `dashboard.css`:

Suggested structure:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>My API Dashboard</title>
    <link rel="stylesheet" href="dashboard.css" />
  </head>
  <body>
    <header class="header">
      <h1>My API Dashboard</h1>
    </header>

    <main class="dashboard">
      <section class="card" id="card-1">
        <h2>Weather</h2>
        <form id="weather-form">
          <input id="city-input" type="text" placeholder="Enter city" />
          <button type="submit">Get Weather</button>
        </form>
        <p id="weather-status"></p>
        <div id="weather-result"></div>
      </section>

      <section class="card" id="card-2">
        <h2>Quote</h2>
        <p id="quote-status">Click to get a quote.</p>
        <blockquote id="quote-text"></blockquote>
        <p id="quote-author"></p>
        <button id="quote-btn">Load Quote</button>
      </section>

      <!-- Optional 3rd card later -->
    </main>

    <script src="dashboard.js"></script>
  </body>
</html>
```

In `dashboard.css`:
- Use Flexbox or Grid to create responsive card layout.
- Style header and cards with some padding, border radius, and subtle colors.
- Ensure it looks reasonable on mobile (stacked cards).

### 3. Reflection (5–10 min)
In `notes-day4.txt`:
- What 2–3 data points do you definitely want the user to see for each card (e.g., temperature, description, quote text)?

---

## Day 5 – Wiring Up the First Card (e.g., Weather)

**Objectives:**
- Connect the first dashboard card to a real API.
- Handle loading, success, and error states.

### 1. Concept (20–30 min)
Focus on:
- Reusing patterns from Days 2–3.
- Validating input (e.g., city name not empty).
- Thinking about how to **structure code by feature**:
  - Functions like `fetchWeather(city)` and `renderWeather(data)`.

### 2. Implement first card (60–70 min)
In `dashboard.js`:
- Setup:
  ```js
  // WEATHER
  const weatherForm = document.querySelector("#weather-form");
  const cityInput = document.querySelector("#city-input");
  const weatherStatus = document.querySelector("#weather-status");
  const weatherResult = document.querySelector("#weather-result");
  ```

- Choose your weather API:
  - If using OpenWeatherMap:
    - Get an API key (free).
    - Use endpoint like:  
      `https://api.openweathermap.org/data/2.5/weather?q={CITY}&appid={API_KEY}&units=metric`
- Implement:

  ```js
  async function fetchWeather(city) {
    const apiKey = "YOUR_API_KEY_HERE"; // or from config.js/env in future
    const url = `https://api.openweathermap.org/data/2.5/weather?q=${encodeURIComponent(
      city
    )}&appid=${apiKey}&units=metric`;

    try {
      weatherStatus.textContent = "Loading...";
      weatherResult.textContent = "";

      const response = await fetch(url);
      if (!response.ok) {
        throw new Error("City not found or network error");
      }
      const data = await response.json();
      renderWeather(data);
      weatherStatus.textContent = "Done.";
    } catch (error) {
      console.error(error);
      weatherStatus.textContent = "Error loading weather. Try again.";
    }
  }

  function renderWeather(data) {
    const temp = data.main.temp;
    const desc = data.weather[0].description;
    const cityName = data.name;
    weatherResult.innerHTML = `
      <p><strong>${cityName}</strong></p>
      <p>Temperature: ${temp} °C</p>
      <p>${desc}</p>
    `;
  }

  weatherForm.addEventListener("submit", (event) => {
    event.preventDefault();
    const city = cityInput.value.trim();
    if (!city) {
      weatherStatus.textContent = "Please enter a city name.";
      return;
    }
    fetchWeather(city);
  });
  ```

- Test various cities and error cases (empty input, nonsense city).

### 3. Reflection (5–10 min)
In `notes-day5.txt`:
- What happens when you enter an invalid city name?
- How did you communicate that to the user?

---

## Day 6 – Second Card (Quotes or Another API) & Code Cleanup

**Objectives:**
- Implement a second card (quotes or any other API).
- Start organizing code into small, clear functions.

### 1. Concept (20–30 min)
Think about:
- Don’t write everything in one giant function.
- Break down features:
  - Weather: `fetchWeather`, `renderWeather`, `handleWeatherSubmit`.
  - Quote: `fetchQuote`, `renderQuote`, `handleQuoteClick`.

### 2. Implement second card (60–70 min)
Using the Quotable API again for quotes.

In `dashboard.js`, add:

```js
// QUOTES
const quoteStatus = document.querySelector("#quote-status");
const quoteText = document.querySelector("#quote-text");
const quoteAuthor = document.querySelector("#quote-author");
const quoteBtn = document.querySelector("#quote-btn");

async function fetchQuote() {
  quoteStatus.textContent = "Loading...";
  quoteText.textContent = "";
  quoteAuthor.textContent = "";

  try {
    const response = await fetch("https://api.quotable.io/random");
    if (!response.ok) {
      throw new Error("Error fetching quote");
    }
    const data = await response.json();
    renderQuote(data);
    quoteStatus.textContent = "Here is your quote:";
  } catch (error) {
    console.error(error);
    quoteStatus.textContent = "Error loading quote.";
  }
}

function renderQuote(data) {
  quoteText.textContent = data.content;
  quoteAuthor.textContent = `— ${data.author}`;
}

quoteBtn.addEventListener("click", fetchQuote);
```

### 3. Code organization pass (20–25 min)
- Group related code with comments (e.g., `// WEATHER SECTION`, `// QUOTES SECTION`).
- Ensure function names are descriptive.
- Remove unnecessary `console.log` statements.
- Make sure you handle “loading” and “error” states consistently for both cards.

### 4. Reflection (5–10 min)
In `notes-day6.txt`:
- Which card (weather or quotes) was easier to wire up? Why?
- What part of the code feels repetitive or like it could be abstracted later?

---

## Day 7 – Dashboard Polish, Edge Cases & Review

**Objectives:**
- Polish the UI/UX a bit.
- Handle edge cases.
- Reflect on async concepts and your P3 project as a whole.

### 1. UI polish (30–40 min)
In `dashboard.css`:
- Improve spacing and typography in cards.
- Add a subtle background color or gradient to the header.
- Highlight error messages with a different color (e.g., red) and loading state with something neutral.
- Ensure cards stack nicely on mobile screens.

### 2. Edge cases & improvements (30–40 min)
Test:
- Empty city input, invalid city input, network offline (simulate by turning off wifi or using a bad URL).
- Click quote button repeatedly – does it still behave correctly?
- Optional minor enhancements:
  - Disable submit button while loading (then re-enable).
  - Show last updated time for weather or quote.

E.g., for button disabling:

```js
quoteBtn.disabled = true;
// after success or error
quoteBtn.disabled = false;
```

### 3. Light code review & comments (15–20 min)
- Add short comments to key functions explaining what they do.
- Scan for:
  - Clear variable names.
  - Avoiding duplicate logic (e.g., repeated loading/error handling).
- If using Git, commit with a message like `"Finish API dashboard with weather and quotes"`.

### 4. Weekly reflection (10–15 min)
In `notes-week5-summary.txt`:
- What did you learn about:
  - Promises and `async/await`?
  - Using `fetch` to call APIs?
  - Handling loading and error states in the UI?
- Which parts still feel unclear (e.g., error handling, building URLs, parsing nested JSON)?
- One concrete improvement you’d like to make to this dashboard later (e.g., add a third card, save last searched city in `localStorage`, style upgrades).

---

If you’d like, next I can create a **Week 6 day‑by‑day plan** focused on:
- Transitioning to backend basics with Node.js and Express.
- Building your first simple REST API to complement what you just did on the frontend.
