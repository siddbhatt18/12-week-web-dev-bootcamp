**Week 12 Theme:** Deployment, production setup, and final polish of your full‑stack app.  
Assume ~2 hours/day. You’ll:

- Deploy backend (Node/Express/Mongo)  
- Deploy frontend (React)  
- Wire them together with environment variables  
- Polish UX, docs, and treat it as a portfolio project

Use any hosting you prefer. I’ll assume:
- **Backend:** Render or Railway (Render example)
- **Frontend:** Netlify or Vercel (Netlify example)

---

## Day 1 – Deployment Overview & Repo Cleanup

**Objectives:**
- Understand the deployment pipeline.
- Make sure your repos are clean and ready to deploy.

### 1. Concept: how deployment fits together (20–30 min)

In `week12/notes-day1.txt`, jot down:

- Final architecture:
  - **Backend:** Public URL (e.g., `https://your-api.onrender.com`)
  - **Frontend:** Public URL (e.g., `https://your-app.netlify.app`)
  - **Database:** MongoDB Atlas (already hosted)
- Flow:
  - Browser → Frontend → Backend → MongoDB

Review:
- Backend repo structure: `index.js`, `models/`, `routes/`, `middleware/`, `.env.example`
- Frontend repo structure: `src/`, `api.js`, `AuthContext`, etc.

### 2. Clean up your repos (45–60 min)

Backend:
- Ensure:
  - `package.json` has a `"start"` script:
    ```json
    "scripts": {
      "start": "node index.js"
    }
    ```
  - `engines` (optional) to specify Node version:
    ```json
    "engines": {
      "node": ">=18"
    }
    ```
- Add `.env.example` (no secrets) with placeholders:
  ```env
  MONGODB_URI=your-mongodb-connection-string
  PORT=4000
  JWT_SECRET=your-jwt-secret
  JWT_EXPIRES_IN=7d
  ```
- Confirm `.gitignore` includes `.env` and `node_modules`.

Frontend:
- Confirm:
  - `package.json` has `"build"` script (Vite creates this by default).
  - `vite.config.js` exists and is standard.

### 3. Final local test (20–30 min)

- Run backend: `npm start`
- Run frontend: `npm run dev`
- Do a quick end‑to‑end: login, create notes, edit/delete, view stats.

Fix any obvious errors before deployment.

---

## Day 2 – Deploy Backend to Render (or Similar)

**Objectives:**
- Deploy your Node/Express API.
- Point it at your existing MongoDB Atlas.

### 1. Prepare for Render (15–20 min)

Create a GitHub repo (if you haven’t):
- Push your backend code (`notes-api`) to GitHub.

Make sure your code:
- Uses `process.env.PORT` (already done in Week 7/10).
- Contains no hardcoded connection strings or secrets.

### 2. Deploy on Render (60–70 min)

1. Go to https://render.com → create account.
2. “New +” → **Web Service**
   - Connect your GitHub.
   - Select your backend repo.
3. Settings:
   - Name: `notes-api` (or similar)
   - Runtime: Node
   - Build Command: `npm install`
   - Start Command: `npm start`
4. Environment variables (Render dashboard → Environment):
   - `MONGODB_URI` → your Atlas connection string
   - `JWT_SECRET` → your secret
   - `JWT_EXPIRES_IN` → `7d` (or whatever you used)
   - `PORT` → `4000` (Render may ignore it and use its own, but fine to set)

Deploy and wait.

When deployed:
- Note your backend URL, e.g.:  
  `https://notes-api.onrender.com`

Test with browser/Postman:
- `GET https://notes-api.onrender.com/` → should get your root message.
- `POST /auth/register` and `/auth/login` (with correct JSON).
- `GET /notes` with `Authorization: Bearer <token>`.

### 3. Reflection (5–10 min)

In `notes-day2.txt`:
- What environment variables did you configure on Render?
- What is your deployed API base URL?

---

## Day 3 – Configure Frontend for Production API & Build

**Objectives:**
- Wire your React app to use the deployed backend URL via env vars.
- Confirm the production build works locally.

### 1. Use environment variables in Vite (30–40 min)

In your React app:

