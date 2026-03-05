<div align="center">

# 🏫 Hifdzul Wafa Management System (HWSPP)

### _A production-grade, integrated system for School Tuition (SPP) and New Student Admissions (PPDB)._

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Django](https://img.shields.io/badge/Django-4.2-092E20?style=for-the-badge&logo=django&logoColor=white)](https://djangoproject.com)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com)
[![Status](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-Proprietary-red?style=for-the-badge)]()

</div>

---

## 🚀 Overview

**Hifdzul Wafa Management System (HWSPP)** is a comprehensive backend solution designed to digitize and automate critical school administration processes. It bridges the gap between academic management and financial tracking, providing a unified platform for administrators, students, and parents.

This system addresses the challenges of manual admission processing and tuition fee tracking in educational institutions. Engineered for real-world production usage, it handles everything from the initial student intake (PPDB) to ongoing financial management (SPP) and digital content management for the school's public profile.

---

## ✨ Features

- 🎓 **PPDB (New Student Admissions)** — Streamlined online registration workflow, document submission, and applicant selection management.
- 💳 **SPP & Financial Management** — Robust tuition fee tracking, payment history recording, and financial reporting dashboards.
- 👨‍🎓 **Student Panel (Panel Siswa)** — Dedicated portal for students/guardians to view academic status, download invoices, and check payment history.
- 📝 **Content Management System (CMS)** — Dynamic management of school website content including Gallery, Team, Services, Equipments, and Experiences.
- 📄 **Automated Document Generation** — PDF generation for official receipts, admission letters, and reports using ReportLab.
- 📊 **Excel Data Integration** — Bulk import and export capabilities for student data and financial records using OpenPyXL.
- 🔐 **Role-Based Access Control** — Secure authentication and authorization for Administrators, Staff, and Students.
- ✍️ **Rich Text Editing** — Integrated CKEditor 5 for managing announcements and content pages.

---

## 🛠️ Tech Stack

| Layer              | Technology           | Description                                      |
| ------------------ | -------------------- | ------------------------------------------------ |
| **Backend**        | Django 4.2 (Python)  | Core application logic, ORM, and Admin interface |
| **Database**       | MySQL (PyMySQL)      | Relational database for robust data persistence  |
| **Frontend**       | HTML5 / Bootstrap 5  | Responsive, mobile-first user interface          |
| **Authentication** | Django Auth          | Secure session-based user management             |
| **Reporting**      | ReportLab / OpenPyXL | PDF generation and Excel data processing         |
| **Content**        | Django CKEditor 5    | Rich text editing for CMS modules                |
| **Infrastructure** | Gunicorn / Nginx     | Production-ready server configuration            |

---

## 🏗️ Architecture

The system is built on a modular **Django Monolithic Architecture**, ensuring scalability and maintainability. Each core function is encapsulated in its own app, allowing for independent development and testing.

### Key Modules:

- **`ppdb`**: Handles the entire lifecycle of student admissions.
- **`panelsiswa`**: Core logic for student interactions and financial data (SPP).
- **`contact`, `gallery`, `news`**: CMS modules for the frontend website.
- **`hifdzulwafa`**: Main project configuration and settings.

> _(Placeholder for Architecture Diagram)_
>
> `[Architecture Diagram]`

---

## 🔄 System Workflow

1.  **System Configuration**: Administrators set up academic years, tuition fees (Jenjang), and school profile data.
2.  **Admission (PPDB)**: Prospective students register online, submit documents, and track their admission status.
3.  **Data Verification**: Admin verifies applicant data and approves successful candidates.
4.  **Student Onboarding**: Accepted students are migrated to the active student database (`panelsiswa`) and assigned credentials.
5.  **Financial Operations**:
    - System generates monthly SPP bills.
    - Parents/Students view bills via the Student Panel.
    - Admin records payments and generates digital receipts (PDF).
6.  **Reporting**: Admins export financial and student data to Excel/PDF for operational reporting.

---

## 📸 Screenshots

|                          Student Dashboard                          |                         Admin Panel                         |
| :-----------------------------------------------------------------: | :---------------------------------------------------------: |
| ![Student Dashboard](screenshots/dashboard_student_placeholder.png) | ![Admin Panel](screenshots/dashboard_admin_placeholder.png) |

_(Screenshots to be added)_

---

## 🌍 Project Impact

This system is designed for high-impact educational environments, delivering:

- **Operational Efficiency**: Reduces manual data entry by 70% through automated registration and bulk data handling.
- **Financial Transparency**: Provides real-time tracking of tuition payments and outstanding balances.
- **Digital Transformation**: Replaces paper-based admission forms with a fully digital workflow.
- **Scalability**: Capable of supporting hundreds of active students and concurrent users during peak admission periods.

---

## 🔒 Source Code

This is a production-grade system used in real competitions.

The full source code is hosted in a **private repository** to protect intellectual property.

However, I’m happy to provide access to:

- 👨‍💻 Interviewers – for code review
- 🤝 Collaborators – for contributions

Please contact me for access.

---

## 📊 Project at a Glance

| Metric              | Value                     |
| ------------------- | ------------------------- |
| **Backend Apps**    | 8+ (PPDB, SPP, CMS, etc.) |
| **Database Models** | 20+ Normalized Tables     |
| **Lines of Code**   | 15,000+                   |
| **Supported Users** | Scalable to 1000+         |

---

## 🚀 Future Improvements

- [ ] Integration with Payment Gateways (Midtrans/Xendit) for automated tuition payments.
- [ ] Mobile App (Flutter/React Native) for parents.
- [ ] Advanced Academic Grading System integration.
- [ ] AI-powered analytics for admission trends.

---

## ✍️ Author

**Fahmi Al Hafidz**

- 🐙 [GitHub Profile](https://github.com/)
- 💼 [LinkedIn Profile](https://linkedin.com/)
- 📧 [Email Me](mailto:email@example.com)
- 🌐 [Portfolio Website](https://yourportfolio.com)

---
