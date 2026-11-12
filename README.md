# Novelist-app

Marketplace buku C2C (baru dan bekas) berbasis mobile (Flutter) dan REST API (Node.js/Express.js & MySQL).

## Tech Stack
- **Backend**: Node.js, Express.js
- **Database**: MySQL (`mysql2`)
- **Authentication**: JWT (`jsonwebtoken`), `bcrypt`
- **Validation**: Zod
- **Image Storage**: Cloudinary via Multer
- **Mobile Client**: Flutter

## Roles & Hak Akses
1. **Admin**
   - Mengawasi marketplace.
   - Menghapus postingan buku yang melanggar ketentuan.
   - Menghapus/menonaktifkan akun pelanggar.
   - *Out of Scope*: Sistem peringatan/surat teguran.

2. **Penjual**
   - Menjual buku baru (*brand-new*) dan bekas (*second-hand*).
   - Form buku baru: Judul, Penulis, Genre (kategori dropdown), Deskripsi/Sinopsis, Harga, Stok, Cover Buku.
   - Form buku bekas: Atribut buku baru ditambah form detail deskripsi kondisi/kerusakan buku.
   - Mengunggah foto buku ke Cloudinary.

3. **Pembeli**
   - Melihat katalog buku.
   - Mencari buku via search bar atau filter tags/genre.
   - Melihat detail buku (termasuk kondisi fisik buku bekas).
   - Melakukan transaksi pembelian buku.

## Scope & Batasan
- **In-Scope**: Auth 3 role (register/login/JWT), CRUD postingan buku, upload gambar, filter tag/genre & search, moderasi admin, relasi DB transaksi/pembelian.
- **Out-of-Scope**: Sistem surat teguran/peringatan, multi-vendor automated payout gateway.
