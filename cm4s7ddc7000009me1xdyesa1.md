---
title: "Cara Backup Database Laravel Secara Otomatis di cPanel Shared Hosting dan VPS"
datePublished: Tue Dec 17 2024 08:29:33 GMT+0000 (Coordinated Universal Time)
cuid: cm4s7ddc7000009me1xdyesa1
slug: cara-backup-database-laravel-secara-otomatis-di-cpanel-shared-hosting-dan-vps
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/iqELIpzpARI/upload/82d6a3f92beac1b7f1b3f42653524735.jpeg
tags: laravel, php

---

Melakukan backup data adalah salah satu tugas paling penting dalam menjaga web aplikasi. Backup database secara rutin adalah keharusan, namun melakukannya secara manual setiap hari terasa membosankan dan sering kali diabaikan oleh developer atau pemilik aplikasi. Jika Kamu mencari panduan langkah demi langkah untuk membuat backup database otomatis setiap hari, artikel ini akan menjelaskan caranya menggunakan cPanel shared hosting atau VPS.

## Jadwal Backup Database Laravel

Untuk membuat backup database Laravel secara otomatis, ada tiga langkah utama yang harus dilakukan:

1. **Install Laravel DB Backup Package**
    
2. **Atur Jadwal Backup di Laravel**
    
3. **Konfigurasi Jadwal di Server**
    

### 1\. Install Laravel DB Backup Package

Langkah pertama adalah menginstal package **haruncpi/laravel-db-backup** menggunakan perintah Composer berikut:

```bash
composer require haruncpi/laravel-db-backup
```

#### Lokasi Penyimpanan Backup

* **Local Disk**: `storage/app/backups`
    
* **S3 Bucket**: `backups`
    

Jika Kamu menggunakan S3, pastikan sudah mengonfigurasinya sebelum melanjutkan.

---

### 2\. Atur Jadwal Backup di Laravel

Setelah package terinstal, langkah selanjutnya adalah mengatur jadwal backup di sisi aplikasi Laravel. Buka file `app/Console/Kernel.php`, lalu tambahkan kode berikut di dalam metode `schedule`:

```php
protected function schedule(Schedule $schedule)
{
    $schedule->command('db:backup')->twiceDaily(0, 12);
}
```

#### Catatan Penting:

* **Metode** `twiceDaily` secara default dijalankan pada pukul 01:00 dan 13:00.
    
* Agar sesuai dengan waktu server atau cronjob di cPanel/VPS, Kamu perlu mengaturnya menjadi pukul 00:00 dan 12:00 (0,12).
    

#### Backup ke AWS S3

Jika ingin menyimpan backup di AWS S3, tambahkan `s3` pada perintah Artisan. Berikut contoh kode lengkapnya:

```php
protected function schedule(Schedule $schedule)
{
    $schedule->command('db:backup s3')->twiceDaily(0, 12);
}
```

#### Metode Alternatif:

Kamu juga bisa menggunakan metode `daily` untuk backup harian atau metode jadwal lain yang tersedia di Laravel Scheduler. Pastikan waktu jadwal aplikasi Kamu dan jadwal server sudah sinkron agar proses berjalan dengan lancar.

---

### 3\. Konfigurasi Jadwal di Server

Setelah mengatur jadwal di Laravel, langkah terakhir adalah mengatur jadwal di sisi server, baik di cPanel shared hosting maupun VPS.

#### **cPanel Shared Hosting**

Pada cPanel, Kamu perlu menggunakan **cronjob** untuk menjalankan jadwal Laravel. Berikut langkah-langkahnya:

1. Login ke cPanel.
    
2. Pilih menu **Cron Jobs**.
    
3. Tambahkan cronjob dengan perintah berikut:
    
    ```bash
    /usr/local/bin/php /home/jhonsmith/public_html/artisan schedule:run >> /dev/null 2>&1
    ```
    
    **Catatan**:
    
    * Ganti `jhonsmith` dengan username cPanel milik Kamu.
        
    * Perintah ini akan menjalankan scheduler Laravel setiap menit.
        

#### **VPS Hosting**

Jika menggunakan VPS, Kamu harus menentukan lokasi pasti dari file PHP dan Artisan. Contoh perintahnya adalah:

```bash
/usr/local/php72/bin/php site.com/artisan schedule:run >> /dev/null 2>&1
```

Jika ingin menjalankan perintah dari root direktori aplikasi, gunakan perintah berikut:

```bash
cd ~/site.com && /usr/local/php72/bin/php artisan schedule:run >> /dev/null 2>&1
```

---

## Kesimpulan

Dengan mengikuti langkah-langkah di atas, Kamu dapat dengan mudah mengatur backup database Laravel secara otomatis di cPanel shared hosting maupun VPS. Hal ini akan sangat membantu mengamankan data aplikasi tanpa perlu melakukannya secara manual setiap hari. Jangan lupa untuk memastikan konfigurasi waktu server dan aplikasi Kamu sudah sesuai.

Bagikan artikel ini kepada orang lain jika Kamu merasa informasi ini bermanfaat!