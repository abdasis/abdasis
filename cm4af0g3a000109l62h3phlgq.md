---
title: "Cara Membuat User di PostgreSQL"
datePublished: Wed Dec 04 2024 21:43:36 GMT+0000 (Coordinated Universal Time)
cuid: cm4af0g3a000109l62h3phlgq
slug: cara-membuat-user-di-postgresql
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733348578093/98a472e6-7b0a-43ab-9e3e-6e308254d5a6.webp
tags: ubuntu, postgresql

---

Membuat user di PostgreSQL adalah langkah penting untuk mengelola akses ke database. Dengan membuat user, kamu dapat memberikan hak akses tertentu kepada pengguna untuk melakukan operasi yang diizinkan di database. Berikut adalah panduan langkah demi langkah untuk membuat user di PostgreSQL.

## Langkah 1: Masuk ke PostgreSQL

Pertama, kamu perlu masuk ke shell PostgreSQL. Untuk melakukan itu, buka terminal dan jalankan perintah berikut:

```bash
sudo -u postgres psql
```

Perintah ini akan masuk ke PostgreSQL dengan menggunakan user `postgres` yang memiliki hak akses penuh ke semua database.

## Langkah 2: Membuat User Baru

Setelah berhasil masuk ke PostgreSQL, kamu bisa membuat user baru dengan perintah `CREATE USER`. Berikut sintaks dasar untuk membuat user:

```sql
CREATE USER nama_user WITH PASSWORD 'kata_sandi';
```

Gantilah `nama_user` dengan nama pengguna yang ingin dibuat, dan `kata_sandi` dengan kata sandi yang ingin diberikan kepada user tersebut.

Contoh:

```sql
CREATE USER john_doe WITH PASSWORD '1234password';
```

Perintah ini akan membuat user dengan nama `john_doe` dan password `1234password`.

## Langkah 3: Memberikan Hak Akses ke User

Setelah membuat user, kamu dapat memberikan hak akses sesuai kebutuhan. Beberapa hak akses yang umum digunakan adalah:

### 1\. **Memberikan Hak Akses ke Database Tertentu**

Untuk memberikan akses ke database tertentu, kamu bisa menggunakan perintah `GRANT`. Misalnya, jika kamu ingin memberikan akses penuh ke database `mydb`, gunakan perintah berikut:

```sql
GRANT ALL PRIVILEGES ON DATABASE mydb TO john_doe;
```

Ini akan memberikan semua hak akses (misalnya, SELECT, INSERT, UPDATE, DELETE) ke database `mydb` untuk user `john_doe`.

### 2\. **Memberikan Akses Superuser**

Jika kamu ingin memberikan akses superuser (akses penuh ke semua database dan pengaturan PostgreSQL), kamu bisa menambahkan perintah `WITH SUPERUSER`:

```sql
ALTER USER john_doe WITH SUPERUSER;
```

**Catatan:** Berhati-hatilah saat memberikan hak superuser karena user ini dapat mengubah pengaturan penting dalam PostgreSQL.

### 3\. **Memberikan Akses ke Tabel atau Skema Tertentu**

Jika kamu ingin memberikan akses hanya ke tabel tertentu di dalam database, kamu bisa menggunakan perintah berikut:

```sql
GRANT SELECT, INSERT, UPDATE ON TABLE nama_tabel TO john_doe;
```

Misalnya, jika kamu ingin memberikan akses ke tabel `products` di database `mydb`, gunakan perintah seperti berikut:

```sql
GRANT SELECT, INSERT, UPDATE ON TABLE products TO john_doe;
```

Ini akan memberikan akses `SELECT`, `INSERT`, dan `UPDATE` pada tabel `products` untuk user `john_doe`.

## Langkah 4: Memverifikasi User dan Hak Akses

Untuk memverifikasi apakah user telah dibuat dan memiliki hak akses yang benar, kamu bisa menggunakan perintah berikut:

### 1\. **Cek User yang Tersedia**

```sql
\du
```

Perintah ini akan menampilkan daftar semua user yang ada di PostgreSQL beserta peran mereka.

### 2\. **Cek Hak Akses User ke Database**

Untuk melihat hak akses user ke database, gunakan perintah:

```sql
\l
```

Ini akan menampilkan daftar semua database dan user yang memiliki hak akses terhadapnya.

## Langkah 5: Keluar dari PostgreSQL

Setelah selesai membuat user dan memberikan hak akses, kamu bisa keluar dari sesi PostgreSQL dengan mengetikkan perintah:

```sql
\q
```

## Kesimpulan

Membuat user di PostgreSQL dan memberikan hak akses yang sesuai adalah langkah penting dalam mengelola database dengan aman. Dengan mengikuti langkah-langkah di atas, kamu bisa membuat user, memberikan hak akses ke database atau tabel tertentu, serta mengelola peran dan hak akses untuk setiap pengguna. Jangan lupa untuk selalu menjaga keamanan dengan memberikan hak akses yang hanya diperlukan oleh user tertentu.