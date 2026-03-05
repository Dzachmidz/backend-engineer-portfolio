<div align="center">

# 📋 Sistem Informasi Absensi Al Wafa

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

**Sistem Informasi Absensi Al Wafa** adalah sistem manajemen absensi berbasis RFID yang dirancang untuk lingkungan pendidikan nyata. Sistem ini menggantikan proses pencatatan kehadiran manual dengan solusi digital otomatis menggunakan kartu RFID yang terintegrasi langsung dengan hardware scanner (IoT device).

Sistem ini dibangun dengan arsitektur **monolitik modular** menggunakan Django, mengekspos **REST API** untuk komunikasi dengan perangkat keras RFID, dan menyediakan **panel admin berbasis web** yang kaya fitur untuk pengelolaan data siswa, kelas, jadwal, dan laporan kehadiran.

> Sistem ini telah digunakan secara aktif di lingkungan institusi pendidikan **Al Wafa**, mengelola data kehadiran siswa secara real-time setiap hari.

---

## ✨ Features

- 🔐 **Autentikasi Admin** — Login/logout aman berbasis session Django, seluruh halaman admin dilindungi `@login_required`
- 📡 **Integrasi Hardware RFID** — REST API endpoint khusus untuk menerima scan UID dari perangkat RFID (ESP32/Arduino)
- ⏱️ **Deteksi Status Otomatis** — Sistem secara cerdas menentukan status kehadiran: **Hadir**, **Terlambat**, atau **Telat Jemput** berdasarkan jam scan
- 🔄 **Multi-Sesi per Kelas** — Setiap kelas dapat memiliki beberapa sesi jadwal (Pagi/Sore), dengan toleransi waktu masuk/pulang yang dapat dikonfigurasi
- 📊 **Dashboard Real-Time** — Menampilkan total siswa, jumlah hadir hari ini, jumlah belum hadir, dan aktivitas absensi terbaru
- 👤 **Manajemen Siswa Lengkap** — CRUD siswa, import massal via file Excel, dan edit data individual
- 🏫 **Manajemen Kelas & Jadwal** — Kelola kelas beserta jadwal masuk & pulang per kelas, termasuk sesi jadwal khusus
- 🪪 **Registrasi Kartu RFID** — Daftarkan UID kartu RFID ke data siswa, dengan fitur pengecekan status kartu (sudah terdaftar / tersedia)
- ✍️ **Absensi Manual** — Entri absensi diluar RFID oleh admin untuk kondisi darurat
- 📜 **Riwayat Absensi** — Tabel histori lengkap seluruh data kehadiran dengan filter dan pagination
- 📤 **Export ke Excel** — Unduh laporan absensi dalam format `.xlsx` menggunakan `openpyxl`
- ⚙️ **Pengaturan Waktu Global** — Konfigurasi jam operasional global sistem dengan pola Singleton

---

## 🛠️ Tech Stack

| Layer               | Technology                     | Purpose                                      |
| ------------------- | ------------------------------ | -------------------------------------------- |
| **Backend**         | Django 4.x (Python 3.x)        | Core logic, ORM, routing, template rendering |
| **REST API**        | Django REST Framework          | Endpoint komunikasi hardware RFID            |
| **Database**        | SQLite (dev) / MySQL (prod)    | Penyimpanan data relasional                  |
| **Frontend**        | Bootstrap 5 + Django Templates | UI responsif & server-side rendering         |
| **IoT Integration** | ESP32 / Arduino (RFID Reader)  | Hardware scanner kartu RFID                  |
| **Export/Import**   | openpyxl                       | Generate & parse file Excel (.xlsx)          |
| **Authentication**  | Django Session Auth            | Keamanan panel admin                         |
| **Tools**           | Git, Virtualenv, Postman       | Version control & development tooling        |

---

## 🏗️ Architecture

Sistem ini menggunakan arsitektur **Django MTV (Model-Template-View)** dengan dua modul aplikasi utama yang terpisah secara bertanggung jawab:

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
│  - Data Siswa/Kelas │  │  - Serializers     │
│  - Riwayat Absensi  │  │  - Absensi Logic   │
│  - RFID Registrasi  │  └─────┬─────────────┘
│  - Absensi Manual   │        │ POST UID
└──────────┬──────────┘  ┌─────▼────────────┐
           │              │  RFID Hardware   │
┌──────────▼──────────────┤  (ESP32/Arduino) │
│      Data Models        └──────────────────┘
│  Siswa | Kelas | Absensi                   │
│  JadwalSesi | RfidLog                      │
│  WaktuOperasional (Singleton)              │
└──────────┬─────────────────────────────────┘
           │ SQL / ORM
