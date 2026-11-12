# PETUNJUK UMUM

1. Baca dan pahami seluruh instruksi sebelum mengerjakan.
2. Pengerjaan dilakukan secara individu.
3. Peserta menentukan sendiri tema proyek yang berkaitan dengan kegiatan Usaha Mikro, Kecil, dan Menengah (UMKM).
4. Gunakan MySQL atau PostgreSQL sebagai sistem manajemen basis data.
5. Backend wajib menggunakan Node.js dan Express.js serta menyediakan REST API.
6. Aplikasi mobile wajib dibuat menggunakan Flutter dan mengonsumsi REST API yang dikembangkan.
7. Terapkan validasi terhadap data yang diterima oleh sistem, baik pada sisi backend maupun antarmuka aplikasi.
8. Terapkan autentikasi untuk memastikan identitas pengguna dan otorisasi untuk membatasi akses berdasarkan hak/role pengguna.
9. Gunakan HTTP method dan HTTP status code yang sesuai pada REST API.
10. Seluruh data utama aplikasi harus tersimpan pada basis data, bukan hanya menggunakan data hardcode.
11. Fitur upload gambar atau file harus disimpan dan dapat diakses kembali melalui aplikasi.
12. Peserta wajib menyiapkan akun pengujian untuk setiap role yang diterapkan.
13. Peserta wajib menjelaskan kode program, struktur basis data, endpoint API, serta alur kerja aplikasi kepada penguji.

---

# TUJUAN PEMBELAJARAN YANG DIUJIKAN

| TUJUAN PEMBELAJARAN (PWD) | TUJUAN PEMBELAJARAN (Basis Data) |
| :--- | :--- |
| • Membangun REST API menggunakan Node.js dan Express.js.<br>• Menerapkan operasi CRUD pada data aplikasi.<br>• Menerapkan autentikasi dan otorisasi pengguna.<br>• Mengelola proses upload dan penyajian file/gambar. | • Menganalisis kebutuhan dan merancang basis data.<br>• Menyusun query DDL dan DML.<br>• Menerapkan Primary Key dan Foreign Key.<br>• Membangun relasi antar tabel serta menjaga integritas data. |

| TUJUAN PEMBELAJARAN (Pemrograman Mobile) |
| :--- |
| • Merancang dan membangun UI aplikasi mobile menggunakan Flutter.<br>• Mengintegrasikan aplikasi mobile dengan REST API.<br>• Menerapkan proses login dan pengelolaan sesi pengguna.<br>• Mengimplementasikan fitur CRUD dan upload file/gambar melalui aplikasi. |

---

# SOAL/TUGAS

**Judul Tugas :** Aplikasi Digital untuk UMKM  
**Deskripsi Tugas :** Buatlah sebuah aplikasi digital yang membantu proses operasional atau pelayanan suatu UMKM. Tema dan jenis UMKM dibebaskan, contohnya toko/retail, kuliner, laundry, jasa, kerajinan, pertanian, atau bidang UMKM lainnya.

**Sistem terdiri dari:**
1. Backend sebagai penyedia REST API menggunakan Node.js dan Express.js.
2. Database sebagai tempat penyimpanan data aplikasi menggunakan MySQL atau PostgreSQL.
3. Aplikasi mobile sebagai client yang dibangun menggunakan Flutter.
4. Penyimpanan file/gambar yang terintegrasi dengan backend.

## Kriteria Fitur:

### Fitur Backend / REST API:
* API menggunakan HTTP method yang sesuai (GET, POST, PUT/PATCH, DELETE).
* API memberikan HTTP status code yang sesuai dengan kondisi request.
* Response API minimal menggunakan format JSON dengan struktur yang konsisten.
* Menerapkan operasi CRUD minimal pada dua jenis data utama yang saling berhubungan sesuai tema proyek.
* Menerapkan autentikasi register dan login. Password harus disimpan dalam bentuk hash, bukan teks biasa.
* Menerapkan otorisasi berdasarkan role pengguna. Minimal terdapat dua role dengan hak akses yang berbeda.
* Endpoint yang bersifat privat harus dilindungi middleware autentikasi dan pemeriksaan role/hak akses.
* Menyediakan fitur upload minimal satu jenis file, berupa gambar atau dokumen, dengan validasi tipe dan ukuran file.
* Menerapkan validasi input dan penanganan error pada endpoint API.
* Data yang ditampilkan dan diolah harus berasal dari database.

### Fitur Mobile:
* Menampilkan halaman login dan register.
* Menampilkan halaman utama sesuai kebutuhan tema UMKM.
* Menampilkan daftar dan detail data utama.
* Menambahkan data baru melalui aplikasi.
* Mengedit data yang sudah tersimpan.
* Menghapus data dengan konfirmasi pengguna.
* Mengunggah gambar atau file melalui aplikasi.
* Menampilkan gambar/file yang telah diunggah.
* Menerapkan pembatasan tampilan atau aksi berdasarkan role pengguna.
* Menampilkan pesan atau informasi yang sesuai ketika proses berhasil maupun gagal.

### Struktur Database:
Peserta wajib membuat database untuk menyimpan data dengan ketentuan:
* Peserta wajib membuat database sesuai nama proyek masing-masing.
* Database minimal terdiri dari tabel `users`, tabel `role` atau mekanisme penyimpanan role pada `users`, serta minimal dua tabel data utama sesuai tema proyek.
* Tabel-tabel yang memiliki hubungan harus menggunakan Primary Key dan Foreign Key yang sesuai.
* Struktur database harus mendukung autentikasi, otorisasi, pengelolaan data utama, dan penyimpanan informasi file/gambar.
* Peserta wajib membuat ERD yang menggambarkan nama tabel, atribut, tipe data, Primary Key, Foreign Key, dan relasi antar tabel.
* Peserta wajib menyertakan file SQL atau migration untuk membuat struktur database.

---

**Catatan:** Tema proyek bebas selama masih berkaitan dengan UMKM. Peserta tidak diwajibkan membuat seluruh fitur bisnis yang kompleks; fokus penilaian adalah terpenuhinya persyaratan teknis minimal dan kesesuaian fitur dengan kebutuhan UMKM yang dipilih.

Fitur tambahan seperti pencatatan transaksi, laporan penjualan, pencarian, filter, notifikasi, atau dashboard dapat menjadi nilai tambah. Kreativitas, kerapian kode, keamanan, dan inovasi akan menjadi pertimbangan penguji.

### “SELAMAT & SUKSES”