# Student Records Management System

A full CRUD (Create, Read, Update, Delete) web application for managing student records.

**Stack:** Node.js + Express + MongoDB (Mongoose) + EJS

## Features
- View all students in a table, with search by name / Student ID / course
- Add a new student (with server-side validation)
- Edit an existing student's details
- Delete a student (with a confirmation prompt)
- Friendly success/error messages
- Clean, responsive UI

## 1. Install dependencies
Open this folder in VS Code, open a terminal (Terminal > New Terminal), and run:

```
npm install
```

This downloads Express, Mongoose, EJS, dotenv, and method-override into a `node_modules` folder.

## 2. Connect to your MongoDB Atlas database
1. Rename `.env.example` to `.env`
2. In MongoDB Atlas: Cluster > Connect > Drivers > copy your connection string
3. Paste it into `.env` as `MONGO_URI=...`, replacing `YOUR_USERNAME`, `YOUR_PASSWORD`, and `YOUR_CLUSTER` with your real values
4. Make sure in Atlas, under "Network Access", your IP address (or 0.0.0.0/0 for "allow from anywhere") is added — otherwise the connection will be refused

## 3. Run the app
```
npm start
```

You should see:
```
Connected to MongoDB Atlas
Server running at http://localhost:3000
```

Open your browser to **http://localhost:3000** — you'll be redirected to the student list.

## 4. Try out every CRUD operation (for your demo)
1. **Create**: click "+ Add Student", fill the form, submit — try leaving a required field blank first to show validation works
2. **Read**: see the table populate; try the search box with a name or course
3. **Update**: click "Edit" on a row, change a value, save, confirm it updates in the table
4. **Delete**: click "Delete" on a row — confirm the "Are you sure?" prompt appears, then confirm the record disappears

## Project structure
```
student-records/
├── app.js                  # Express app entry point, DB connection
├── models/
│   └── Student.js          # Mongoose schema + validation rules
├── routes/
│   └── students.js         # All CRUD routes
├── views/
│   ├── index.ejs           # List + search page
│   ├── new.ejs              # Add student form
│   ├── edit.ejs              # Edit student form
│   ├── error.ejs            # Error page
│   └── partials/
│       ├── header.ejs
│       └── footer.ejs
├── public/css/style.css    # Styling
├── .env.example             # Template for your DB connection string
└── package.json
```

## For your project report / presentation
- **Database design**: one collection (`students`) with a Mongoose schema enforcing required fields, email format, and year-of-study range (1-6) — this is the validation layer since MongoDB itself is schema-less
- **CRUD mapping**:
  - Create → `POST /students`
  - Read → `GET /students` (list + search)
  - Update → `GET /students/:id/edit` then `PUT /students/:id`
  - Delete → `DELETE /students/:id`
- **Security**: all queries go through Mongoose (no raw string-built queries), server-side validation runs on every create/update, delete requires a JS confirmation prompt
- **Error handling**: try/catch around every database call, with user-friendly messages instead of raw error dumps
