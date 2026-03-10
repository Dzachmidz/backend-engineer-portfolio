<div align="center">

# 📸 Raihmoment

### _A previously deployed, production grade Django powered company profile & service management platform for a professional photography and videography studio._

[![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Django](https://img.shields.io/badge/Django-4.2-092E20?style=for-the-badge&logo=django&logoColor=white)](https://djangoproject.com)
[![Bootstrap](https://img.shields.io/badge/Bootstrap-5-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)](https://getbootstrap.com)
[![MySQL](https://img.shields.io/badge/MySQL-Production-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://mysql.com)
[![Status](https://img.shields.io/badge/Status-Archived-lightgrey?style=for-the-badge)]()

</div>

---

## 🔒 Source Code

This was a production grade system previously deployed for a real world business.  
The source code is maintained in a **private repository** to protect intellectual property.

However, I'm happy to provide access to:

- 👨‍💻 **Interviewers** – to review code quality and system architecture
- 🤝 **Collaborators** – if you're interested in contributing

[![Email](https://img.shields.io/badge/Email-Contact_Me-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:fahmialhafidza@gmail.com)

---

## 📌 Overview

> **Raihmoment** is a full stack company profile and business management platform engineered for a professional photography & videography studio.

It solved the core challenge of digitizing a creative service business by centralizing service catalog management, pricing packages, client portfolio showcasing, equipment inventory, team presentation, and client inquiry handling — all within a single, maintainable Django system.

Designed for **real world production usage**, the platform gave studio administrators complete control over content via a rich admin interface while delivering a clean, responsive experience to prospective clients.

---

## ✨ Features

- 🎨 **Dynamic Service Catalog** — Manage photography and videography services with detailed descriptions, color theming, and rich HTML content via CKEditor 5.
- 💰 **Tiered Pricing Packages** — Create and showcase multiple pricing tiers per service, with itemized package inclusions and a "popular" flag for marketing emphasis.
- 🖼️ **Client Portfolio & Experiences** — Document completed client projects with descriptions, photography samples, client names, and dates — linked directly to the relevant service and package.
- 📷 **Gallery Management** — Attach multiple gallery images per portfolio entry for complete visual storytelling.
- 🔧 **Equipment Catalog** — Hierarchical equipment inventory (Category → Type → Item) with detailed spec sheets and images.
- 👥 **Team Profiles** — Present team members with roles, photos, and social media links (Instagram, LinkedIn, Twitter, Facebook).
- 📬 **Contact & Inquiry System** — Managed client inquiry form with backend capture for follow-up workflows.
- 🛡️ **Django Admin Panel** — Full CMS control: create, update, and manage all content without touching code.
- 🔗 **SEO Friendly URL Slugs** — Auto-generated slugs on all public-facing entities for clean, indexable URLs.

---

## 🛠️ Tech Stack

| Layer              | Technology               | Purpose                                |
| ------------------ | ------------------------ | -------------------------------------- |
| **Backend**        | Django 4.2 (Python 3.12) | Core logic, ORM, Admin CMS             |
| **Database**       | MySQL                    | Production data persistence            |
| **Rich Text**      | django ckeditor 5        | WYSIWYG content editing in admin       |
| **Image Handling** | Pillow                   | Media upload processing & validation   |
| **Frontend**       | Bootstrap 5 + jQuery     | Responsive UI & interactive components |
| **Infrastructure** | Nginx + Gunicorn         | Production-grade HTTP serving          |
| **Tools**          | Git, VS Code             | Version control, development           |

---

## 🏗️ Architecture

The project follows a **Modular Monolith** architecture — each business domain is encapsulated as an independent Django application while sharing a unified database and request pipeline.

```
┌──────────────────────────────┐
│     Browser / Client Device  │
└──────────────┬───────────────┘
               │ HTTP Request
┌──────────────▼───────────────┐
│     raihmoment/urls.py       │  Central URL dispatcher
└──────────────┬───────────────┘
               │
    ┌──────────▼──────────────────────────────────────────┐
    │                    Django Apps                       │
    │                                                      │
    │  services  │  experiences  │  equipments  │  gallery │
    │  team      │  contact                               │
    └──────────┬──────────────────────────────────────────┘
               │ ORM Queries
┌──────────────▼───────────────┐    ┌─────────────────────────┐
│       Data Models (ORM)      │◄───│   Templates (HTML+BS5)  │
│  (Service, Experience,       │    │   Context Processors     │
│   Equipment, Gallery, etc.)  │    └─────────────────────────┘
└──────────────┬───────────────┘
               │ SQL
┌──────────────▼───────────────┐
│        MySQL Database        │
│        (dbraihmoment)        │
└──────────────────────────────┘
```

### Key Modules

| Module        | Responsibility                                                 |
| ------------- | -------------------------------------------------------------- |
| `services`    | Service catalog, pricing packages, and package item breakdowns |
| `experiences` | Client portfolio entries linked to services and packages       |
| `equipments`  | Hierarchical equipment catalog (Category → Type → Item)        |
| `gallery`     | Multi-image gallery tied to individual portfolio entries       |
| `team`        | Team member profiles with social media links                   |
| `contact`     | Client inquiry form and submission management                  |

### Design Highlights

- **Context Processors** — `services.context_processors` injects the global service list into every template automatically, eliminating repetitive view-level queries.
- **Auto-Slug Generation** — All public models implement `save()` overrides to auto-generate URL-safe slugs from names and titles, ensuring SEO consistency.
- **Relational Integrity** — Foreign key chains (`Service → PackageHarga → RincianPaket`, `Experience → Gallery`) enforce referential integrity at the database level.
- **Rich Content Editing** — CKEditor 5 is integrated into the admin for service detail fields, enabling non-technical staff to manage structured content.

---

## 🔄 System Workflow

1. **Content Setup** — Studio admin creates services, pricing packages, and package inclusions via the Django admin panel.
2. **Portfolio Entry** — After completing a client session, admin logs the experience: links it to a service and package, uploads the hero image, and attaches gallery photos.
3. **Equipment Catalog Update** — Admin maintains the equipment inventory, adding new gear under the appropriate category and type hierarchy.
4. **Team Management** — Team member profiles are updated as the studio grows, with direct social media linking.
5. **Client Inquiry** — Prospective clients submit inquiries via the contact form; submissions are captured in the backend for manual follow-up.
6. **Public Presentation** — The frontend renders the live service catalog, portfolio, gallery, equipment list, team, and contact page dynamically from the database.

---

## 📸 Screenshots

<div align="center">

|                                                     |                                                 |
| :-------------------------------------------------: | :---------------------------------------------: |
|                     **Gallery**                     |             **Service Detail Page**             |
| ![Gallery](/image/event-organizer/raihmoment.jpeg)  | ![Service](/image/event-organizer/service.jpeg) |
|                    **Equipment**                    |                   **Contact**                   |
| ![Portfolio](/image/event-organizer/equipment.jpeg) |

</div>

---

## 🚀 Getting Started

> ⚠️ **Source code is in a private repository.** The steps below apply once access is granted.

### Prerequisites

- Python 3.10+
- MySQL Server
- Git

### Installation

1. **Clone the repository** _(requires granted access)_

   ```bash
   git clone https://github.com/Dzachmidz/Raihmoment.git
   cd Raihmoment
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

4. **Configure database** — Update `raihmoment/settings.py` with your MySQL credentials.

5. **Run migrations**

   ```bash
   python manage.py migrate
   ```

6. **Create superuser**

   ```bash
   python manage.py createsuperuser
   ```

7. **Start development server**
   ```bash
   python manage.py runserver
   ```

---

## 🌍 Project Impact

- 📦 Replaced static HTML pages with a **fully CMS driven** platform — zero code changes needed for content updates.
- 🔗 Enabled **direct service to portfolio linking**, giving clients a clear view of work produced at each pricing tier.
- 🧑‍💼 Reduced content management overhead significantly by centralizing all studio assets — services, portfolio, equipment, and team — in one admin panel.
- 📱 Responsive Bootstrap 5 frontend ensures optimal presentation across desktop and mobile devices.
- 🔍 Auto-slug generation on all entities delivers clean, SEO-friendly URLs with no manual configuration.

---

## 📊 Project at a Glance

| Metric                   | Value                                                           |
| ------------------------ | --------------------------------------------------------------- |
| **Backend Modules**      | 6 (services, experiences, equipments, gallery, team, contact)   |
| **Custom DB Tables**     | 11                                                              |
| **Total DB Tables**      | 17+ (incl. Django internals)                                    |
| **URL Endpoints**        | 15+                                                             |
| **Media Upload Paths**   | 6 (services, equipment, gallery, team, experiences, jenis_alat) |
| **Admin-Managed Models** | 11                                                              |

---

## 🗺️ Roadmap

- [x] Dynamic service catalog with tiered pricing
- [x] Client portfolio & gallery management
- [x] Hierarchical equipment inventory
- [x] Team profiles with social media integration
- [x] CKEditor 5 rich text integration
- [x] Auto-slug URL generation across all entities
- [ ] REST API layer for headless/mobile client support
- [ ] Client-facing booking & scheduling module
- [ ] Testimonials module with star ratings
- [ ] Email notification on contact form submission
- [ ] Image optimization pipeline (WebP conversion, lazy loading)

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
