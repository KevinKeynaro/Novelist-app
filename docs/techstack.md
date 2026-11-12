# Novelist Tech Stack

## Backend

- **Runtime & Language**: Node.js, JavaScript (CommonJS)
- **Framework**: Express.js (v5)
- **Database**: MySQL via `mysql2/promise` (Connection pool, raw SQL)
- **Authentication & Security**:
  - `jsonwebtoken` (JWT 3 roles: Admin, Penjual, Pembeli)
  - `bcrypt` (Password hashing)
  - `cors` (Cross-origin resource sharing)
- **Validation**: `zod` (Request body & param validation)
- **File Upload & Storage**:
  - `multer` (Memory storage)
  - `cloudinary` (Cloud image hosting untuk cover buku)
- **Configuration**: `dotenv` (Environment variables)
- **Dev Tool**: `nodemon` (Hot reload)

### Out of Scope (Backend)
- Payment gateway
- Realtime chat

---

## Frontend

- **Framework**: Flutter (Dart)
- **Libraries**:
  - `image_picker` (Pick book covers)
  - `google_fonts`
