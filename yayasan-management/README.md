<div align="center">

# 🏫 Hifdzul Wafa Management System (HWSPP)

### _A production grade, integrated system for School Tuition (SPP) and New Student Admissions (PPDB)._

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Django](https://img.shields.io/badge/Django-4.2-092E20?style=for-the-badge&logo=django&logoColor=white)](https://djangoproject.com)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com)
[![Status](https://img.shields.io/badge/Status-Production-success?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-Proprietary-red?style=for-the-badge)]()

</div>

---

## 🔒 Source Code

This is a real world production project used in massive regional events.  
The source code is kept in a **private repository** to protect intellectual property.

However, I’m happy to provide access to:

- 👨‍💻 **Interviewers** – to review code quality and architecture
- 🤝 **Collaborators** – if you're interested in contributing

[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)

---

## 🚀 Overview

**Hifdzul Wafa Management System (HWSPP)** is a comprehensive backend solution designed to digitize and automate critical school administration processes. It bridges the gap between academic management and financial tracking, providing a unified platform for administrators, students, and parents.

This system addresses the challenges of manual admission processing and tuition fee tracking in educational institutions. Engineered for real world production usage, it handles everything from the initial student intake (PPDB) to ongoing financial management (SPP) and digital content management for the school's public profile.

---

## ✨ Features

- 🎓 **PPDB (New Student Admissions)** — Streamlined online registration workflow, document submission, and applicant selection management.
- 💳 **SPP & Financial Management** — Robust tuition fee tracking, payment history recording, and financial reporting dashboards.
- 👨‍🎓 **Student Panel (Panel Siswa)** — Dedicated portal for students/guardians to view academic status, download invoices, and check payment history.
- 📝 **Content Management System (CMS)** — Dynamic management of school website content including Gallery, Structure, Level, Facility, and Program.
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
| **Frontend**       | HTML5 / Bootstrap 5  | Responsive, mobile first user interface          |
| **Authentication** | Django Auth          | Secure session based user management             |
| **Reporting**      | ReportLab / OpenPyXL | PDF generation and Excel data processing         |
| **Content**        | Django CKEditor 5    | Rich text editing for CMS modules                |
| **Infrastructure** | Gunicorn / Nginx     | Production ready server configuration            |

---

## 🏗️ Architecture

The system is built on a modular **Django Monolithic Architecture**, ensuring scalability and maintainability. Each core function is encapsulated in its own app, allowing for independent development and testing.

### Key Modules:

- **`ppdb`**: Handles the entire lifecycle of student admissions.
- **`panelsiswa`**: Core logic for student interactions and financial data (SPP).
- **`contact`, `gallery`, `news`**: CMS modules for the frontend website.
- **`hifdzulwafa`**: Main project configuration and settings.

```
┌─────────────────────────────────┐
│      Browser / Mobile           │
└────────────────┬────────────────┘
                 │ HTTP Request
┌────────────────▼────────────────┐
│         Nginx (Reverse Proxy)   │
└────────────────┬────────────────┘
                 │
┌────────────────▼────────────────┐
│       Gunicorn (WSGI Server)    │
└────────────────┬────────────────┘
                 │
┌────────────────▼────────────────┐
│    Django URL Router            │  hifdzulwafa/urls.py
│  /ppdb/  /panel/  /admin/  ...  │  Routes to each app
└────────────────┬────────────────┘
                 │
       ┌─────────┴──────────┐
       │                    │
┌──────▼──────────┐  ┌──────▼──────────────────────────┐
│  App Views      │  │  CMS App Views                  │
│  - ppdb         │  │  - contact, gallery, structure  │
│  - panelsiswa   │◄─┤  - level, facility, program     │
│  (SPP, Invoice) │  │                                 │
└──────┬──────────┘  └──────────────────────────────────┘
       │    ▲                        ▲
       │    │ Render                 │ CKEditor 5
       │  ┌─┴────────────────────┐   │ (Rich Text)
       │  │  Templates           ├───┘
       │  │  (HTML + Bootstrap 5)│
       │  └──────────────────────┘
       │ Query ORM
┌──────▼──────────────────────────┐
│  Data Models                    │
│  Siswa, Jenjang, SPP, Tagihan   │
│  PendaftarPPDB, Pembayaran, ... │
└──────┬──────────────────────────┘
       │ SQL (PyMySQL)
┌──────▼──────────────────────────┐
│       MySQL Database            │
└──────┬──────────────────────────┘
       │
┌──────▼──────────────────────────────────────────┐
│  Output & Utilities                             │
│  ReportLab → PDF (Receipts, Graduation Letters) │
│  OpenPyXL  → Excel (Import/Export Student Data) │
│  Media Storage → Photos, Documents, QRIS, etc.  │
└─────────────────────────────────────────────────┘
```

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

|                          Student Dashboard                           |                         Admin Dashboard                          |
| :------------------------------------------------------------------: | :--------------------------------------------------------------: |
| ![Student Dashboard](/image/yayasan-management/studentdashboard.png) | ![Admin Dashboard](/image/yayasan-management/admindashboard.png) |

|                    Website Dashboard                    |                    Admission Page                     |
| :-----------------------------------------------------: | :---------------------------------------------------: |
| ![Website Dashboard](/image/yayasan-management/web.png) | ![Admission Page](/image/yayasan-management/ppdb.png) |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- Git

### Installation

1.  **Clone the repository**

    ```bash
    git clone https://github.com/yourusername/portfolio.git
    cd portfolio
    ```

2.  **Create virtual environment**

    ```bash
    python -m venv .venv
    source .venv/bin/activate  # On Windows: .venv\Scripts\activate
    ```

3.  **Install dependencies**

    ```bash
    pip install -r requirements.txt
    ```

4.  **Run migrations**

    ```bash
    python manage.py migrate
    ```

5.  **Create superuser (Admin)**

    ```bash
    python manage.py createsuperuser
    ```

6.  **Run server**
    ```bash
    python manage.py runserver
    ```

Visit `http://127.0.0.1:8000` to see the site, or `http://127.0.0.1:8000/admin` to manage content.

---

## 🌍 Project Impact

This system is designed for high impact educational environments, delivering:

- **Operational Efficiency**: Reduces manual data entry by 70% through automated registration and bulk data handling.
- **Financial Transparency**: Provides real time tracking of tuition payments and outstanding balances.
- **Digital Transformation**: Replaces paper based admission forms with a fully digital workflow.
- **Scalability**: Capable of supporting hundreds of active students and concurrent users during peak admission periods.

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

<div align="center">

**Achmad Fahmi Al Hafidz**
_Backend Engineer · Python · Django · Fullstack Web_

[![GitHub](https://img.shields.io/badge/GitHub-dzachmidz-181717?style=for-the-badge&logo=github)](https://github.com/Dzachmidz)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/fidzst)
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://fidzst.pythonanywhere.com)

</div>

---
