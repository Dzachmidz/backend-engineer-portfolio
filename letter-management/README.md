<div align="center">

# 📤 Letter Management Information System

### _A production-grade correspondence management system built for real-world organizational operations._

[![PHP](https://img.shields.io/badge/PHP-7.x-777BB4?style=for-the-badge&logo=php&logoColor=white)](https://php.net)
[![CodeIgniter](https://img.shields.io/badge/CodeIgniter-3.x-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)](https://codeigniter.com)
[![MySQL](https://img.shields.io/badge/MySQL-MariaDB-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-3/4-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com)
[![Status](https://img.shields.io/badge/Status-Production-success?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)]()

</div>

---

## 🔒 Source Code

This is a real-world production project used in massive regional events.  
The source code is kept in a **private repository** to protect intellectual property.

However, I’m happy to provide access to:

- 👨‍💻 **Interviewers** – to review code quality and architecture
- 🤝 **Collaborators** – if you're interested in contributing

[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)

---

## 📌 Overview

> **Letter Management Information System** is a full-featured, production-ready **Correspondence Management System (CMS)** designed for Indonesian government and organizational environments.

This system solves the inefficiency of manual letter management by digitalizing the entire correspondence lifecycle — from incoming and outgoing letters to internal office memos and bulk correspondence. It was designed and deployed for use in real organizational workflows, replacing paper-based processes with a centralized, trackable, and auditable digital system.

Built on **CodeIgniter 3** with a clean MVC architecture, it features session-based authentication, role-based access control, automated letter numbering, file attachments, and a comprehensive reporting suite.

---

## ✨ Features

- 🔐 **Session-Based Authentication** — Secure login/logout with MD5-hashed passwords, brute-force flash messaging, and email-based password reset
- 📥 **Incoming Mail (Surat Masuk)** — Record, track, and archive all incoming correspondence with full CRUD and detail views
- 📤 **Outgoing Mail (Surat Keluar)** — Manage and generate outgoing letters with auto-incremented letter numbers
- 📋 **Office Memo (Nota Dinas)** — Create and manage internal service notes with automated nota number generation
- 📦 **Bulk Incoming Mail (Surat Masuk Massal)** — Handle and categorize mass/bulk incoming correspondence as a separate workflow
- 🗂️ **Kode Arsip Classification** — Standard government archive classification codes (e.g., `000/001/NND/2024`) for systematic document filing
- 🔢 **Auto-Numbering Engine** — Dynamic letter number generation via AJAX based on recipient unit, archive code, and year
- 📎 **File Attachment Support** — Upload and manage supporting documents linked to correspondence records
- 📊 **Reporting & Print Module** — Generate and print filtered correspondence reports (by date range, unit, letter type)
- 👥 **User Management** — Admin-controlled user accounts with profile management and last-login tracking
- 🏢 **Departmental Structure** — Manage organizational units (departments) and their relationships
- 📧 **Email Notification System** — SMTP-based email for account verification and password reset via Gmail

---

## 🛠️ Tech Stack

| Layer              | Technology                    | Purpose                                          |
| ------------------ | ----------------------------- | ------------------------------------------------ |
| **Backend**        | PHP 7.x + CodeIgniter 3       | MVC core logic, ORM-style Active Record, routing |
| **Database**       | MySQL / MariaDB               | Relational data persistence                      |
| **Frontend**       | Bootstrap + jQuery            | Responsive UI, AJAX interactions                 |
| **Authentication** | PHP Session + MD5             | User session management and credential handling  |
| **Email**          | PHPMailer / CI Email via SMTP | Account verification & password reset            |
| **Storage**        | Local filesystem              | File attachment handling                         |
| **Infrastructure** | Apache / Nginx + Linux        | Web server deployment                            |
| **Dev Tools**      | Git, phpMyAdmin               | Version control & database management            |

---

## 🏗️ Architecture

The project follows the standard **CodeIgniter MVC (Model–View–Controller)** architecture with a clean separation of concerns:

```
┌────────────────────────┐
│    Browser / Client    │
└───────────┬────────────┘
            │ HTTP Request
┌───────────▼────────────┐
│   CodeIgniter Router   │  Routes URIs to Controllers
└───────────┬────────────┘
            │
┌───────────▼────────────┐
│      Controllers       │  Web.php / Users.php / SuratController.php
│  (Auth, Surat, Admin)  │
└──────┬──────────┬──────┘
       │ Query    │ Load
┌──────▼──────┐  ┌▼─────────────────┐
│   Mcrud     │  │     Views         │
│   (Model)   │  │  (HTML Templates) │
└──────┬──────┘  └──────────────────┘
       │ SQL
┌──────▼──────────────────┐
│  MySQL / MariaDB         │
│  (db_surat)              │
└──────────────────────────┘
```

### Key Modules

| Module             | Controller            | Responsibility                                      |
| ------------------ | --------------------- | --------------------------------------------------- |
| **Authentication** | `Web.php`             | Login, logout, password reset via email token       |
| **Correspondence** | `SuratController.php` | SM, SK, Nota Dinas, Nota Dinas CRUD, auto-numbering |
| **Administration** | `Users.php`           | Dashboard, user management, settings, reports       |
| **Data Layer**     | `Mcrud.php`           | Centralized Active Record model for all tables      |

### Database Structure

The system manages **12+ relational tables** including:

| Table                     | Description                                             |
| ------------------------- | ------------------------------------------------------- |
| `tbl_user`                | User accounts, credentials, profiles, and login history |
| `tbl_sm`                  | Incoming Mail (Surat Masuk) records                     |
| `tbl_sk`                  | Outgoing Mail (Surat Keluar) records                    |
| `tbl_ns`                  | Office Memo (Nota Dinas) / internal memorandums         |
| `tbl_surmas`              | Bulk Incoming Mail (Surat Masuk Massal) records         |
| `tbl_memo`                | Internal memo records                                   |
| `tbl_bagian`              | Organizational department/division data                 |
| `kode_arsip`              | Standard government archive classification codes        |
| `unit_kerja`              | Work unit / organizational unit registry                |
| `nota_dinas`              | Extended office memo with stored procedure support      |
| `kab_kota`                | Regional reference data (District/City)                 |
| `kecamatan` / `kelurahan` | Sub-district and village reference data                 |

---

## 🔄 System Workflow

```
1. AUTHENTICATION
   └─ User logs in → Session created → Redirected to dashboard

2. CORRESPONDENCE INTAKE (Surat Masuk)
   └─ Select sender/recipient unit → Auto-generate letter number via AJAX
   └─ Fill in date, archive code, classification, subject
   └─ Save to `tbl_sm` → Confirmation flash message

3. CORRESPONDENCE DISPATCH (Surat Keluar)
   └─ Select recipient unit → Auto-generate outgoing letter number
   └─ Input subject, classification code, dispatch properties
   └─ Save to `tbl_sk`

4. INTERNAL MEMO (Nota Dinas)
   └─ Create nota with numbered format: KODE/NNN/UNIT/YEAR
   └─ Attach supporting documents (lampiran)
   └─ Track via `tbl_ns` and `nota_dinas`

5. REPORTING
   └─ Select date range + filter by unit/type
   └─ Generate filtered report view
   └─ Print-ready output for Surat Masuk, Surat Keluar, and Surmas

6. ADMINISTRATION
   └─ Manage users, departments (Bagian), archive codes
   └─ View audit trail through last-login timestamps
```

---

## 📸 Screenshots

<div align="center">

|                                         |                                     |
| :-------------------------------------: | :---------------------------------: |
|          **Dashboard / Home**           |           **Login Page**            |
| ![Dashboard](screenshots/dashboard.png) |   ![Login](screenshots/login.png)   |
|         **Incoming Mail List**          |       **Outgoing Mail Form**        |
|   ![SM List](screenshots/sm_list.png)   | ![SK Form](screenshots/sk_form.png) |
|               **Report**                |         **User Management**         |
|   ![Report](screenshots/laporan.png)    |   ![Users](screenshots/users.png)   |

</div>

> _Run the application locally to see the live interface._

---

## 📈 Project Impact

- 🏛️ **Deployed in an organizational environment** — actively used by staff across multiple departments
- ⚡ **Eliminates manual letter tracking** — replaces error-prone paper registers with a searchable digital archive
- 🔢 **Automated document numbering** — reduces administrative overhead and prevents duplicate or incorrect letter numbers
- 📁 **Structured archiving** — implements the national government archive classification standard, ensuring compliance and auditability
- 📊 **Reporting at scale** — generates printable correspondence reports on demand, filterable by date range and organizational unit
- 👥 **Multi-user support** — supports concurrent access for multiple staff members with individual session isolation

---

## 🔒 Source Code

This is a production-grade system used in real organizational environments.

The full source code is hosted in a **private repository** to protect intellectual property.

However, I'm happy to provide access to:

- 👨‍💻 **Interviewers** – for code review and architecture evaluation
- 🤝 **Collaborators** – for contributions and improvements

Please contact me for access.

[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)

---

## 📊 Project at a Glance

| Metric                            | Value                                |
| --------------------------------- | ------------------------------------ |
| **Backend Framework**             | CodeIgniter 3 (PHP)                  |
| **Controllers**                   | 3 (Web, Users, SuratController)      |
| **Database Tables**               | 12+                                  |
| **Correspondence Types**          | 4 (SM, SK, Nota Dinas, Surmas, Memo) |
| **Report Views**                  | 6 (SM, SK, Surmas — list & print)    |
| **Archive Classification Codes**  | 100+ (national standard)             |
| **Authentication Mechanism**      | Session-based with email token reset |
| **Supported Regions (Reference)** | 38 Kab/Kota (East Java)              |

---

## 🗺️ Future Improvements

- [ ] Role-Based Access Control (RBAC) with granular permissions per module
- [ ] REST API layer for mobile app integration
- [ ] PDF generation (server-side) using TCPDF or DomPDF
- [ ] Digital signature support for official letters
- [ ] Full-text search across all correspondence
- [ ] Email notification on new incoming letters
- [ ] Activity / audit log per user
- [ ] Docker containerization for portable deployment

---

## 👤 Author

<div align="center">

**Achmad Fahmi Al Hafidz**
_Backend Engineer · PHP · CodeIgniter · Python · Django_

[![GitHub](https://img.shields.io/badge/GitHub-fidzst-181717?style=for-the-badge&logo=github)](https://github.com/fidzst)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin)](https://linkedin.com/in/your-profile)
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-4A90E2?style=for-the-badge&logo=vercel&logoColor=white)](https://your-portfolio.com)

</div>

---

<div align="center">

_Built with dedication for real-world organizational efficiency — powered by PHP & CodeIgniter._

</div>
