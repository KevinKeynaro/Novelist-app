# LAPORAN PERANCANGAN SISTEM SWEETCRAFT
**Sistem Informasi Pemesanan Bakery & Custom Cake Pre-Order Berbasis Mobile (Flutter) dan REST API (Express.js & MySQL)**

---

## 1. PENDAHULUAN

### 1.1 Latar Belakang
Sektor Usaha Mikro, Kecil, dan Menengah (UMKM) di bidang kuliner, khususnya toko kue (*bakery & pastry*), memiliki karakteristik operasional yang khas:
1. Menyediakan produk siap saji (*ready-stock*) dengan jumlah dan masa simpan terbatas.
2. Melayani pesanan khusus (*custom cake / birthday cake*) yang menuntut penyesuaian desain, pesan dekorasi, rasa, ukuran, dan jadwal pengambilan.

Selama ini, transaksi pesanan kue kustom pada UMKM umumnya dilakukan secara manual melalui pesan instan (WhatsApp/Instagram direct message). Pendekatan manual ini menimbulkan beberapa masalah:
- Foto referensi desain sering tercecer atau tertukar antar pelanggan.
- Kesepakatan harga dan tenggat waktu tidak terdokumentasi terstruktur.
- Pemilik toko kesulitan memperbarui status pengerjaan kue kepada pelanggan secara transparan.

Aplikasi **SweetCraft** dirancang sebagai solusi digital terintegrasi untuk mendigitalkan seluruh siklus pemesanan toko kue UMKM, mulai dari etalase produk siap saji hingga alur kurasi pesanan kue kustom.

### 1.2 Tujuan Proyek
- Menyediakan katalog digital untuk produk bakery siap saji.
- Menyediakan fasilitas pengajuan pesanan kustom melalui pengunggahan foto referensi dan spesifikasi dekorasi.
- Mengotomatisasi peninjauan pesanan dan penentuan harga oleh pemilik toko (Penjual).
- Memberikan transparansi status pengerjaan pesanan kepada pelanggan (Pembeli).
- Memenuhi seluruh kriteria kompetensi asesmen: REST API (Express.js), basis data relasional (MySQL), autentikasi & otorisasi multi-role, manipulasi file/gambar (Cloudinary), dan aplikasi mobile client (Flutter).

---

## 2. SPESIFIKASI PENGGUNA & HAK AKSES (ROLE)

Sistem membedakan dua aktor utama dengan batas otorisasi yang tegas:

```
+-----------------------------------------------------------------+
|                           SWEETCRAFT                            |
+--------------------------------+--------------------------------+
|       ROLE: PENJUAL (OWNER)    |     ROLE: PEMBELI (CUSTOMER)   |
+--------------------------------+--------------------------------+
| - Kelola Menu Kue (CRUD)       | - Eksplorasi Katalog Menu      |
| - Upload Foto Menu             | - Pesan Produk Ready-Stock     |
| - Review Custom Pre-order      | - Ajukan Custom Pre-order      |
| - Input Harga Custom Cake      | - Upload Foto Referensi Desain |
| - Update Status Produksi       | - Lacak Riwayat & Status Order |
+--------------------------------+--------------------------------+
```

### 2.1 Penjual (Store Owner)
- **Katalog Produk**: Menambahkan produk baru, mengubah informasi harga/stok/deskripsi, menghapus produk, serta mengunggah foto produk ke server.
- **Kurasi Pesanan Kustom**: Melihat daftar pesanan kustom yang masuk, memeriksa foto referensi yang diunggah pembeli, dan menetapkan harga final berdasarkan tingkat kerumitan desain.
- **Manajemen Operasional**: Mengubah tahapan produksi (*Diterima*, *Diproses*, *Siap Diambil/Dikirim*, *Selesai*, atau *Ditolak*).

### 2.2 Pembeli (Customer)
- **Autentikasi**: Melakukan registrasi akun dan login mandiri untuk mendapatkan sesi berbasis JSON Web Token (JWT).
- **Pemesanan Ready-Stock**: Memilih menu dari etalase toko, menyertakan catatan tulisan ucapan/dekorasi ringan, dan menyelesaikan pesanan.
- **Pemesanan Custom Cake**: Mengisi formulir spesifikasi kue kustom, menyertakan deskripsi preferensi bahan/rasa, serta mengunggah file foto referensi desain dari galeri perangkat.
- **Pemantauan Status**: Memeriksa riwayat pesanan pribadi dan melihat pembaruan status pengerjaan secara manual (*pull-to-refresh*).

---

## 3. ARSITEKTUR TEKNOLOGI (TECH STACK)

```
[ Mobile Client: Flutter ]
           │ (HTTPS / Multipart Form-Data / JSON)
           ▼
[ REST API: Express.js (Node.js) ] ── (JWT / Zod Validation)
      │                     │
      ▼                     ▼
[ MySQL Database ]     [ Cloudinary Storage ]
 (Data Relasional)      (File Gambar & Referensi)
```

### 3.1 Backend & Basis Data
- **Node.js & Express.js (v5)**: Menyediakan RESTful API endpoint untuk autentikasi, manajemen menu, upload gambar, dan pengelolaan pesanan.
- **MySQL 8.x (`mysql2`)**: Basis data relasional penyimpan data pengguna, peran, kategori menu, produk kue, dan data transaksi pemesanan.
- **Keamanan & Autentikasi**:
  - `bcrypt`: Hashing password satu arah sebelum disimpan ke basis data.
  - `jsonwebtoken` (JWT): Stateless authentication token untuk proteksi endpoint privat.