1. Create `.env` files:
   - `.env.development`:
     ```env
     VITE_API_BASE_URL=http://localhost:4000
     ```
   - `.env.production`:
     ```env
     VITE_API_BASE_URL=https://notes-api.onrender.com
     ```
   (Replace with your backend URL.)

2. Update `api.js` to use env var:

   ```js
   const API_BASE_URL = import.meta.env.VITE_API_BASE_URL || "http://localhost:4000";
   ```

3. Restart dev server (`npm run dev`) to ensure it picks up `.env.development`.

### 2. Test dev & build (30–40 min)

- Run dev:
  - Verify that using `http://localhost:4000` still works locally.
- Build production:
  ```bash
  npm run build
  ```
  - Check that the build succeeds.
- Preview build (optional, Vite):
  ```bash
  npm run preview
  ```
  - Confirm app works against production API (`VITE_API_BASE_URL` in production preview if configured).

### 3. Reflection (5–10 min)

In `notes-day3.txt`:
- How does your frontend know which backend URL to use (dev vs prod)?
- Where in code do you reference `VITE_API_BASE_URL`?

---

## Day 4 – Deploy Frontend (Netlify or Vercel)

**Objectives:**
- Deploy your React app.
- Connect it to the production API.

### 1. Push frontend to GitHub (15–20 min)

If not already:
- Create a GitHub repo for your React app.
- `git init`, `git add .`, `git commit`, `git remote add origin ...`, `git push`.

### 2. Deploy on Netlify (45–60 min)

1. Go to https://netlify.com → Sign up / log in.
2. “Add new site” → “Import an existing project” → choose your React repo.
3. Build settings:
   - Build command: `npm run build`
   - Publish directory: `dist`
4. Environment variables (Netlify site settings → Build & Deploy → Environment):
   - Add `VITE_API_BASE_URL` with your production API URL:
     `https://notes-api.onrender.com`
5. Trigger a deploy.

After deployment:
- Netlify gives you a URL: `https://your-app-name.netlify.app`.
- Open it in browser:
  - Try logging in (same user as before).
  - Create and manage notes.
  - Confirm network tab shows calls to your `notes-api` URL.

### 3. Fix any CORS issues (10–20 min)

If calls fail with CORS errors:
- Ensure backend `index.js` has:

  ```js
  const cors = require("cors");

  app.use(
    cors({
      origin: ["http://localhost:5173", "https://your-app-name.netlify.app"],
      credentials: false,
    })
  );
  ```

- Redeploy backend, then refresh frontend and retest.

### 4. Reflection (5–10 min)

In `notes-day4.txt`:
- What’s your frontend live URL?
- Did you need to update CORS to include the Netlify URL?

---

## Day 5 – Production Testing & UX Polish

**Objectives:**
- Test the entire app in production.
- Fix small UX issues and rough edges.

### 1. Production test checklist (30–40 min)

From a normal browser (ideally incognito):

1. Visit your frontend URL.
2. Register a new user (if you made a register UI; if not, use Postman once, then login in the app).
3. Log in:
   - Confirm token storage works (reload page → remain logged in if you implemented that).
4. Notes usage:
   - Create, edit (if implemented), delete notes.
   - Use search/filter; verify behavior.
   - Check stats panel.
5. Log out → ensure protected routes redirect or show login prompt.
6. Try invalid actions:
   - Access `/` while logged out → redirected?
   - Use weird URLs → 404 page or some feedback.

Note issues in `week12/issues-production.md`.

### 2. UX Polish (40–50 min)

Tackle 1–3 small improvements such as:

- Better empty states:
  - “You have no notes yet. Create your first note above.”
- Clearer navigation:
  - Distinguish active nav link (e.g., with bold/underline).
- Consistent button labels:
  - “Add Note” vs “Create” vs “Submit” → pick one convention.
- Mobile view:
  - Check on small screen (DevTools device mode).
  - Ensure layout doesn’t break; adjust CSS as needed.

### 3. Reflection (5–10 min)

In `notes-day5.txt`:
- What felt different testing in production vs locally?
- What UX changes made the biggest difference?

---

## Day 6 – Documentation, Screenshots & Portfolio Angle

**Objectives:**
- Write a clear, concise README.
- Capture screenshots / short demo notes.
- Frame this as a portfolio project.

