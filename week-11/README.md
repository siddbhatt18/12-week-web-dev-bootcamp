Here’s your **Week 11 (Days 1–7) plan**, focused on building the **backend for your capstone full‑stack project** (Task Manager / Habit Tracker / etc. you defined in Week 10).

Assume ~2–3 hours/day.  
Each day: **Learn → Do → Reflect → Stretch**.  
By the end of Week 11 you should have:

- A working **Express + Mongo + Auth** backend for your capstone.  
- Models, routes, validation, and ownership logic for your main resources.  
- A tested API (via Postman/Insomnia) ready for frontend integration next week.

I’ll call your main resource `Item` generically; substitute `Task`, `Habit`, `Project`, etc. as needed.

---

## Day 1 – Set Up Dedicated Backend Project & Base Models

**Goals:**
- Create a clean backend project for the capstone.
- Set up DB connection, auth, and skeleton for main models.

### 1. Learn (20–30 minutes)

You already know most of this; today is more about application:

- Think about **what you’ll reuse** from your Todos backend:
  - DB connect logic.
  - User model & auth routes.
  - Auth middleware.
- Think about **what needs to change**:
  - New `Item` model fields.
  - New routes/validation rules.

In your notes:
- List which files you’ll copy/adapt from your previous API.
- List what’s new (e.g. `Task`/`Habit` model fields).

### 2. Do (60–90 minutes)

1. **Create new backend project folder**, e.g. `capstone-api`:

   ```bash
   mkdir capstone-api
   cd capstone-api
   npm init -y
   npm install express mongoose dotenv cors bcrypt jsonwebtoken
   npm install --save-dev nodemon
   ```

2. **Project structure:**

   Create folders:

   - `config/` – `db.js`
   - `models/` – `User.js`, `Item.js` (placeholder)
   - `routes/` – `auth.js`, `items.js` (placeholder)
   - `middleware/` – `auth.js`
   - `controllers/` (optional, you can add later this week)

