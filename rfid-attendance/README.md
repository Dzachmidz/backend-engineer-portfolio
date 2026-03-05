<div align="center">

# 📋 Al Wafa Attendance Information System

### _A production-grade, IoT-integrated automated attendance management system built with Django._

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Django](https://img.shields.io/badge/Django-4.x-092E20?style=for-the-badge&logo=django&logoColor=white)](https://djangoproject.com)
[![DRF](https://img.shields.io/badge/Django_REST_Framework-Latest-red?style=for-the-badge&logo=django&logoColor=white)](https://www.django-rest-framework.org)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com)
[![SQLite](https://img.shields.io/badge/SQLite-Database-003B57?style=for-the-badge&logo=sqlite&logoColor=white)](https://sqlite.org)
[![Status](https://img.shields.io/badge/Status-Production-success?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)]()

</div>

---

## 📌 Overview

**Al Wafa Attendance Information System** is an RFID-based attendance management system designed for a real educational environment. It replaces manual attendance recording with an automated digital solution using RFID cards directly integrated with a hardware scanner (IoT device).

The system is built on a **modular monolithic** architecture using Django, exposing a **REST API** for communication with RFID hardware, and providing a feature-rich **web-based admin panel** for managing student data, classes, schedules, and attendance reports.

> This system is actively deployed at the **Al Wafa** educational institution, managing real-time student attendance data every day.

---

## ✨ Features

- 🔐 **Admin Authentication** — Secure session-based login/logout; all admin pages protected by `@login_required`
- 📡 **RFID Hardware Integration** — Dedicated REST API endpoint for receiving UID scans from RFID devices (ESP32/Arduino)
- ⏱️ **Automatic Status Detection** — The system intelligently determines attendance status: **Present**, **Late**, or **Late Pickup** based on scan time
- 🔄 **Multi-Session per Class** — Each class can have multiple schedule sessions (Morning/Afternoon) with configurable check-in/check-out time tolerances
- 📊 **Real-Time Dashboard** — Displays total students, today's attendance count, absent count, and recent attendance activity
- 👤 **Complete Student Management** — Student CRUD, bulk import via Excel file, and individual data editing
- 🏫 **Class & Schedule Management** — Manage classes with check-in & check-out schedules per class, including special schedule sessions
- 🪪 **RFID Card Registration** — Register RFID card UIDs to student records, with card status checking (registered / available)
- ✍️ **Manual Attendance** — Admin entry of attendance outside of RFID for emergency situations
- 📜 **Attendance History** — Complete history table of all attendance data with filtering and pagination
- 📤 **Export to Excel** — Download attendance reports in `.xlsx` format using `openpyxl`
- ⚙️ **Global Time Settings** — Configure global system operating hours using a Singleton pattern

---

## 🛠️ Tech Stack

| Layer               | Technology                     | Purpose                                      |
| ------------------- | ------------------------------ | -------------------------------------------- |
| **Backend**         | Django 4.x (Python 3.x)        | Core logic, ORM, routing, template rendering |
| **REST API**        | Django REST Framework          | RFID hardware communication endpoint         |
| **Database**        | SQLite (dev) / MySQL (prod)    | Relational data storage                      |
| **Frontend**        | Bootstrap 5 + Django Templates | Responsive UI & server-side rendering        |
| **IoT Integration** | ESP32 / Arduino (RFID Reader)  | RFID card hardware scanner                   |
| **Export/Import**   | openpyxl                       | Generate & parse Excel files (.xlsx)         |
| **Authentication**  | Django Session Auth            | Admin panel security                         |
| **Tools**           | Git, Virtualenv, Postman       | Version control & development tooling        |

---

## 🏗️ Architecture

The system uses a **Django MTV (Model-Template-View)** architecture with two main application modules with clearly separated responsibilities:

```
┌────────────────────────────────────────────┐
│         Browser / Admin Client             │
└──────────────────┬─────────────────────────┘
                   │ HTTP Request
┌──────────────────▼─────────────────────────┐
│            Django URL Router               │
│    (absensi/urls.py → app-level urls)      │
└──────────┬───────────────────┬─────────────┘
           │                   │
┌──────────▼──────────┐  ┌─────▼─────────────┐
│  adminapp (Web UI)  │  │  userapp (REST API)│
│  - Dashboard        │  │  - /api/rfid-scan/ │
│  - Student/Class    │  │  - Serializers     │
│  - Attendance Log   │  │  - Attend. Logic   │
│  - RFID Register    │  └─────┬─────────────┘
│  - Manual Attend.   │        │ POST UID
└──────────┬──────────┘  ┌─────▼────────────┐
           │              │  RFID Hardware   │
┌──────────▼──────────────┤  (ESP32/Arduino) │
│      Data Models        └──────────────────┘
│  Student | Class | Attendance              │
│  ScheduleSession | RfidLog                 │
│  OperationalTime (Singleton)               │
└──────────┬─────────────────────────────────┘
           │ SQL / ORM
┌──────────▼─────────────────────────────────┐
│         Database (SQLite / MySQL)           │
└────────────────────────────────────────────┘
```

### Main Modules:

- **`userapp`** — Manages core data models (`Student`, `Class`, `Attendance`, `ScheduleSession`, `RfidLog`, `OperationalTime`), REST API for RFID hardware, and automated attendance logic.
- **`adminapp`** — Manages all web admin views: dashboard, data management, RFID registration, attendance history, and export/import features.

### Automated Attendance Mechanism:

1. RFID hardware sends `POST /api/rfid-scan/` with payload `{"uid": "XXXX"}`
2. The system looks up the `Student` by card UID
3. If found, the system determines the **attendance mode** (`check-in` / `check-out`) based on:
   - Whether an open `Attendance` record (checkout_time null) exists for today
   - Schedule time from the relevant class session
4. Attendance status is automatically calculated: `On Time` or `Late`
5. JSON response is sent back to the hardware (student name, mode, message)

---

## 🔄 System Workflow

### Check-In Flow

```
[Tap RFID Card]
      │
      ▼
[Hardware POST → /api/rfid-scan/]
      │
      ▼
[Look Up Student by RFID UID]
      │
      ├── Not Found → Log RfidLog (status: unknown) → Response Error
      │
      └── Found
              │
              ▼
      [Fetch Class Schedule / Active Session]
              │
              ▼
      [Calculate Status: On Time / Late]
              │
              ▼
      [Save Attendance record to Database]
              │
              ▼
      [Response: "Welcome, {Name}"]
```

### Check-Out Flow

```
[Tap RFID Card (2nd time)]
      │
      ▼
[System detects open attendance today (checkout_time = null)]
      │
      ▼
[Check current time >= scheduled checkout start]
      │
      ├── Not Yet Time → Response: "You already checked in at HH:MM"
      │
      └── Time Met
              │
              ▼
      [Update checkout_time on Attendance record]
              │
              ▼
      [Response: "Goodbye, {Name}"]
```

### Admin Panel Flow

```
1. Admin login → /login/ (session-based auth)
2. Dashboard → View today's present/absent summary
3. Manage Classes → Add/edit classes + configure schedule sessions
4. Manage Students → CRUD + bulk Excel import
5. RFID Registration → Register/check cards to students
6. Manual Attendance → Input attendance without RFID
7. Attendance History → Filter & export reports to Excel
```

---

## 📸 Screenshots

<div align="center">

|                                         |                                           |
| :-------------------------------------: | :---------------------------------------: |
|           **Admin Dashboard**           |             **Student Data**              |
| ![Dashboard](screenshots/dashboard.png) |  ![Students](screenshots/data_siswa.png)  |
|         **Attendance History**          |           **RFID Registration**           |
|   ![History](screenshots/riwayat.png)   | ![RFID](screenshots/registrasi_rfid.png)  |
|          **Class Management**           |           **Manual Attendance**           |
|  ![Class](screenshots/data_kelas.png)   | ![Manual](screenshots/absensi_manual.png) |

</div>

> _Placeholder — run the system to see the live interface._

---

## 🌍 Project Impact

- ✅ **Deployed at a real educational institution** — The system operates actively at **Al Wafa** to record student attendance every day
- ✅ **Eliminates manual attendance** — Replaces error-prone and manipulation-susceptible paper-based recording
- ✅ **IoT Integration** — Connects physical RFID hardware directly to a digital database via REST API
- ✅ **Administrative efficiency** — Admins can export attendance reports to Excel in seconds
- ✅ **Real-time detection** — Attendance status (on time/late) is automatically calculated without admin intervention
- ✅ **Data scalability** — Architecture supports adding new classes, schedule sessions, and students without downtime

---

## 🔒 Source Code

This is a production-grade system used in a real educational environment.

The full source code is hosted in a **private repository** to protect intellectual property.

However, I'm happy to provide access to:

- 👨‍💻 **Interviewers** — for code quality & architecture review
- 🤝 **Collaborators** — if you're interested in contributing

Please contact me for access.

[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)

---

## 📊 Project at a Glance

| Metric               | Value                                                                     |
| -------------------- | ------------------------------------------------------------------------- |
| **Backend Modules**  | 2 (`adminapp`, `userapp`)                                                 |
| **Database Models**  | 6 (Student, Class, Attendance, ScheduleSession, RfidLog, OperationalTime) |
| **API Endpoints**    | 1 REST + 9 Admin Routes                                                   |
| **Admin Features**   | Dashboard, Students, Classes, Sessions, RFID Reg, Manual, History         |
| **IoT Integration**  | RFID Card Reader (ESP32/Arduino over HTTP)                                |
| **Export Format**    | Excel (.xlsx) via openpyxl                                                |
| **Authentication**   | Django Session-based (Admin Panel)                                        |
| **Deployment Ready** | Gunicorn + Nginx (Linux Server)                                           |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- Git

### Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/yourusername/absensi-alwafa.git
   cd absensi-alwafa
   ```

2. **Create virtual environment**

   ```bash
   python -m venv .venv
   source .venv/bin/activate  # Windows: .venv\Scripts\activate
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Run migrations**

   ```bash
   python manage.py migrate
   ```

5. **Create superuser (Admin)**

   ```bash
   python manage.py createsuperuser
   ```

6. **Run development server**

   ```bash
   python manage.py runserver
   ```

   Visit `http://127.0.0.1:8000/login` to access the admin panel.

### RFID Hardware Integration

The system exposes a REST API endpoint for the RFID scanner device:

```
POST /api/rfid-scan/
Content-Type: application/json

{
  "uid": "A1B2C3D4"
}
```

Configure your ESP32/Arduino to send `POST` requests to this endpoint when a card is tapped.

---

## 🗺️ Roadmap

- [x] RFID-based automated check-in & check-out
- [x] Multi-session scheduling per class
- [x] Smart attendance status (On Time / Late)
- [x] Admin dashboard with real-time stats
- [x] Export attendance to Excel
- [x] Import students from Excel
- [x] RFID card registration & management
- [ ] WhatsApp/SMS notification to parents
- [ ] Monthly attendance report generation (PDF)
- [ ] Docker support for streamlined deployment
- [ ] Role-based access (Super Admin / Operator)
- [ ] Mobile-responsive PWA for admin panel

---

## 👤 Author

<div align="center">

**Achmad Fahmi Al Hafidz**
_Backend Engineer · Python · Django · IoT Systems_

[![GitHub](https://img.shields.io/badge/GitHub-fidzst-181717?style=for-the-badge&logo=github)](https://github.com/fidzst)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/your-profile)
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://your-portfolio.com)

</div>

---

<div align="center">

_Built with ❤️ using Django & Python — deployed in a real educational institution._

</div>
