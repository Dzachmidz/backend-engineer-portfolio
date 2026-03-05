<div align="center">

# 🎓 TechAcademy — Course Booking API Platform

### _A production-grade backend API service for online course browsing, registration, and class booking._

[![Node.js](https://img.shields.io/badge/Node.js-18.x-339933?style=for-the-badge&logo=node.js&logoColor=white)](https://nodejs.org)
[![Express](https://img.shields.io/badge/Express.js-4.18-000000?style=for-the-badge&logo=express&logoColor=white)](https://expressjs.com)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://postgresql.org)
[![Prisma](https://img.shields.io/badge/Prisma-5.x-2D3748?style=for-the-badge&logo=prisma&logoColor=white)](https://prisma.io)
[![JWT](https://img.shields.io/badge/Auth-JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white)](https://jwt.io)
[![Vercel](https://img.shields.io/badge/Deployed-Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://vercel.com)
[![Status](https://img.shields.io/badge/Status-Production_Ready-success?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)]()

</div>

---

## 📌 Overview

**TechAcademy** is a backend API service that powers a full online learning and course booking platform. It allows users to browse available courses, create and manage accounts, and enroll in or book classes — all through a clean, versioned RESTful API.

The system handles the full lifecycle of a learner: from registration and authentication, through course discovery and enrollment, to payment processing, progress tracking, and course completion.

Core backend capabilities include:

- ✅ **Authentication & Authorization** — JWT-based stateless sessions with OTP email verification and Google OAuth2
- ✅ **Course Management** — hierarchical course catalog (Class → Chapter → Lesson) with filtering and search
- ✅ **Booking Workflow** — transaction-based class enrollment with multi-bank payment support and admin approval
- ✅ **Role-Based Access Control** — strict separation between learner and admin API surfaces
- ✅ **RESTful API Design** — versioned endpoints under `/api/v1`, consistent JSON response structure

---

## ✨ Features

- 🔐 **User Authentication with JWT** — secure login and registration with hashed passwords (bcrypt) and stateless JWT session tokens
- 📧 **OTP Email Verification** — automated 6-digit OTP sent via SMTP on registration and password reset
- 🔑 **Google OAuth2 SSO** — social login integration using the `googleapis` library
- 🏫 **Course Catalog API** — browse, filter, and retrieve courses by category, level, price, and rating
- 📅 **Class Booking System** — enroll in free courses immediately or initiate a payment flow for paid courses
- 📈 **Learning Progress Tracking** — per-lesson progress with percentage calculation and completion state
- 📖 **User Booking History** — retrieve all past and active enrollments with status and progress data
- ⭐ **Course Rating System** — submit ratings that auto-update the course average score
- 🔔 **In-App Notifications** — per-user notification records for payment updates and system events
- 🛡️ **Role-Based Access Control** — `restrict` (user) and `isAdmin` middleware guards on all sensitive routes
- 📊 **Admin Dashboard API** — manage users, approve payments, and oversee platform content
- 🐛 **Error Monitoring** — Sentry integration for real-time exception tracking across all API routes

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Backend** | Node.js 18 + Express.js 4.18 | RESTful API server, routing, middleware pipeline |
| **Database** | PostgreSQL 15 | Relational data persistence with foreign key constraints |
| **ORM** | Prisma 5 | Type-safe queries, migrations, connection pooling |
| **Authentication** | JWT + bcrypt | Stateless auth tokens, secure password hashing |
| **OAuth2** | Google APIs (`googleapis`) | Social login (Google SSO) |
| **Email** | Nodemailer + EJS | Transactional email — OTP, activation, password reset |
| **Media Storage** | ImageKit CDN + Multer | Profile and thumbnail uploads with CDN delivery |
| **Validation** | Joi | Request body schema validation |
| **Error Monitoring** | Sentry | Exception tracking and performance tracing |
| **API Style** | REST API | Versioned endpoints under `/api/v1` |
| **Infrastructure** | Vercel | Serverless deployment, zero-config CI/CD |
| **Dev Tools** | Nodemon, dotenv, Morgan, Postman | Hot-reload, env management, HTTP logging, API testing |

---

## 🏗️ API Architecture

TechAcademy uses a **modular RESTful MVC architecture** — each domain (auth, courses, bookings, users) is a self-contained module with its own route file, controller, and middleware chain.

```
┌──────────────────────────────────────┐
│         Client (React / Postman)     │
└──────────────────┬───────────────────┘
                   │ HTTPS — JSON
┌──────────────────▼───────────────────┐
│          Express.js API Server       │
│          /api/v1/{resource}          │
│                                      │
│  ┌─────────────────────────────┐     │
│  │       Route Modules (14)    │     │
│  │  /auth  /class  /payment    │     │
│  │  /user  /lesson /learning   │     │
│  │  /chapter /rating /notif …  │     │
│  └──────────────┬──────────────┘     │
│                 │                    │
│  ┌──────────────▼──────────────┐     │
│  │      Middleware Stack       │     │
│  │  restrict │ isAdmin │ Joi   │     │
│  │  error    │ notfound        │     │
│  └──────────────┬──────────────┘     │
│                 │                    │
│  ┌──────────────▼──────────────┐     │
│  │       Controllers           │     │
│  │   Business logic per domain │     │
│  └──────────────┬──────────────┘     │
│                 │                    │
│  ┌──────────────▼──────────────┐     │
│  │       Prisma ORM Client     │     │
│  │   Type-safe DB queries      │     │
│  └──────────────┬──────────────┘     │
└─────────────────┼────────────────────┘
                  │ SQL
┌─────────────────▼────────────────────┐
│         PostgreSQL Database          │
│   12 relational tables               │
│   Users │ Class │ Chapters │ Lessons │
│   Transactions │ Learning │ Rating … │
└──────────────────────────────────────┘
```

**Key design decisions:**
- **Modular routes** — each resource has its own route file, imported and mounted in `index.routes.js`
- **Controller-per-domain pattern** — business logic isolated per module (`auth.controllers.js`, `payment.controllers.js`, etc.)
- **Middleware guards** — `restrict` validates JWT tokens; `isAdmin` enforces admin-only access
- **Prisma schema-first** — all tables, relations, and constraints defined in `schema.prisma`, applied via migrations
- **Dual database URLs** — pooled connection for app queries, direct connection for migrations

---

## 📡 Example API Endpoints

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/v1/auth/register` | Register new user account |
| `POST` | `/api/v1/auth/login` | User login, returns JWT token |
| `POST` | `/api/v1/auth/login-admin` | Admin login |
| `POST` | `/api/v1/auth/verify-otp` | Verify OTP to activate account |
| `POST` | `/api/v1/auth/forgot-password` | Request password reset OTP |
| `POST` | `/api/v1/auth/reset-password` | Set new password with OTP |

### Courses

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/v1/class` | Get all courses (filterable) |
| `GET` | `/api/v1/class/:classCode` | Get course detail |
| `POST` | `/api/v1/class` | Create a new course (Admin) |
| `PUT` | `/api/v1/class/:classCode` | Update course (Admin) |
| `DELETE` | `/api/v1/class/:classCode` | Delete course (Admin) |
| `GET` | `/api/v1/category` | List all categories |

### Booking & Payments

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/v1/payment` | Book a class / create transaction |
| `GET` | `/api/v1/payment` | Get user booking history |
| `GET` | `/api/v1/admin/payment` | List all transactions (Admin) |
| `PUT` | `/api/v1/admin/payment/:id` | Approve or reject payment (Admin) |

### Learning Progress

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/v1/learning` | Get enrolled courses and progress |
| `PUT` | `/api/v1/learning` | Mark lesson viewed, update progress % |
| `POST` | `/api/v1/rating` | Submit course rating |

---

## 📝 Example Request & Response

### POST `/api/v1/auth/login`

**Request**
```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Response**
```json
{
  "status": true,
  "message": "OK",
  "err": null,
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "user": {
      "id": 1,
      "fullName": "John Doe",
      "email": "user@example.com",
      "isActivated": true
    }
  }
}
```

### POST `/api/v1/auth/register`

**Request**
```json
{
  "fullName": "Jane Doe",
  "email": "jane@example.com",
  "noTelp": "081234567890",
  "password": "securepassword"
}
```

**Response**
```json
{
  "status": true,
  "message": "Created",
  "err": null,
  "data": {
    "fullName": "Jane Doe",
    "email": "jane@example.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

---

## 📸 Screenshots

<div align="center">

| | |
|:---:|:---:|
| **Postman — Auth Endpoints** | **Postman — Course Catalog** |
| ![Auth](screenshots/postman-auth.png) | ![Courses](screenshots/postman-courses.png) |
| **API Response — Login** | **API Response — Booking** |
| ![Login Response](screenshots/response-login.png) | ![Booking Response](screenshots/response-booking.png) |

</div>

> _Contact for a live API demo or Postman collection export._

---

## 🚀 Project Impact

- 🔐 **Enterprise-grade authentication** — multi-method auth (Email+OTP, Google OAuth2) with secure password hashing and stateless JWT sessions
- 📦 **Scalable course architecture** — hierarchical Class → Chapter → Lesson data model supports large catalogs with full relational integrity
- 💳 **Full booking workflow** — end-to-end transaction flow from enrollment request through admin approval to active learning access
- 📈 **Real progress tracking** — per-lesson tracking with automatic percentage recalculation demonstrates complex business logic
- ☁️ **Cloud-native stack** — Vercel + PostgreSQL + ImageKit CDN is fully production-deployable with zero infrastructure overhead
- 📧 **Automated communication** — OTP delivery, account activation, and password reset via dynamic EJS email templates

---

## 📊 Project at a Glance

| Metric | Value |
|---|---|
| **Route Modules** | 14 |
| **API Endpoints** | 60+ |
| **Database Tables** | 12 |
| **Auth Methods** | 3 (Email+OTP, Google OAuth2, Admin) |
| **Middleware Layers** | 6 |
| **External Integrations** | 3 (ImageKit, Nodemailer, Sentry) |
| **Deployment Platform** | Vercel |
| **API Style** | REST — versioned under `/api/v1` |

---

## 🗺️ Future Improvements

- [ ] **Payment gateway** — Midtrans or Xendit integration for automated payment verification
- [ ] **Real-time notifications** — Socket.io WebSocket push events replacing polling
- [ ] **Video streaming** — Mux or Cloudflare Stream for adaptive-bitrate lesson delivery
- [ ] **Certificate generation** — auto-generate PDF certificates on course completion
- [ ] **Full-text course search** — PostgreSQL FTS or Elasticsearch for course discovery
- [ ] **Rate limiting** — Redis-backed throttling per IP and per JWT to prevent abuse
- [ ] **Automated tests** — Jest + Supertest coverage for all API endpoints
- [ ] **Docker setup** — Docker Compose for consistent local development environments
- [ ] **Refresh token rotation** — improve session security with short-lived access tokens
- [ ] **Instructor analytics** — enrollment trends, revenue reports, and completion rate dashboards

---

## 🔒 Source Code

This is a production-style backend API system.

The full source code is hosted in a **private repository** to protect intellectual property.

However, I'm happy to provide access to:

- 👨‍💻 **Interviewers** — for code review
- 🤝 **Collaborators** — for contributions

Please contact me for access.

[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)

---

## 👤 Author

<div align="center">

| | |
|---|---|
| **GitHub** | [![GitHub](https://img.shields.io/badge/GitHub-Profile-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/yourusername) |
| **LinkedIn** | [![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/yourprofile) |
| **Email** | [![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com) |
| **Portfolio** | [![Portfolio](https://img.shields.io/badge/Portfolio-Visit-FF5722?style=for-the-badge&logo=google-chrome&logoColor=white)](https://yourportfolio.com) |

</div>

---

<div align="center">

_Built with passion for clean backend engineering. Open to opportunities and collaborations._

[![Stars](https://img.shields.io/github/stars/yourusername/techacademy?style=social)](https://github.com/yourusername/techacademy)

</div>
