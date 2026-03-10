<div align="center">

# 🏕️ Scouting Information System

### _A previously deployed, production grade CMS & information portal for a district level Scouting organization._

[![PHP](https://img.shields.io/badge/PHP-7.4+-777BB4?style=for-the-badge&logo=php&logoColor=white)](https://php.net)
[![CodeIgniter](https://img.shields.io/badge/CodeIgniter-3.x-EF4223?style=for-the-badge&logo=codeigniter&logoColor=white)](https://codeigniter.com)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-3/4-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com)
[![Status](https://img.shields.io/badge/Status-Archived-lightgray?style=for-the-badge)]()
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)]()

</div>

---

## 🔒 Source Code

This was a production grade CMS & information portal previously deployed for a real district level Scouting organization.  
The source code is kept in a **private repository** to protect intellectual property.

However, I’m happy to provide access to:

- 👨‍💻 **Interviewers** – to review code quality and architecture
- 🤝 **Collaborators** – if you're interested in contributing

[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)

---

## 📌 Overview

> **Scouting Information System** is a fullstack web portal and Content Management System built for a district level Scouting (_Kepramukaan_) organization in Indonesia.

The system was designed to solve a real operational problem: the organization needed a centralized, easily managed digital presence to publish news, announce events, manage multimedia content, and engage the public — all without relying on a technical team for day to day updates.

Built on **CodeIgniter 3 (PHP MVC framework)** and previously deployed in a live government/organization environment, the platform handled everything from public-facing content delivery to a secure, role-based back office management panel.

---

## ✨ Features

- 🔐 **Secure Authentication System** — Session based login with CAPTCHA verification and `password_hash` encryption for admin access
- 🗞️ **News & Article Management** — Full CRUD for news articles with categories, tags, SEO friendly slugs, and comment moderation
- 📅 **Event & Agenda Module** — Create, publish, and display upcoming events linked to registered users
- 🖼️ **Multimedia Management** — Dedicated modules for photo albums, video playlists, image galleries, and banner sliders
- 📂 **File Download Center** — Upload and serve downloadable files (documents, forms, resources) to the public
- 📊 **Polling / Survey System** — Built in public polling with answer tracking and result display
- 📢 **Announcement Board** — Quick publish announcements displayed on the homepage
- 🧩 **Dynamic Menu Builder** — Configure multi level navigation menus from the admin panel
- 🎨 **Template & Appearance Settings** — Switch between website templates and customize headers, logos, and backgrounds
- 📬 **Contact Form** — Public inquiry form with data storage and admin review
- 📈 **Visitor Statistics** — Basic hit counter and visit statistics per page/article
- 👤 **Role-Based User Management** — Multi-level admin roles (`admin`, `operator`) with per module access control (`users_modul`)
- 🛡️ **Profanity Filter** — Automated bad word filtering for public comments and form submissions
- 📰 **RSS Feed** — Auto generated RSS feed for news syndication

---

## 🛠️ Tech Stack

| Layer              | Technology                     | Purpose                                 |
| ------------------ | ------------------------------ | --------------------------------------- |
| **Backend**        | PHP 7.4+, CodeIgniter 3        | MVC framework, routing, business logic  |
| **Database**       | MySQL 8.0                      | Relational data persistence (35 tables) |
| **Frontend**       | Bootstrap, HTML5, CSS3, jQuery | Responsive UI and templating            |
| **Rich Text**      | CKEditor 4                     | WYSIWYG content editing for articles    |
| **File Manager**   | KCFinder                       | Web-based media upload and management   |
| **Web Server**     | Apache + mod_rewrite           | Clean URL routing (htaccess)            |
| **Infrastructure** | Linux / cPanel Hosting         | Shared/VPS production deployment        |
| **Dev Tools**      | Git, phpMyAdmin, Composer      | Version control & database management   |

---

## 🏗️ Architecture

The application follows a clean **MVC (Model-View-Controller)** architecture enforced by CodeIgniter 3, structured for maintainability and separation of concerns.

```
┌─────────────────────────────────────┐
│         Browser / Public User       │
└────────────────┬────────────────────┘
                 │ HTTP Request
┌────────────────▼────────────────────┐
│    Apache + mod_rewrite (.htaccess) │ Clean URL routing
└────────────────┬────────────────────┘
                 │
┌────────────────▼────────────────────┐
│         CodeIgniter Router          │ Maps URI segments to controllers
└────────────────┬────────────────────┘
                 │
      ┌──────────┴───────────┐
      │                      │
┌─────▼──────┐      ┌────────▼────────┐
│ Controllers│      │  Administrator  │  Secure admin panel
│ (Public)   │      │  Controller     │  (role-based access)
│            │      │  (2800+ lines)  │
│ Main       │      └────────┬────────┘
│ Berita     │               │
│ Agenda     │      ┌────────▼────────┐
│ Albums     │      │  Session Auth   │  CAPTCHA + password_hash
│ Download   │      └────────┬────────┘
│ Halaman    │               │
│ Hubungi    │      ┌────────▼────────┐
│ Playlist   │      │   Models        │
│ Tag, etc.  │◄─────┤ Model_utama     │  Generic CRUD abstraction
└─────┬──────┘      │ Model_app       │  Auth & user management
      │             │ Model_menu      │  Navigation builder
      │             └────────┬────────┘
      │                      │
      └──────────┬───────────┘
                 │ SQL Queries
┌────────────────▼────────────────────┐
│         MySQL Database              │
│         (35 Tables)                 │
└────────────────┬────────────────────┘
                 │
┌────────────────▼────────────────────┐
│     Views / Template Engine         │  Swappable template system
│  (dinas-1 theme + CKEditor)         │
└─────────────────────────────────────┘
```

### Key Architectural Decisions

| Decision                      | Detail                                                                                                                           |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| **Generic Model Layer**       | `Model_utama` provides a reusable query abstraction (`view_join`, `view_where_ordering_limit`, etc.) used across all controllers |
| **Role-Based Access Control** | `users_modul` table maps users to permitted admin modules                                                                        |
| **Swappable Template System** | Template name is stored in the database; views are loaded dynamically                                                            |
| **CAPTCHA on Public Forms**   | All public submission forms (comments, contact, login) are protected by a server-rendered CAPTCHA                                |
| **SEO-Friendly URLs**         | Every article and category uses a `*_seo` slug column, resolved through `mod_rewrite`                                            |

---

## 🔄 System Workflow

### Public Frontend Flow

1. **Request Routing** — Apache's `mod_rewrite` strips `index.php` and routes the clean URL to CodeIgniter's front controller
2. **Controller Dispatch** — The matched controller (e.g., `Berita`, `Agenda`) loads the required model and queries the database
3. **Data Aggregation** — The homepage controller (`Main`) aggregates data from multiple modules: latest news, polling, videos, announcements
4. **Category Resolution** — News articles are resolved to categories via `kategori_seo` slugs for SEO-friendly browsing
5. **View Rendering** — The template engine loads the active theme layout and injects the content view, assembling the final page

### Admin Panel Flow

1. **Authentication** — Admin accesses `/administrator`; session-based login is protected by CAPTCHA and `password_verify()`
2. **Module Access Check** — After login, the user's permitted modules are fetched from `users_modul` and rendered in the sidebar
3. **Content Operations** — Admins perform CRUD on all content types (news, events, galleries, downloads, menus, settings)
4. **Media Upload** — Rich media is handled via KCFinder (file manager) and CKEditor (inline image embedding)
5. **Visitor Counter** — Each page view increments a statistics counter stored in the `statistik` table

---

## 📸 Screenshots

<div align="center">

|                                           |                                     |
| :---------------------------------------: | :---------------------------------: |
|       **Homepage / Public Portal**        |       **News Article Detail**       |
|   ![Homepage](/image/scout-system/dashboard.png)   | ![Article](/image/scout-system/article.png) |
|            **Admin Dashboard**            |    **Content Management Panel**     |
| ![Admin](/image/scout-system/admin.png) |  ![CMS](/image/scout-system/content.png)  |

</div>

---

## 📊 Project Impact

- 🏛️ **Deployed for a real district-level government/organization unit** — served as the official digital presence for a Scouting organization
- 👥 **Supports multi-role teams** — administrators and operators could independently manage their assigned content modules
- 📰 **Centralizes content operations** — eliminated manual HTML editing by providing a full back-office CMS
- ⚡ **Automates public communication** — announcements, events, and news were instantly published to the public portal upon admin approval
- 🗂️ **Consolidates 35+ data entities** — from news and videos to polling, file downloads, banners, and visitor analytics in a single unified system
- 🔒 **Production-hardened security** — CAPTCHA verification, `password_hash` encryption, session-based auth, and direct-access protection on all PHP files

---

## Project at a Glance

| Metric                        | Value                                                                           |
| ----------------------------- | ------------------------------------------------------------------------------- |
| **Framework**                 | CodeIgniter 3 (PHP MVC)                                                         |
| **Backend Controllers**       | 14                                                                              |
| **Database Tables**           | 35                                                                              |
| **Admin Panel Lines of Code** | 2,800+                                                                          |
| **Content Modules**           | News, Events, Gallery, Videos, Downloads, Polling, Banners, Menus, Pages, Links |
| **User Roles**                | 2 (Admin, Operator)                                                             |
| **Template System**           | Dynamic / Swappable                                                             |
| **Deployment Environment**    | Apache + MySQL / cPanel Hosting                                                 |

---

## 🗺️ Future Improvements

- [ ] **REST API Layer** — Expose content endpoints for mobile app consumption
- [ ] **Laravel Migration** — Refactor to Laravel for improved DI, testing, and modern tooling
- [ ] **Full-Text Search** — Upgrade article search with MySQL FULLTEXT or Elasticsearch integration
- [ ] **Email Notifications** — SMTP-based notifications for new comments and contact form submissions
- [ ] **Docker Support** — Containerize the development environment for faster onboarding
- [ ] **SEO Enhancements** — Add dynamic sitemap generation and Open Graph meta tags
- [ ] **Two-Factor Authentication (2FA)** — Strengthen admin login security
- [ ] **Audit Log** — Track all admin actions with timestamps and user attribution

---

## 👤 Author

<div align="center">

**Achmad Fahmi Al Hafidz**
_Backend Engineer · Python · Django · Fullstack Web Developer_

[![GitHub](https://img.shields.io/badge/GitHub-dzachmidz-181717?style=for-the-badge&logo=github)](https://github.com/Dzachmidz)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/fidzst)
[![Email](https://img.shields.io/badge/Email-Contact-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://fidzst.pythonanywhere.com)

</div>

---
