---
title: "Mengatasi Error "Could not change directory to /home/user" pada PostgreSQL"
datePublished: Wed Dec 04 2024 20:57:33 GMT+0000 (Coordinated Universal Time)
cuid: cm4add8gh000009la8ik9cgmn
slug: mengatasi-error-could-not-change-directory-to-homeuser-pada-postgresql
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733345810458/46e3b2a4-4902-41b4-82cc-a664b6e9f43a.webp
tags: postgresql, debian

---

Menghadapi masalah saat menjalankan perintah `psql` dengan user `postgres` sering terjadi, terutama jika ada pengaturan izin direktori yang tidak sesuai. Artikel ini membahas penyebab dan solusi dari error berikut:

```bash
could not change directory to "/home/user"  
psql: could not connect to server: No such file or directory  
Is the server running locally and accepting connections on Unix domain socket "/var/run/postgresql/.s.PGSQL.5432"?
```

## Penyebab Error

Error ini biasanya muncul karena:

1. Direktori `/home` atau `/home/user` memiliki izin yang salah sehingga user `postgres` tidak dapat mengaksesnya.
    
2. Direktori **PGDATA** (lokasi data PostgreSQL) juga memiliki pengaturan izin yang tidak sesuai untuk user `postgres`.
    

Masalah ini dapat terjadi akibat kesalahan pengaturan izin, seperti menggunakan perintah berikut tanpa memahami dampaknya:

```bash
sudo chmod 777 -u postgres /home/user
```

Hal ini menyebabkan seluruh partisi home hanya dapat diakses oleh root.

## Langkah-Langkah Solusi

### 1\. Perbaiki Izin Direktori Home

Gunakan perintah berikut untuk memperbaiki izin:

```bash
sudo chmod og+rX /home /home/user
```

Perintah ini memastikan bahwa direktori `/home` dan `/home/user` dapat dibaca oleh user lain, termasuk `postgres`.

### 2\. Atur Izin pada Direktori PGDATA

Jika direktori **PGDATA** berada di dalam `/home/user`, pastikan izin sudah benar untuk user `postgres`:

```bash
sudo chown postgres:postgres -R /home/user/PGDATA
```

Langkah ini memberikan kepemilikan penuh kepada user `postgres` untuk direktori tersebut.

### 3\. Pastikan Server PostgreSQL Berjalan

Restart server PostgreSQL untuk memastikan layanan berjalan:

```bash
sudo service postgresql restart
```

### 4\. Pertimbangan Lokasi Direktori PGDATA

Jika direktori **PGDATA** ditempatkan di dalam `/home/user` untuk mengelola log file besar, pastikan folder tersebut memiliki izin yang benar sejak awal. Sebaiknya gunakan lokasi yang lebih aman dan terdedikasi untuk database, seperti `/var/lib/postgresql`.

## Catatan Keamanan

* Menggunakan `chmod og+X` pada direktori home meningkatkan risiko keamanan karena direktori menjadi dapat diakses oleh user lain.
    
* Pastikan untuk tidak memberikan izin berlebihan, seperti `chmod 777`, pada direktori sensitif.
    

Dengan mengikuti langkah-langkah di atas, Kamu dapat mengatasi error ini dan memastikan PostgreSQL berjalan dengan baik.