┌──────────▼─────────────────────────────────┐
│         Database (SQLite / MySQL)           │
└────────────────────────────────────────────┘
```

### Modul Utama:

- **`userapp`** — Mengelola model data inti (`Siswa`, `Kelas`, `Absensi`, `JadwalSesi`, `RfidLog`, `WaktuOperasional`), REST API untuk hardware RFID, dan logika absensi otomatis.
- **`adminapp`** — Mengelola seluruh tampilan web admin: dashboard, manajemen data, registrasi RFID, riwayat absensi, dan fitur ekspor/impor data.

### Mekanisme Absensi Otomatis:

1. Hardware RFID mengirim `POST /api/rfid-scan/` dengan payload `{"uid": "XXXX"}`
2. Sistem mencari `Siswa` berdasarkan UID kartu
3. Jika ditemukan, sistem menentukan **mode absensi** (`masuk` / `pulang`) berdasarkan:
   - Ada/tidaknya record `Absensi` terbuka (jam_keluar null) hari ini
   - Jadwal waktu dari sesi kelas yang relevan
4. Status kehadiran dihitung otomatis: `Tepat Waktu` atau `Terlambat`
5. Response JSON dikirim kembali ke hardware (nama siswa, mode, pesan)

---

## 🔄 System Workflow

### Alur Absensi Masuk (Check-In)

```
[Tap Kartu RFID]
      │
      ▼
[Hardware POST → /api/rfid-scan/]
      │
      ▼
[Cari Siswa by RFID UID]
      │
      ├── Tidak Ditemukan → Log RfidLog (status: unknown) → Response Error
      │
      └── Ditemukan
              │
              ▼
      [Ambil Jadwal Kelas / Sesi Aktif]
              │
              ▼
      [Hitung Status: Tepat Waktu / Terlambat]
              │
              ▼
      [Simpan record Absensi ke Database]
              │
              ▼
      [Response: "Selamat Datang, {Nama}"]
```

### Alur Absensi Pulang (Check-Out)

```
[Tap Kartu RFID ke-2]
      │
      ▼
[Sistem deteksi ada open_absensi hari ini (jam_keluar = null)]
      │
      ▼
[Cek waktu saat ini >= jadwal_pulang_mulai]
      │
      ├── Belum Waktunya → Response: "Anda sudah absen masuk pukul HH:MM"
      │
      └── Sudah Waktunya
              │
              ▼
      [Update jam_keluar pada record Absensi]
              │
              ▼
      [Response: "Selamat Jalan, {Nama}"]
```

### Alur Admin Panel

```
1. Admin login → /login/ (session-based auth)
2. Dashboard → Lihat ringkasan hadir/tidak hadir hari ini
3. Kelola Kelas → Tambah/edit kelas + konfigurasi jadwal sesi
4. Kelola Siswa → CRUD + import Excel massal
5. Registrasi RFID → Daftarkan/cek kartu ke siswa
6. Absensi Manual → Input absensi tanpa RFID
7. Riwayat Absensi → Filter & export laporan ke Excel
```

---

## 📸 Screenshots

<div align="center">

|                                         |                                           |
| :-------------------------------------: | :---------------------------------------: |
|           **Admin Dashboard**           |              **Data Siswa**               |
| ![Dashboard](screenshots/dashboard.png) |  ![Students](screenshots/data_siswa.png)  |
|           **Riwayat Absensi**           |            **Registrasi RFID**            |
|   ![History](screenshots/riwayat.png)   | ![RFID](screenshots/registrasi_rfid.png)  |
|           **Manajemen Kelas**           |            **Absensi Manual**             |
|  ![Class](screenshots/data_kelas.png)   | ![Manual](screenshots/absensi_manual.png) |

</div>

> _Placeholder — jalankan sistem untuk melihat tampilan langsung._

---

## 🌍 Project Impact

- ✅ **Digunakan di institusi pendidikan nyata** — Sistem beroperasi aktif di **Al Wafa** untuk mencatat kehadiran siswa setiap hari
- ✅ **Mengeliminasi absensi manual** — Menggantikan pencatatan dengan kertas yang rawan kesalahan & manipulasi
- ✅ **Integrasi IoT** — Menghubungkan hardware RFID fisik langsung ke database digital melalui REST API
- ✅ **Efisiensi administrasi** — Admin dapat mengekspor laporan kehadiran ke Excel dalam hitungan detik
- ✅ **Deteksi real-time** — Status kehadiran (tepat waktu/terlambat) dihitung otomatis tanpa intervensi admin
- ✅ **Skalabilitas data** — Arsitektur mendukung penambahan kelas, sesi jadwal, dan siswa baru tanpa down-time

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

| Metric               | Value                                                             |
| -------------------- | ----------------------------------------------------------------- |
| **Backend Modules**  | 2 (`adminapp`, `userapp`)                                         |
| **Database Models**  | 6 (Siswa, Kelas, Absensi, JadwalSesi, RfidLog, WaktuOperasional)  |
| **API Endpoints**    | 1 REST + 9 Admin Routes                                           |
| **Admin Features**   | Dashboard, Students, Classes, Sessions, RFID Reg, Manual, History |
| **IoT Integration**  | RFID Card Reader (ESP32/Arduino over HTTP)                        |
| **Export Format**    | Excel (.xlsx) via openpyxl                                        |
| **Authentication**   | Django Session-based (Admin Panel)                                |
| **Deployment Ready** | Gunicorn + Nginx (Linux Server)                                   |

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
