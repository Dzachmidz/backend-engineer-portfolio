<div align="center">

# 🏅 GYMNASTIC SCORING SYSTEM: Integrated Sports Event Management System

### _A production grade, real time management system designed for large scale regional sports competitions._

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Django](https://img.shields.io/badge/Django-5.2-092E20?style=for-the-badge&logo=django&logoColor=white)](https://djangoproject.com)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5.3-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com)
[![MySQL](https://img.shields.io/badge/MySQL-Production-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com)
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

## 📌 Overview

> **Gimnastik Scoring System** is a comprehensive backend solution engineered to manage the entire lifecycle of large scale gymnastics and sports competitions — from regional club events to provincial-level championships.

It solves complex logistical challenges by digitizing participant registration, document verification, live scoring, referee management, and medal tallying across **multiple events**. Designed for high-reliability **real-world production usage**, this system eliminates manual paper trails, ensures data integrity during live events, and provides instantaneous results to officials and the public.

---

## ✨ Features

- 📝 **Registration & Verification** — Secure portal for clubs to register athletes with automated age categorization and document upload (ID, BPJS, KK).
- ⚡ **Live Scoring Engine** — Real time score entry and processing with sub second latency for public displays.
- 🥇 **Automated Medal Tally** — Dynamic calculation of medal standings globally and by category.
- 👮 **Referee Management** — Digital assignment and tracking system for match officials.
- 📄 **Document Generation** — Automated PDF creation for certificates, ID cards, and official reports.
- 🛡️ **Role-Based Access Control** — Granular permissions for Super Admins, Verifiers, Referees, and Club Officials.

---

## 🛠️ Tech Stack

| Layer              | Technology          | Purpose                          |
| ------------------ | ------------------- | -------------------------------- |
| **Backend**        | Django 5.2 (Python) | Core logic, ORM, Admin Interface |
| **Database**       | MySQL               | Production Data persistence      |
| **Frontend**       | Bootstrap 5, jQuery | Responsive UI & DataTables       |
| **Infrastructure** | Nginx + Gunicorn    | Production serving               |
| **Tools**          | Git, VS Code        | Version control & Development    |

---

## 🏗️ Architecture

The project follows a **Modular Monolith** architecture to ensure maintainability:

```
┌────────────────────────┐
│    Browser / Tablets   │
└───────────┬────────────┘
            │ HTTP Request
┌───────────▼────────────┐
│      Django URLs       │  Routes to apps (score, registration, etc)
└───────────┬────────────┘
            │
┌───────────▼────────────┐    ┌─────────────────┐
│       App Views        │◄───┤    Templates    │
│ (Score, Medal, Referee)│    │  (HTML + BS5)   │
└───────────┬────────────┘    └─────────────────┘
            │ Query
┌───────────▼────────────┐
│      Data Models       │
│ (Participant, Score, Club) │
└───────────┬────────────┘
            │ SQL
┌───────────▼────────────┐
│    MySQL Database      │
└────────────────────────┘
```

### Key Modules:

- **`skorapp`**: Core scoring engine and public display logic.
- **`pendaftaranapp`**: Participant registration, age verification, and file uploads.
- **`medaliapp`**: Aggregation logic for medal standings.
- **`wasitapp`**: Referee assignment and scoring input interfaces.
- **`printapp`**: PDF generation using WeasyPrint or similar tools.

---

## 🔄 Workflow

1.  **Registration**: Club officials register athletes and upload documents.
2.  **Verification**: Admins review documents; system auto-validates eligibility.
3.  **Event Setup**: Match schedules and referee assignments are configured.
4.  **Live Execution**:
    - Referees input scores via tablets.
    - System calculates totals instantly.
5.  **Broadcast**: Public dashboards update in real-time.
6.  **Reporting**: Final reports generated automatically.

---

## 📸 Screenshots

<div align="center">

|                                         |                                     |
| :-------------------------------------: | :---------------------------------: |
|              **Dashboard**              |       **Live Scoring Board**        |
| ![Dashboard](/image/gimnastik-scoring-system/dashboard.png) | ![Scoring](/image/gimnastik-scoring-system/liveskor.png) |
|      **Participant Verification**       |           **Medal Tally**           |
| ![Verification](/image/gimnastik-scoring-system/verification.png) |  ![Medal](/image/gimnastik-scoring-system/medals.png)   |

</div>

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- MySQL Server (or SQLite for dev)
- Git

### Installation

1.  **Clone the repository** (If granted access)

    ```bash
    git clone https://github.com/Dzachmidz/gymnastics-scoring-system.git
    cd gymnastics-scoring-system
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

5.  **Create superuser**

    ```bash
    python manage.py createsuperuser
    ```

6.  **Run server**
    ```bash
    python manage.py runserver
    ```

---

## 📊 Project at a Glance

| Metric              | Value                                                |
| ------------------- | ---------------------------------------------------- |
| **Modules**         | 7+ (Score, Registration, Medal, Referee, User, etc.) |
| **Database Tables** | 25+                                                  |
| **API Endpoints**   | 50+                                                  |
| **Users Supported** | Scalable to Thousands                                |

---

## 🗺️ Roadmap

- [x] Digital Registration & Verification
- [x] Real-time Scoring Engine
- [x] Automated Medal Tally
- [ ] REST API for Mobile App Integration
- [ ] Microservices Migration for specific modules
- [ ] AI-based Performance Analytics

---

## 👤 Author

<div align="center">

**Achmad Fahmi Al Hafidz**
_Backend Engineer · Python · Django · Fullstack Web_

[![GitHub](https://img.shields.io/badge/GitHub-dzachmidz-181717?style=for-the-badge&logo=github)](https://github.com/Dzachmidz)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/fidzst)
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://fidzst.pythonanywhere.com)

</div>

---