### 1. README for backend & frontend (45–60 min)

Backend `README.md` should include:
- **Project name:** e.g., “Notes API (Node/Express/Mongo)”
- **Description:** Short overview of what it does.
- **Tech stack:** Node, Express, MongoDB, Mongoose, JWT.
- **Features:**
  - Auth (register/login with JWT)
  - User-specific notes CRUD
  - Filters, pinned, etc. (if implemented)
- **API docs:** Summarize key endpoints (you already wrote details in Week 7; link or copy).
- **Local setup:**
  - Clone, `npm install`.
  - `.env` variables needed.
  - `npm start`.

Frontend `README.md`:
- **Name:** e.g., “Notes App – React Frontend”
- **Description:** Single-page app to manage notes with authentication.
- **Tech:** React, Vite, React Router, Context.
- **Features:**
  - JWT login, logout.
  - Create/edit/delete notes.
  - Search/filter, stats, responsive UI.
- **Live demo URL** (Netlify/Vercel).
- **API URL** (the backend).
- **Local setup:** `npm install`, `.env`, `npm run dev`.

### 2. Screenshots & short “story” (25–30 min)

- Take 2–4 screenshots:
  - Login page.
  - Notes dashboard with notes.
  - Any special screen (stats/filter).
- Save them in a `/screenshots` folder in frontend repo.
- In README, embed them (optional) or at least mention.

In `week12/portfolio-notes.md`, write:
- A short “project story” (2–3 paragraphs):
  - Why you built it.
  - What you learned (auth, full-stack, deployment).
  - How someone might extend it (teams, sharing, reminders, etc.).

### 3. Reflection (5–10 min)

In `notes-day6.txt`:
- Summarize your app in 3–4 sentences as if telling a recruiter.
- Note 1–2 things you’re proud of technically.

---

## Day 7 – Final Review, Retrospective & Next Steps

**Objectives:**
- Do a final pass on everything.
- Reflect on the 12‑week journey.
- Plan concrete next steps.

### 1. Final walkthrough (20–30 min)

- Open backend repo on GitHub:
  - Skim files, README, commit history.
- Open frontend repo on GitHub:
  - Skim components, hooks, README, screenshots.
- Visit your live app once more, in an incognito/private window:
  - Register/login, create few notes, test quickly.

Fix any last tiny issues if needed.

### 2. 12‑week retrospective (30–40 min)

In `week12/retrospective.md`, reflect on:

1. **Skills gained:**
   - HTML/CSS, JS fundamentals, DOM & localStorage.
   - Async JS and APIs (`fetch`, `async/await`).
   - Node/Express, REST, MongoDB/Mongoose.
   - React (components, state, hooks, routing).
   - Auth with JWT (backend) + auth flow (frontend).
   - Deployment and environment configuration.

2. **What you can build now:**
   - Static sites from scratch.
   - Interactive frontend apps.
   - REST APIs with persistent data.
   - Full-stack apps with login, protected data, basic analytics.

3. **What still feels weak:**
   - E.g., testing (Jest), advanced React patterns, TypeScript, performance.

4. **Next 4–8 weeks plan:**
   - Ideas:
     - Add automated tests (backend & frontend).
     - Add more features (tags, sharing, pagination).
     - Learn TypeScript and migrate parts of the app.
     - Build a different full-stack project (e.g., habit tracker, expense tracker).

### 3. Shareable summary (15–20 min)

In `week12/shareable-summary.txt`, write a concise blurb you might use on:
- LinkedIn
- CV
- Portfolio site

Example template:
> Over 12 weeks I built a full‑stack notes application using React, Node.js, Express, and MongoDB. It supports user registration and login with JWT, user-specific notes CRUD, search/filtering, basic analytics, and a responsive UI. I deployed the backend to Render and the frontend to Netlify, configured environment variables for production, and documented the API and architecture.

Adjust to your voice and stack.

---

You now have:

- A deployed full‑stack app with auth, CRUD, filters, and basic analytics.
- Experience with the full lifecycle: design → build → deploy → document.
- A concrete, demonstrable project for your portfolio.

If you want to continue, I can suggest a follow‑up study path (testing, TypeScript, another project, or deepening in React/Node).
