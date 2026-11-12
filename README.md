# SweetCraft - Bakery & Cake Pre-order System

Aplikasi mobile pemesanan kue dan produk bakery berbasis UMKM. Mendukung pembelian produk siap saji (*ready-stock*) serta pengajuan pesanan kustom (*custom cake pre-order*) dengan unggah foto referensi desain dan penyesuaian dekorasi.

---

## Daftar Isi
- [Latar Belakang](#latar-belakang)
- [Fitur Utama](#fitur-utama)
- [Hak Akses & Aktor](#hak-akses--aktor)
- [Tech Stack](#tech-stack)
- [Struktur Direktori](#struktur-direktori)
- [Alur Kerja Sistem](#alur-kerja-sistem)
- [Instalasi & Menjalankan Proyek](#instalasi--menjalankan-proyek)

---

## Latar Belakang
UMKM bakery sering menghadapi kendala dalam pencatatan pesanan khusus (*custom cake*), pengelolaan variasi dekorasi, dan transparansi status pesanan pelanggan. SweetCraft mendigitalisasi operasional toko kue melalui REST API mandiri dan aplikasi mobile Flutter, mencakup katalog produk, pengunggahan foto referensi pesanan kustom, penentuan harga terkurasi, dan pemantauan status produksi.

---

## Fitur Utama

### 1. Pembeli (Customer)
- **Katalog Ready-Stock**: Menjelajahi daftar kue siap pesan dengan filter kategori/varian.
- **Kustomisasi Dekorasi**: Opsi request pesan ucapan atau modifikasi dekorasi pada menu yang mendukung.
- **Pengajuan Custom Pre-order**: Mengunggah foto referensi kue kustom beserta deskripsi detail kebutuhan.
- **Pelacakan Status Pesanan**: Memantau progres pesanan secara berkala (*Menunggu Konfirmasi*, *Diterima*, *Diproses*, *Siap Diambil/Dikirim*, *Selesai*).

### 2. Penjual (Store Owner)
- **Manajemen Menu (CRUD)**: Menambah, melihat, memperbarui, dan menghapus menu kue beserta foto produk.
- **Review & Kurasi Custom Cake**: Meninjau foto referensi dan deskripsi dari pembeli, menetapkan harga akhir pesanan kustom.
- **Manajemen Status Pesanan**: Mengubah status tahapan produksi dan penyelesaian pesanan.

---

## Hak Akses & Aktor

| Peran (Role) | Hak Akses & Kemampuan |
| :--- | :--- |
| **Penjual (Owner)** | Akses penuh CRUD menu katalog, upload foto menu ke Cloudinary, review custom pre-order, input harga pesanan custom, update status produksi pesanan. |
| **Pembeli (Customer)** | Registrasi & login, melihat katalog menu, membuat pesanan ready-stock, upload foto referensi custom cake, melihat histori dan status pesanan pribadi. |

---

## Tech Stack

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MySQL (Driver: `mysql2`)
- **Keamanan & Autentikasi**: JSON Web Token (`jsonwebtoken`), Password Hashing (`bcrypt`)
- **Validasi Data**: Zod
- **Media Storage**: Cloudinary via Multer memory storage

### Frontend Mobile
- **Framework**: Flutter
- **Bahasa**: Dart
- **Arsitektur Komunikasi**: REST API Client via HTTP request

---

## Struktur Direktori

```text
Novelist-app/
├── backend/
│   ├── database/             # File migrasi / skema SQL
│   │   └── schema.sql        # DDL struktur tabel basis data
│   ├── src/
│   │   ├── config/           # Konfigurasi database & third-party service (Cloudinary)
│   │   ├── controllers/      # Logika pemrosesan request & response
│   │   ├── middlewares/      # Middleware auth JWT, role-guard, & multer upload
│   │   ├── models/           # Query abstraction basis data
│   │   ├── routes/           # Definisi endpoint REST API
│   │   ├── services/         # Business logic terpusat
│   │   ├── utils/            # Helper fungsi, response formatter
│   │   └── validations/      # Skema validasi request (Zod)
│   ├── .env.example          # Contoh variabel lingkungan
│   ├── package.json          # Dependensi dan script backend
│   └── index.js              # Entry point server Express
├── docs/
│   └── soal_asas_koke.md     # Dokumen acuan spesifikasi tugas
├── frontend/
│   ├── android/              # Konfigurasi platform Android
│   ├── lib/
│   │   ├── core/             # Konfigurasi tema, konstanta, network client
│   │   ├── models/           # Data model serialisasi JSON
│   │   ├── providers/        # State management antarmuka
│   │   ├── services/         # HTTP service pemanggil REST API
│   │   ├── views/            # Layar antarmuka (Auth, Menu, Order, Admin)
│   │   └── widgets/          # Komponen antarmuka yang dapat digunakan ulang
│   └── pubspec.yaml          # Dependensi Flutter
└── README.md
```

---

## Alur Kerja Sistem

### 1. Pesanan Ready-Stock
1. Pembeli melihat katalog kue dan memilih menu yang tersedia.
2. Pembeli menambahkan catatan dekorasi (bila tersedia) dan membuat pesanan.
3. Penjual menerima pesanan dan memproses status ke tahap pembuatan.

### 2. Pesanan Custom Pre-Order
1. Pembeli membuka form custom cake.
2. Pembeli mengunggah foto referensi desain dan mengisi rincian deskripsi kue.
3. Foto terunggah ke Cloudinary, data pesanan tercatat dengan status `Menunggu Konfirmasi`.
4. Penjual meninjau gambar dan rincian, kemudian menetapkan harga pesanan.
5. Pembeli mengonfirmasi dan pesanan masuk ke tahap pengerjaan.

---

## Instalasi & Menjalankan Proyek

### Backend
1. Masuk ke direktori backend:
   ```bash
   cd backend
   ```
2. Pasang dependensi:
   ```bash
   npm install
   ```
3. Salin file `.env.example` menjadi `.env` dan lengkapi kredensial basis data serta Cloudinary:
   ```bash
   cp .env.example .env
   ```
4. Impor `backend/database/schema.sql` ke database MySQL Anda.
5. Jalankan server dalam mode pengembangan:
   ```bash
   npm run dev
   ```

### Frontend
1. Masuk ke direktori frontend:
   ```bash
   cd frontend
   ```
2. Ambil paket dependensi Flutter:
   ```bash
   flutter pub get
   ```
3. Jalankan aplikasi pada emulator atau perangkat fisik:
   ```bash
   flutter run
   ```
