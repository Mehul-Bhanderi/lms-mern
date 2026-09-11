# Learning Management System (MERN)

A full-stack course platform: instructors publish courses with video lectures, students subscribe through Razorpay, and admins track revenue and enrolment from a dashboard.

## Features

**Accounts and access** — Registration and login with JWT issued in an HTTP-only cookie, bcrypt-hashed passwords, password reset over email with a hashed, expiring token, and role-based route guards separating students from admins.

**Courses** — Admins create courses with a thumbnail, then add or remove lectures. Media uploads go to Cloudinary via multer, so video and image files never touch the app server's disk long-term. Students browse the catalogue and open a course description before subscribing.

**Payments** — Razorpay subscriptions with verification, cancellation, and a stored payment record per user. The admin dashboard aggregates subscription counts and revenue.

**Dashboard** — Chart.js visualisations of enrolment and revenue, plus lecture management for each course.

**Contact** — Contact form delivered by nodemailer over SMTP.

## Stack

**Backend** — Express, MongoDB with Mongoose, JWT, bcrypt, Cloudinary, multer, nodemailer, Razorpay, morgan, cookie-parser.

**Frontend** — React with Vite, Redux Toolkit, React Router, Tailwind CSS with DaisyUI, Chart.js via `react-chartjs-2`, `react-slick` carousel, `react-hot-toast`, axios.

## Layout

```
backend/
  server.js, app.js
  config/db.config.js
  models/           user, course, payment
  controllers/      user, course, payment, miscellaneous
  routes/           user, course, payment, miscellaneous
  middleware/       auth (JWT + roles), multer (uploads), error
  utils/            error.utils, sendEmail
client/
  src/Pages/        HomePage, Login, About, Contact, Denied
  src/Pages/Course/ CourseList, CourseDescription, CreateCourse
  src/Pages/Dashboard/ AdminDashboard, AddLecture, DisplayLecture
  src/Components/   Navbar, Sidebar, Footer, CourseCard, CarouselSlide, InputBox, auth/RequireAuth
  src/Helpers/      axiosInstance, regexMatcher
  src/Layout/       Layout
```

## Setup

Requires Node.js, a MongoDB instance, and accounts for Cloudinary, Razorpay and an SMTP provider.

**Backend**

```bash
cd backend
npm install
cp .env.example .env     # then fill in your values
npm start
```

**Frontend**

```bash
cd client
npm install
cp .env.example .env     # then set the API URL
npm run dev
```

The app runs at `http://localhost:5173`.

## Environment

The backend expects the keys listed in `backend/.env.example`, covering the Mongo connection, JWT secret and expiry, Cloudinary credentials, Razorpay key/secret/plan, and SMTP settings. The client needs only `VITE_REACT_APP_API_URL`, pointing at the backend's `/api` prefix.

Routes are mounted as `/api/user`, `/api/courses`, `/api/payments`, and `/api/` for miscellaneous endpoints.
