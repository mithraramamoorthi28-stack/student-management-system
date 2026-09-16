🎓 Student Management System — Full-Stack CRUD Web Application

A complete Student Management System built with **Node.js, Express.js, and
MySQL**, with a responsive vanilla HTML/CSS/JavaScript frontend. Every
Create, Read, Update, Delete, and Search action goes through a real REST
API to a real MySQL database — nothing is stored in the browser.

```
Frontend (HTML/CSS/JS) → REST API (Express.js) → MySQL Database
```

---

## 📋 Project Description

This project lets a user manage student records (add, view, edit, delete,
search) through a clean web dashboard. It's a genuine full-stack
application: the frontend never touches the database directly — it only
calls REST endpoints exposed by an Express server, which performs
parameterized SQL queries against MySQL using the `mysql2` package.

---

## ✨ Features

- Add new students with full validation
- View all students in a responsive, searchable table
- View full details of a single student in a modal
- Edit any student's information
- Delete a student with a confirmation prompt
- Duplicate roll-number prevention (checked in the database and the backend)
- Backend-powered search (name or roll number)
- Success/error messages and inline field validation
- Loading and empty states
- Responsive layout for desktop and mobile
- One command runs the whole application (frontend is served by Express)

---

## 🛠️ Technologies Used

| Layer     | Technology                     |
|-----------|----------------------------------|
| Frontend  | HTML5, CSS3, Vanilla JavaScript (fetch API) |
| Backend   | Node.js, Express.js              |
| Database  | MySQL                             |
| DB Driver | mysql2 (parameterized queries)    |
| Config    | dotenv (.env environment variables) |
| API Style | REST (JSON)                       |

No React, MongoDB, Firebase, or PHP is used — kept intentionally simple.

---

## 📁 Project Structure

```
student-management-node/
├── frontend/
│   ├── index.html
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── script.js
│
├── backend/
│   ├── server.js
│   ├── db.js
│   ├── routes/
│   │   └── studentRoutes.js
│   ├── controllers/
│   │   └── studentController.js
│   ├── package.json
│   └── .env.example
│
├── database/
│   └── schema.sql
│
├── .gitignore
└── README.md
```

---

## 🗄️ Database Setup

1. Make sure MySQL is installed and running.
2. Run the schema file to create the database and table:
   ```bash
   mysql -u root -p < database/schema.sql
   ```
   This creates the `student_management` database, the `students` table,
   and inserts 3 sample rows so the table isn't empty on first load.

**Table structure:**

| Column       | Type          | Constraint             |
|--------------|---------------|---------------------------|
| id           | INT           | Primary Key, Auto Increment |
| name         | VARCHAR(100)  | NOT NULL                  |
| roll_number  | VARCHAR(30)   | UNIQUE, NOT NULL          |
| department   | VARCHAR(100)  | NOT NULL                  |
| email        | VARCHAR(100)  | NOT NULL                  |
| phone        | VARCHAR(10)   | NOT NULL                  |

---

## ⚙️ Backend Setup

### 1. Install dependencies
```bash
cd backend
npm install
```

### 2. Configure environment variables
Copy the example file and fill in your real MySQL credentials:
```bash
cp .env.example .env
```
Then edit `.env`:
```
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_mysql_password
DB_NAME=student_management
PORT=5000
```
`.env` is already listed in `.gitignore`, so your password is never
committed to GitHub.

### 3. Run the project
```bash
npm start
```
This starts Express on `http://localhost:5000` **and** serves the
frontend from the same server — open that URL in your browser and the
whole application (UI + API + database) is live.

(Optional, for development with auto-restart on file changes:
`npm run dev`, which uses `nodemon`.)

---

## 🔌 API Endpoints

| Method | Endpoint                        | Description                     |
|--------|-----------------------------------|-----------------------------------|
| GET    | `/api/students`                   | Get all students                  |
| GET    | `/api/students?search=term`       | Get students filtered by name/roll number |
| GET    | `/api/students/:id`               | Get a single student by ID        |
| POST   | `/api/students`                   | Create a new student               |
| PUT    | `/api/students/:id`               | Update an existing student        |
| DELETE | `/api/students/:id`               | Delete a student                    |

All requests/responses are JSON. Validation failures return `400`,
duplicate roll numbers return `409`, and a missing student returns `404`.

---

## 🔁 CRUD Explanation

- **Create:** Add Student form → `POST /api/students` → controller
  validates input, checks for duplicate roll number → `INSERT` into MySQL.
- **Read:** Page load / search box → `GET /api/students` (or with
  `?search=`) → `SELECT` from MySQL → rendered into the table.
- **View:** Clicking "View" → `GET /api/students/:id` → fresh `SELECT`
  for that one row → shown in a modal.
- **Update:** Clicking "Edit" pre-fills the form → submitting →
  `PUT /api/students/:id` → controller re-validates, re-checks roll number
  uniqueness → `UPDATE` in MySQL.
- **Delete:** Clicking "Delete" → confirmation dialog → `DELETE /api/students/:id`
  → row removed from MySQL → table refreshes.

---

## 📸 Screenshots

_Add screenshots here before submission:_
- Add Student form
- Student list table
- Edit in progress
- Delete confirmation
- MySQL table showing data

---

## 🔮 Future Improvements

- Pagination and sorting for large student lists
- Export records to CSV/PDF
- Optional authentication for staff/admin access
- Profile photo upload per student
- Attendance and grades modules
- Deployment to a live host (e.g. Render + PlanetScale/MySQL hosting)

---

## 👨‍💻 GitHub Setup

```bash
git init
git add .
git commit -m "Initial commit: Student Management System (Node.js, Express, MySQL)"
git branch -M main
git remote add origin https://github.com/<your-username>/student-management-node.git
git push -u origin main
```

`.gitignore` already excludes `node_modules/` and `.env`, so another
student can clone the repo, run `npm install`, copy `.env.example` to
`.env` with their own credentials, run `database/schema.sql`, and start
the app with `npm start`.