3. **Set up basic server in `index.js`:**

   ```js
   require("dotenv").config();
   const express = require("express");
   const cors = require("cors");
   const connectDB = require("./config/db");

   const app = express();
   const PORT = process.env.PORT || 3000;

   app.use(cors());
   app.use(express.json());

   connectDB();

   app.get("/", (req, res) => {
     res.send("Capstone API");
   });

   app.listen(PORT, () => {
     console.log(`Server running on http://localhost:${PORT}`);
   });
   ```

4. **DB connection (`config/db.js`):**

   ```js
   const mongoose = require("mongoose");

   async function connectDB() {
     const uri = process.env.MONGODB_URI;
     if (!uri) {
       console.error("MONGODB_URI not set");
       process.exit(1);
     }
     try {
       await mongoose.connect(uri);
       console.log("MongoDB connected");
     } catch (err) {
       console.error("MongoDB connection error:", err.message);
       process.exit(1);
     }
   }

   module.exports = connectDB;
   ```

5. **`.env` file:**

   ```env
   MONGODB_URI=your-connection-string-here
   JWT_SECRET=some-long-random-secret
   JWT_EXPIRES_IN=7d
   PORT=3000
   ```

6. **Add dev script in `package.json`:**

   ```json
   "scripts": {
     "dev": "nodemon index.js"
   }
   ```

7. **Draft main `Item` model structure in notes** (no code yet):  
   Example `Task`:

   - `title`: String, required, min length
   - `description`: String
   - `status`: enum `"todo" | "in-progress" | "done"`
   - `dueDate`: Date (optional)
   - `user`: ObjectId ref `User`
   - timestamps

### 3. Reflect (10–15 minutes)

- What did you reuse from old projects? What’s new?
- Does the current project structure feel understandable when you look at it top-down?

### 4. Stretch (optional, 20–30 minutes)

- Add a simple `/api/health` route that checks `mongoose.connection.readyState` and returns DB status.
- Initialize a Git repo and make your first commit with this base setup.

---

## Day 2 – User & Item Models, Basic Auth Routes

**Goals:**
- Implement `User` model & auth routes (register/login) similar to Week 9.
- Implement `Item` model with proper schema & validation.

### 1. Learn (20–30 minutes)

Conceptual work:

- Revisit your Week 9 `User` model and adjust if needed:
  - Do you want a `name` or `role` field for this app?
- Design `Item` validation rules:
  - What’s required?
  - What default values make sense?

In your notes:
- Write validation rules for `Item`, e.g.:
  - `title` required, min length 3.
  - `status` default `"todo"`.

### 2. Do (60–90 minutes)

1. **`models/User.js`:** reuse from previous project (with any tweaks like `name`, `role`).

2. **`routes/auth.js`:** copy and adapt register/login routes from your Week 9 API:
   - POST `/api/auth/register`
   - POST `/api/auth/login`

   Wire in `index.js`:

   ```js
   const authRouter = require("./routes/auth");
   app.use("/api/auth", authRouter);
   ```

3. **`models/Item.js`:**

   Example for Task:

   ```js
   const mongoose = require("mongoose");

   const itemSchema = new mongoose.Schema(
     {
       title: {
         type: String,
         required: [true, "Title is required"],
         trim: true,
         minlength: [3, "Title must be at least 3 characters"],
       },
       description: {
         type: String,
         trim: true,
       },
       status: {
         type: String,
         enum: ["todo", "in-progress", "done"],
         default: "todo",
       },
       dueDate: {
         type: Date,
       },
       user: {
         type: mongoose.Schema.Types.ObjectId,
         ref: "User",
         required: true,
       },
     },
     { timestamps: true }
   );

   const Item = mongoose.model("Item", itemSchema);

   module.exports = Item;
   ```

4. **Smoke test DB with a quick temp route:**

   ```js
   const Item = require("./models/Item");

   app.get("/api/test-item", async (req, res) => {
     try {
       const item = await Item.create({
         title: "Test item",
         user: new mongoose.Types.ObjectId(), // temp fake id
       });
       res.json(item);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to create test item" });
     }
   });
   ```

   - Hit it once to ensure the model works; then remove/disable later.

### 3. Reflect (10–15 minutes)

- How does this `Item` model align with your Week 10 design?
- Are you missing any fields? Overcomplicating any?

### 4. Stretch (optional, 20–30 minutes)

- Add a `priority` or `frequency` field (for habits) with `enum`.
- Consider indexing `user` + `status` combinations (optional, just to be aware of indexes).

---

## Day 3 – CRUD API for Items (User-Owned, Basic Validation)

**Goals:**
- Implement full CRUD for `Item` (create, list, get one, update, delete).
- Ensure routes are protected and scoped to the authenticated user.

### 1. Learn (20–30 minutes)

You know the patterns; focus on designing them cleanly:

- Decide on base path: `/api/items` or more specific (`/api/tasks`, `/api/habits`).
- For each route:
  - List what it receives (`params`, `query`, `body`).
  - List what it returns (status, JSON shape).

In notes:
- Write the list of endpoints:
  - GET `/api/items`
  - POST `/api/items`
  - GET `/api/items/:id`
  - PUT `/api/items/:id`
  - DELETE `/api/items/:id`

### 2. Do (90–120 minutes)

1. **Auth middleware (`middleware/auth.js`):** reuse from Week 9.

2. **`routes/items.js`:**

   ```js
   const express = require("express");
   const Item = require("../models/Item");
   const auth = require("../middleware/auth");

   const router = express.Router();

   // All routes here require auth
   router.use(auth);

   // GET /api/items
   router.get("/", async (req, res) => {
     try {
       const items = await Item.find({ user: req.user.userId }).sort({
         createdAt: -1,
       });
       res.json(items);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to fetch items" });
     }
   });

   // POST /api/items
   router.post("/", async (req, res) => {
     try {
       const { title, description, status, dueDate } = req.body;
       const item = await Item.create({
         title,
         description,
         status,
         dueDate,
         user: req.user.userId,
       });
       res.status(201).json(item);
     } catch (err) {
       console.error(err);
       if (err.name === "ValidationError") {
         return res.status(400).json({ error: err.message });
       }
       res.status(500).json({ error: "Failed to create item" });
     }
   });

   // GET /api/items/:id
   router.get("/:id", async (req, res) => {
     const { id } = req.params;
     try {
       const item = await Item.findOne({ _id: id, user: req.user.userId });
       if (!item) {
         return res.status(404).json({ error: "Item not found" });
       }
       res.json(item);
     } catch (err) {
       console.error(err);
       if (err.name === "CastError") {
         return res.status(400).json({ error: "Invalid ID format" });
       }
       res.status(500).json({ error: "Failed to fetch item" });
     }
   });

   // PUT /api/items/:id
   router.put("/:id", async (req, res) => {
     const { id } = req.params;
     const { title, description, status, dueDate } = req.body;
     const update = { title, description, status, dueDate };

     // Remove undefined fields
     Object.keys(update).forEach(
       (key) => update[key] === undefined && delete update[key]
     );

     if (Object.keys(update).length === 0) {
       return res.status(400).json({ error: "No valid fields to update" });
     }

     try {
       const item = await Item.findOneAndUpdate(
         { _id: id, user: req.user.userId },
         update,
         { new: true, runValidators: true }
       );
       if (!item) {
         return res.status(404).json({ error: "Item not found" });
       }
       res.json(item);
     } catch (err) {
       console.error(err);
       if (err.name === "ValidationError") {
         return res.status(400).json({ error: err.message });
       }
       if (err.name === "CastError") {
         return res.status(400).json({ error: "Invalid ID format" });
       }
       res.status(500).json({ error: "Failed to update item" });
     }
   });

   // DELETE /api/items/:id
   router.delete("/:id", async (req, res) => {
     const { id } = req.params;
     try {
       const deleted = await Item.findOneAndDelete({
         _id: id,
         user: req.user.userId,
       });
       if (!deleted) {
         return res.status(404).json({ error: "Item not found" });
       }
       res.json(deleted);
     } catch (err) {
       console.error(err);
       if (err.name === "CastError") {
         return res.status(400).json({ error: "Invalid ID format" });
       }
       res.status(500).json({ error: "Failed to delete item" });
     }
   });

   module.exports = router;
   ```

3. **Wire in `index.js`:**

   ```js
   const itemsRouter = require("./routes/items");
   app.use("/api/items", itemsRouter);
   ```

4. **Test all endpoints in Postman/Insomnia:**
   - With invalid/missing Authorization header → expect 401.
   - With JWT for user A vs user B → items must be separated.

### 3. Reflect (10–15 minutes)

- Which part felt easiest due to prior practice? Which part was trickiest?
- Did you correctly enforce ownership for all routes?

### 4. Stretch (optional, 20–30 minutes)

- Add basic **filtering** on GET `/api/items` using query params, e.g.:
  - `/api/items?status=done`
- Or: implement pagination: `?page=1&limit=10` using `skip` + `limit`.

---

## Day 4 – Domain-Specific Features (Statuses, Stats, Filters)

**Goals:**
- Implement 1–2 domain specific endpoints or behaviors:
  - E.g. stats, status transitions, date-based filters.
- Start making the backend reflect your unique project idea (not just generic CRUD).

### 1. Learn (20–30 minutes)

Think about your domain:

- Task Manager:
  - Stats: counts per status.
  - Filter by due date (overdue, due today).
- Habit Tracker:
  - Track completions, streak count endpoints.

In notes, brainstorm 2–3 “smart” endpoints:
- Example:
  - `GET /api/items/stats` – aggregated counts.
  - `GET /api/items/overdue` – items with past due date.

### 2. Do (60–90 minutes)

Pick 1–2 extra endpoints and implement.

Examples (for Task Manager):

1. **Stats endpoint `/api/items/stats`:**

   ```js
   router.get("/stats", async (req, res) => {
     try {
       const userId = req.user.userId;

       const total = await Item.countDocuments({ user: userId });
       const byStatus = await Item.aggregate([
         { $match: { user: new mongoose.Types.ObjectId(userId) } },
         { $group: { _id: "$status", count: { $sum: 1 } } },
       ]);

       const statusCounts = byStatus.reduce((acc, item) => {
         acc[item._id] = item.count;
         return acc;
       }, {});

       res.json({ total, statusCounts });
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to fetch stats" });
     }
   });
   ```

2. **Overdue endpoint `/api/items/overdue`:**

   ```js
   router.get("/overdue", async (req, res) => {
     try {
       const now = new Date();
       const items = await Item.find({
         user: req.user.userId,
         dueDate: { $lt: now },
         status: { $ne: "done" },
       }).sort({ dueDate: 1 });
       res.json(items);
     } catch (err) {
       console.error(err);
       res.status(500).json({ error: "Failed to fetch overdue items" });
     }
   });
   ```

3. **Test endpoints thoroughly**:
   - Create items with different statuses and due dates.
   - Confirm stats and overdue lists match expectations.

### 3. Reflect (10–15 minutes)

- How do these domain-specific endpoints make your app more useful than a generic todo list?
- Do you see other similar endpoints that could add value later?

### 4. Stretch (optional, 20–30 minutes)

- Implement a bulk update route (e.g., mark many items as done with one request).
- Or: add server-side search by keyword in `title`/`description` using `$regex`.

---

## Day 5 – Backend Error Handling & Security Pass

**Goals:**
- Make error responses consistent.
- Do a first-pass security/sanity review.
- Add any missing validation.

### 1. Learn (20–30 minutes)

Concepts:

- Error-handling middleware:
  - Centralize repeated error handling code.
- Security basics:
  - Don’t leak stack traces in production responses.
  - Never return password or passwordHash.
  - Validate input thoroughly.

In notes:
- Decide on a **standard error response shape**, e.g.:
  - `{ error: "message" }` or `{ error: { message, details } }`.

### 2. Do (60–90 minutes)

1. **Create global error handler (optional but helpful):**

   In `middleware/errorHandler.js`:

   ```js
   function errorHandler(err, req, res, next) {
     console.error(err);

     if (err.name === "ValidationError") {
       return res.status(400).json({ error: err.message });
     }

     if (err.name === "CastError") {
       return res.status(400).json({ error: "Invalid ID format" });
     }

     res.status(500).json({ error: "Something went wrong" });
   }

   module.exports = errorHandler;
   ```

   In `index.js`:

   ```js
   const errorHandler = require("./middleware/errorHandler");
   // ... after routes:
   app.use(errorHandler);
   ```

   Then in routes, you can `next(err)` instead of `res.status(...).json(...)` for many cases.

2. **Input validation review:**
   - `auth/register`:
     - Check email, password length, possibly format.
   - `auth/login`:
     - Check missing email/password.
   - `items` routes:
     - Ensure `title` is validated by Mongoose.
     - In POST/PUT, avoid accepting unknown fields unless you intentionally allow them.

3. **Security checklist:**
   - Confirm:
     - No route returns `passwordHash`.
     - Error messages don’t leak DB details.
     - All `items` routes use `auth` and filter by `user`.

4. **Re-test core flows in Postman:**
   - Successful register/login.
   - Unauthorized access without token.
   - CRUD for items.
   - Stats/overdue.

### 3. Reflect (10–15 minutes)

- Did you find any bugs or missing checks during this cleanup?
- How does having a consistent error format help frontend development?

### 4. Stretch (optional, 20–30 minutes)

- Add rate limiting to auth routes using a simple library like `express-rate-limit` (optional, but good security awareness).
- Add rudimentary logging for requests (method, path, status).

---

## Day 6 – Documentation & Example Usage

**Goals:**
- Document your API so you can integrate from React easily next week.
- Create examples of requests for each core endpoint.

### 1. Learn (20–30 minutes)

Concepts:

- API docs essentials:
  - Endpoint, method, URL.
  - Description.
  - Headers (auth).
  - Request body.
  - Response (status + example JSON).
- Tools:
  - Simple markdown docs are enough.
  - Optional: Postman collections.

In notes:
- Decide on where to keep docs:
  - `backend/README.md` or `docs/api.md`.

### 2. Do (60–90 minutes)

1. **Write API docs:**

   In e.g. `API.md`:

   For each core route, document:

   - `POST /api/auth/register`
     - Body: `{ "email": "string", "password": "string" }`
     - Responses: `201` (user created), `400`, `409`.
   - `POST /api/auth/login`
     - Body: ...
     - Response: `{ "token": "...", "user": { ... } }`
   - `GET /api/items` (auth required)
     - Headers: `Authorization: Bearer <token>`
     - Response: array of items.
   - etc.

2. **Optional: export Postman collection:**
   - Save all requests in Postman.
   - Export collection as JSON for future reference.

3. **Quick “API contract” check:**
   - Does your planned frontend know exactly:
     - What endpoints exist?
     - What they expect and return?

### 3. Reflect (10–15 minutes)

- How would someone unfamiliar with your code use your API just from the docs?
- Did writing docs reveal any inconsistencies you might want to fix in the code?

### 4. Stretch (optional, 20–30 minutes)

- Add example curl commands in docs, e.g.:

  ```bash
  curl -X GET http://localhost:3000/api/items \
    -H "Authorization: Bearer <token>"
  ```

- Consider adding a simple route `/api/version` that returns your app version and build date.

---

## Day 7 – Backend Review & Readiness for Frontend Integration

**Goals:**
- Perform an end-to-end review of your backend.
- Ensure it’s ready to be consumed by your React frontend in Week 12.
- Identify any missing pieces.

### 1. Review (30–45 minutes)

Walk through this mental checklist:

- **Setup:**
  - [ ] `.env` correctly configured.
  - [ ] `connectDB()` works (Mongo connected).
  - [ ] `npm run dev` starts server without errors.

- **Auth:**
  - [ ] `User` model defined.
  - [ ] Register/login routes work and hash passwords.
  - [ ] JWT is issued and verified by `authMiddleware`.
  - [ ] `/api/auth/me` (if you added it) returns current user.

- **Items:**
  - [ ] `Item` model matches your domain (Task/Habit/etc.).
  - [ ] CRUD routes implemented and require auth.
  - [ ] Ownership enforced (`user: req.user.userId`).
  - [ ] Any extra endpoints (stats, overdue, etc.) work.

- **Errors & Docs:**
  - [ ] Reasonable validation & error handling.
  - [ ] API docs exist and are up to date.

In notes:
- Jot down any TODOs you note during review.

### 2. Do – Final Small Fixes & Polish (60–90 minutes)

1. **Address any TODOs** from review.
2. **Run through core user journey with Postman:**
   - Register new user.
   - Login, store token.
   - Create item.
   - List items.
   - Update item.
   - Delete item.
   - Hit any stats/extra endpoints.

3. **Create a minimal “integration test” script (optional):**
   - Just a simple Node script that logs in and fetches items using `fetch` or `axios`, to confirm flows work programmatically.

### 3. Self-Assessment (20–30 minutes)

Mark ✅ / ❌:

- Backend completeness:
  - [ ] I have a full auth system with register/login + JWT.
  - [ ] I have CRUD routes for my main resource(s), protected and user-scoped.
  - [ ] I have at least one domain-specific endpoint (stats, filters, etc.).
  - [ ] I have a consistent error format and basic validation.

- Integration readiness:
  - [ ] I know all the endpoints my React app will need.
  - [ ] I have example requests (Postman or docs) for each.
  - [ ] I can easily explain to “future me” how to use this API.

Write 3 bullet points:
- 2 things you’re proud of in this backend.
- 1 area you want to improve later (e.g., testing, performance, advanced security).

### 4. Reflect (15–20 minutes)

In your notes:

- Describe the **full flow** your future frontend will follow when:
  1. User visits the app and logs in.
  2. User views and filters their items.
  3. User updates/completes items.
  4. User logs out.

- How does this backend compare (in complexity and robustness) to the simple todo API you built earlier?

### 5. Stretch (optional, 30–45 minutes)

- Start a **very small** piece of frontend integration early:
  - Spin up a fresh React app or reuse your learning app.
  - Create one simple page that logs in and fetches `/api/items`.
- Or:
  - Start sketching UI flows (wireframes) for Week 12 frontend work.

---

If you’d like next, I can:

- Create a **Week 12 plan** focused on wiring your React frontend to this backend (full CRUD, auth-based UI, deployment), or  
- Help you refactor or extend a specific part of your backend (e.g., multi-resource support, projects + tasks, etc.).
