---
title: "Laravel Translations UI: Solusi Mudah untuk Manajemen Terjemahan"
datePublished: Thu Dec 19 2024 04:08:29 GMT+0000 (Coordinated Universal Time)
cuid: cm4usxc6k000209mn9pnwgxjk
slug: laravel-translations-ui-solusi-mudah-untuk-manajemen-terjemahan
canonical: https://github.com/MohmmedAshraf/laravel-translations
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734581273678/6e87c493-8fe4-4b2c-b5c1-d449c7dd6962.png
tags: laravel, laravel-packages

---

#### Apa itu Laravel Translations UI?

**Laravel Translations UI** adalah paket yang dirancang untuk memberikan antarmuka pengguna yang intuitif dalam mengelola terjemahan di aplikasi Laravel. Dengan fitur unggulan seperti menambah, mengedit, menghapus, hingga mengekspor terjemahan, paket ini mempermudah pekerjaan Kamu. Selain itu, integrasi dengan Google Translate API memungkinkan penerjemahan konten ke berbagai bahasa secara otomatis.

---

### 🔑 **Fitur Utama**

* **Pengelolaan Terjemahan yang Mudah:** Tambah, edit, dan hapus terjemahan melalui antarmuka yang ramah pengguna.
    
* **Manajemen Kunci Terjemahan:** Organisasi terjemahan menjadi lebih terstruktur.
    
* **Pencarian Cepat:** Temukan terjemahan berdasarkan kunci atau nilai dengan mudah.
    
* **Import & Export Praktis:** Proses terjemahan antar aplikasi Laravel menjadi lebih sederhana.
    
* **Kolaborasi Mudah:** Undang kontributor untuk bekerja sama dalam mengelola terjemahan.
    
* **Integrasi Google Translate:** Mendukung penerjemahan otomatis yang akurat.
    
* **Ekstra:** Fitur tambahan untuk meningkatkan efisiensi alur kerja Kamu.
    

---

### 🎯 **Roadmap Pengembangan**

* Menambahkan pengujian.
    
* Peningkatan antarmuka pengguna (UI).
    
* Dukungan untuk terjemahan vendor.
    
* Riwayat revisi.
    
* Fitur baru lainnya.
    

---

### 🛠️ **Persyaratan**

* **PHP 8.2+**
    
* **Laravel 11.x**
    

---

### 🚀 **Langkah Instalasi**

#### **Pemberitahuan Penting: Breaking Changes**

Versi terbaru beralih dari **Livewire** ke **Inertia**, membawa peningkatan kinerja dan pengalaman pengguna. Jika Kamu menggunakan versi lama, ikuti langkah-langkah berikut:

1. **Uninstall Versi Lama**  
    Jalankan perintah berikut untuk membersihkan instalasi sebelumnya:
    
    ```bash
    php artisan translations:clean
    ```
    
    Atau hapus secara manual:
    
    ```bash
    composer remove outhebox/laravel-translations
    ```
    
2. **Install Ulang**  
    Instal paket baru dengan perintah:
    
    ```bash
    composer require outhebox/laravel-translations --with-all-dependencies
    ```
    
3. **Publikasi Aset dan File Migrasi**  
    Jalankan:
    
    ```bash
    php artisan translations:install
    ```
    

---

### ⚡ **Penggunaan**

* **Mengimpor Terjemahan**  
    Untuk mengimpor terjemahan:
    
    ```bash
    php artisan translations:import
    ```
    
    Untuk mengimpor ulang semua terjemahan:
    
    ```bash
    php artisan translations:import --fresh
    ```
    
* **Akses Dashboard UI**  
    Kunjungi `/translations` di browser. Di lingkungan produksi, buat pengguna owner terlebih dahulu:
    
    ```bash
    php artisan translations:contributor
    ```
    
* **Ekspor Terjemahan**  
    Ekspor terjemahan dari dashboard atau gunakan:
    
    ```bash
    php artisan translations:export
    ```
    

---

### ⚙️ **Konfigurasi**

Atur file konfigurasi dengan perintah:

```bash
php artisan vendor:publish --tag=translations-config
```

---

### 🔄 **Upgrade**

Saat memperbarui ke versi baru, pastikan untuk memeriksa panduan upgrade dan jalankan:

```bash
php artisan translations:publish
```

Untuk otomatisasi, tambahkan ke `composer.json`:

```json
"scripts": {
    "post-update-cmd": [
        "@php artisan translations:publish --ansi"
    ]
}
}
```

Laravel Translations UI siap meningkatkan produktivitas dan efisiensi dalam pengelolaan terjemahan Kamu!