- **Validasi Data**: `zod` untuk validasi skema request body sebelum diproses oleh controller.
- **Upload File**: `multer` sebagai middleware memory storage yang meneruskan file ke CDN pihak ketiga (**Cloudinary**), menghasilkan URL publik permanen.

### 3.2 Frontend Mobile
- **Flutter & Dart**: Antarmuka cross-platform dengan arsitektur modular.
- **HTTP Client**: Konsumsi REST API backend menggunakan format JSON dan pengiriman `multipart/form-data` untuk upload gambar.
- **Session Management**: Penyimpanan lokal token JWT dan identitas role pengguna.

---

## 4. PERANCANGAN BASIS DATA RELASIONAL

Sistem mengadopsi 4 entitas utama yang saling berelasi dengan integritas data berbasis *Primary Key* (PK) dan *Foreign Key* (FK):

```
+---------------+         +---------------+
|     ROLES     |         |  CATEGORIES   |
+---------------+         +---------------+
| id (PK)       |         | id (PK)       |
| name          |         | name          |
+-------+-------+         +-------+-------+
        │ 1                               │ 1
        │ N                               │ N
+-------v-------+         +-------v-------+
|     USERS     |         |     CAKES     |
+---------------+         +---------------+
| id (PK)       |         | id (PK)       |
| role_id (FK)  |         | category_id   |
| name          |         | name          |
| email (UQ)    |         | price         |
| password      |         | is_custom     |
| phone         |         | image_url     |
+-------+-------+         +-------+-------+
        │ 1                               │ 1
        │ N                               │ N
+-------v---------------------------------v-------+
|                     ORDERS                      |
+-------------------------------------------------+
| id (PK)                                         |
| user_id (FK -> users.id)                        |
| cake_id (FK -> cakes.id, nullable untuk custom) |
| order_type ('ready_stock' / 'custom')           |
| custom_image_url (nullable)                     |
| custom_description (nullable)                   |
| decoration_note (nullable)                      |
| agreed_price (DECIMAL)                          |
| pickup_date (DATETIME)                          |
| status ('pending', 'approved', 'processing',    |
|         'ready', 'completed', 'cancelled')      |
| created_at, updated_at                          |
+-------------------------------------------------+
```

### Penjelasan Relasi Entitas:
1. **`roles` ↔ `users` (1 : N)**: Setiap pengguna memiliki satu role (`penjual` atau `pembeli`).
2. **`categories` ↔ `cakes` (1 : N)**: Satu kategori (misal: *Tart, Cupcake, Pastry, Artisan Bread*) menaungi banyak produk kue.
3. **`users` ↔ `orders` (1 : N)**: Pengguna pembeli dapat memiliki banyak transaksi pemesanan.
4. **`cakes` ↔ `orders` (1 : N)**: Pesanan produk ready-stock merujuk langsung ke ID kue pada katalog. Untuk pesanan custom pre-order murni, kolom ini opsional (*nullable*) dan digantikan oleh `custom_image_url` serta `custom_description`.

---

## 5. SKENARIO ALUR BISNIS OPERASIONAL

```
1. PEMBELIAN KUE READY-STOCK
[Pembeli] Pilih menu -> Tambah catatan ucapan -> Submit Order (Status: Pending)
[Penjual] Cek pesanan -> Konfirmasi (Status: Processing) -> Update (Status: Ready / Completed)

2. PEMESANAN CUSTOM CAKE PRE-ORDER
[Pembeli] Form Custom -> Upload Foto Referensi + Catatan -> Submit (Status: Pending Review)
[Penjual] Tinjau Desain & Foto -> Input Nominal Harga Final (Status: Price Offered / Approved)
[Pembeli] Setuju dengan penawaran harga
[Penjual] Proses Produksi -> Update (Status: Processing -> Ready -> Completed)
```

---

## 6. PEMENUHAN KRITERIA ASESMEN (soal_asas_koke.md)

| No | Syarat Dokumen Ujian | Implementasi pada SweetCraft | Status |
| :--- | :--- | :--- | :--- |
| 1 | **Tema UMKM** | Operasional toko kue & bakery (katalog & pre-order). | Terpenuhi |
| 2 | **Database MySQL** | Skema 5 tabel berelasi PK-FK terstruktur. | Terpenuhi |
| 3 | **REST API Node.js/Express** | HTTP methods standar (GET, POST, PUT, DELETE) & JSON response. | Terpenuhi |
| 4 | **Autentikasi & Otorisasi** | Bcrypt hash password, JWT token, 2 Role (Penjual & Pembeli). | Terpenuhi |
| 5 | **CRUD 2 Data Berelasi** | CRUD Menu Kue (`categories` ↔ `cakes`) & Kelola Pesanan (`orders`). | Terpenuhi |
| 6 | **Upload & Serving File** | Upload foto menu & referensi custom cake via Multer + Cloudinary. | Terpenuhi |
| 7 | **Mobile App (Flutter)** | UI interaktif, form input, image picker, navigasi role-based. | Terpenuhi |
| 8 | **Akun Pengujian** | Akun Penjual (`penjual@sweetcraft.com`) dan Pembeli (`pembeli@sweetcraft.com`). | Terpenuhi |
