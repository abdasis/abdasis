---
title: "Laravel Cheat Sheet: Tips for Building Secure Applications"
datePublished: Tue Dec 17 2024 09:44:39 GMT+0000 (Coordinated Universal Time)
cuid: cm4sa1xuk000o08johhlocg9q
slug: laravel-cheat-sheet-tips-for-building-secure-applications
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/ccUpnIOk-B0/upload/4d88ecf18e85d451dc038f77b7195539.jpeg
tags: laravel, php

---

## **Pengantar**

Laravel adalah framework yang sudah dilengkapi fitur keamanan bawaan. Namun, fleksibilitasnya memungkinkan pengembang membuat implementasi yang lebih kompleks, yang dapat memunculkan celah keamanan jika tidak hati-hati. Panduan ini dirancang untuk membantu Kamu menghindari kesalahan umum dan memastikan aplikasi Laravel tetap aman.

---

## **Dasar-Dasar Keamanan Laravel**

1. **Nonaktifkan Debug Mode di Produksi**  
    Atur variabel lingkungan `APP_DEBUG` menjadi `false`:
    
    ```typescript
    APP_DEBUG=false
    ```
    
2. **Pastikan Application Key Telah Digenerate**  
    Gunakan perintah berikut:
    
    ```bash
    php artisan key:generate
    ```
    
3. **Atur Konfigurasi PHP yang Aman**  
    Rujuk ke PHP Configuration Cheat Sheet untuk pengaturan PHP yang aman.
    
4. **Setel Izin File dan Direktori**
    
    * Direktori: Maksimal `775`
        
    * File non-eksekusi: Maksimal `664`
        
    * File eksekusi (seperti Artisan): Maksimal `775`
        
5. **Periksa Ketergantungan yang Rentan**  
    Gunakan *Enlightn Security Checker* untuk memverifikasi keamanan dependensi.
    

---

## **Keamanan Cookie dan Manajemen Session**

1. **Aktifkan Middleware EncryptCookies**  
    Tambahkan middleware berikut di `App\Http\Kernel`:
    
    ```php
    protected $middlewareGroups = [
        'web' => [
            \App\Http\Middleware\EncryptCookies::class,
            ...
        ],
    ];
    ```
    
2. **Setel HttpOnly untuk Session Cookie**
    
    ```php
    'http_only' => true,
    ```
    
3. **Konfigurasi Cookie Domain**  
    Jika tidak menggunakan subdomain:
    
    ```php
    'domain' => null,
    ```
    
4. **Set SameSite Cookie**  
    Pilih antara `lax` atau `strict`:
    
    ```php
    'same_site' => 'lax',
    ```
    
5. **Aktifkan Secure Cookie untuk HTTPS**
    
    ```php
    'secure' => true,
    ```
    
6. **Setel Timeout Session Rendah**  
    Rekomendasi: 15-30 menit.
    
    ```php
    'lifetime' => 15,
    ```
    

---

## **Autentikasi**

### **Guards dan Providers**

* Laravel memiliki *guards* untuk autentikasi dan *providers* untuk mengambil data pengguna.
    
* Konfigurasi ada di file `config/auth.php`.
    

### **Starter Kits**

* **Laravel Breeze**: Autentikasi dasar.
    
* **Laravel Fortify**: *Headless authentication backend*.
    
* **Laravel Jetstream**: Starter kit lengkap dengan UI.
    

### **API Authentication**

* **Passport**: *OAuth2 authentication provider*.
    
* **Sanctum**: *API token authentication provider*.
    

---

## **Mass Assignment**

Hindari kerentanan dengan:

1. Menggunakan `$request->only()` atau `$request->validated()` alih-alih `$request->all()`.
    
2. Tidak mengosongkan `$guarded` pada model.
    
3. Menghindari penggunaan `forceFill` kecuali data sudah divalidasi.
    

---

## **SQL Injection**

### **Proteksi Eloquent ORM**

Laravel melindungi SQL injection secara bawaan dengan parameterisasi query:

```php
User::where('email', $email)->get();
```

### **Raw Query**

Gunakan *binding* untuk data yang tidak terpercaya:

```php
User::whereRaw('email = ?', [$request->input('email')])->get();
```

### **Validasi Kolom**

Hindari input pengguna menentukan nama kolom. Validasi input:

```php
$request->validate(['sortBy' => 'in:price,updated_at']);
```

---

## **Cross Site Scripting (XSS)**

* Gunakan `{{ }}` untuk output aman.
    
* Hindari `{!! !!}` pada data yang tidak terpercaya.
    

---

## **File Upload yang Aman**

1. **Validasi Jenis dan Ukuran File**
    
    ```php
    $request->validate([
        'photo' => 'file|size:100|mimes:jpg,bmp,png'
    ]);
    ```
    
2. **Hindari Nama File dari Input Pengguna**  
    Tetapkan nama file secara manual:
    
    ```php
    $filename = Str::random(10) . '.' . $request->file('photo')->extension();
    ```
    

---

Dengan mengikuti tips ini, Kamu dapat membangun aplikasi Laravel yang lebih aman dan terhindar dari kerentanan umum.