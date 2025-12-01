Todo App

Simple, humble todo application built with the MERN stack and JWT authentication.

🔖 Project summary

This is a minimal Todo application that lets users create, read, update, delete, and mark tasks complete. The app uses React for the frontend, Node.js + Express for the backend, and MongoDB as the database. Authentication is handled with JWT and cookies.

Key highlights:

User signup & login (JWT stored/validated via cookies)

CRUD for todos (text, completed, timestamps)

Secure routes for authenticated users

Simple, responsive UI (React + Tailwind/CSS)

🧰 Tech stack

Frontend: React (Vite / Create React App)

Backend: Node.js, Express

Database: MongoDB (Atlas)

Auth: JSON Web Tokens (JWT) + HTTP-only cookies

HTTP client (dev): axios

Extras: react-hot-toast (notifications), dotenv, cookie-parser

✨ Features

Signup / Login / Logout (secure cookie + JWT)

Add, edit, delete todos

Toggle todo completion

Protected API routes (only owner can access their todos)

Defensive frontend to avoid render crashes

📁 Suggested repo structure
root/
├─ client/               # React app
│  ├─ src/
│  ├─ public/
│  └─ package.json
├─ server/               # Express API
│  ├─ controllers/
│  ├─ models/
│  ├─ routes/
│  ├─ middleware/        # auth, error handlers
│  └─ package.json
├─ .env.example
├─ README.md
└─ LICENSE
⚙️ Environment variables (.env)

Create a .env file in the server/ folder. Example:

PORT=8000
MONGODB_URI=mongodb+srv://<username>:<password>@cluster0.for6sxo.mongodb.net/to_app?retryWrites=true&w=majority
# NOTE: If your password contains '#', encode it as %23 (e.g. hariom123%23)
JWT_SECRET=your_jwt_secret_here
CLIENT_URL=http://localhost:3000
COOKIE_NAME=token
COOKIE_MAX_AGE=86400000
🚀 Run locally

Backend (server/):

cd server
npm install
npm run dev     # or node index.js

Frontend (client/):

cd client
npm install
npm run dev     # or npm start

Open http://localhost:3000 (or the port your client uses).

🔌 Important API endpoints (examples)

Base: http://localhost:8000

Auth

POST /user/signup — { name, email, password } → registers and sets cookie

POST /user/login — { email, password } → logs in and sets cookie

GET /user/logout — clears cookie

Todos (protected)

GET /todo/fetch — fetch user todos

POST /todo/create — { text, completed } → create todo

PUT /todo/update/:id — update text or completed status

DELETE /todo/delete/:id — delete a todo

Tip: Include withCredentials: true in axios when calling protected routes.

🛡️ Authentication & cookies (notes)

Use HTTP-only cookies to store the JWT so it's not accessible from JavaScript.

On the server, verify JWT on protected routes (middleware) and attach user id to req.user.

When testing locally with cookies, make sure your axios calls include { withCredentials: true } and your server sets proper CORS headers including credentials: true and origin set to your client URL.

✅ Frontend defensive tips (prevent blank/white screen)

Always check network response shape before replacing state.

Merge backend response with existing todo instead of blindly replacing to avoid missing keys (_id, completed).

Use safe render guards: todos.filter(Boolean).map(...).

🔧 Common troubleshooting

White page on update: Check browser console for crash stack and inspect PUT response body. Ensure returned object includes _id or update merging is used.

Auth cookie not set: Confirm server sets Set-Cookie with HttpOnly; SameSite=None; Secure (for HTTPS) and CORS allows credentials.

Password special characters: URL-encode reserved chars (# → %23) in MONGODB_URI.

🤝 Contribution

If you'd like to contribute:

Fork the repo

Create a feature branch

Open a pull request with a clear description

Tell me which one you want next and I’ll add it.
