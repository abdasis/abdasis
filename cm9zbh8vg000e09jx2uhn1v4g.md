---
title: "Traits di PHP 8.3: Fitur Baru, Tapi Masih Buruk"
datePublished: Sun Apr 27 2025 07:17:27 GMT+0000 (Coordinated Universal Time)
cuid: cm9zbh8vg000e09jx2uhn1v4g
slug: traits-di-php-83-fitur-baru-tapi-masih-buruk
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1745738208533/55ae645a-7b4e-4e62-88bd-494c6b353626.webp
tags: php

---

## Apa Itu Traits di PHP?

Traits di PHP itu fitur yang diciptakan buat mengatasi masalah pewarisan tunggal (single inheritance). Jadi, kita bisa masukin kode yang sama ke beberapa kelas tanpa harus bikin hirarki kelas yang ribet. Tapi, meskipun kelihatannya solusi yang oke, kenyataannya traits sering bikin kode jadi lebih susah dipelihara dan malah nambahin masalah desain. Meskipun PHP terus berkembang, traits masih jadi topik yang kontroversial.

Nah, di PHP 8.3, ada beberapa perubahan di fitur traits ini. Apa yang berubah? Apakah makin oke atau malah makin parah? Mari kita bahas.

## Apa yang Baru di Traits PHP 8.3?

Beberapa perubahan terbaru yang masuk ke traits di PHP:

* **PHP 8.0**: Sekarang kita bisa mendefinisikan metode abstrak dalam traits.
    
* **PHP 8.2**: Traits sekarang bisa punya konstanta.
    
* **PHP 8.3**: Ada perubahan di cara trait dan kelas induk ngelola properti statis.
    

Tapi, meskipun ada fitur baru, menurut aku justru makin memperburuk keadaan. Yuk, kita coba lihat kenapa.

### Dampak dari Perubahan di PHP 8.3

Beberapa perubahan yang dihadirkan malah bikin masalah yang ada sebelumnya makin berat. Dalam konteks prinsip desain seperti SOLID, dua dari tiga fitur baru ini malah bertentangan. Abstraksi di metode atau kelas yang dibuat oleh traits itu sebenernya mempertegas ketergantungan pada pewarisan. Selain itu, penggunaan properti statis di traits juga sering jadi sumber masalah yang bisa bikin kode kita susah di-maintain, susah diprediksi, dan susah diubah.

## Kenapa Traits Itu Buruk?

Berikut beberapa alasan kenapa traits bukan solusi terbaik, bahkan setelah PHP 8.3:

### 1\. Pelanggaran Prinsip Tanggung Jawab Tunggal (SRP)

Ketika kita pakai banyak traits dalam sebuah kelas, kelas tersebut bisa jadi punya banyak tanggung jawab, yang akhirnya melanggar prinsip **Single Responsibility Principle (SRP)**. Bayangin aja, semakin banyak traits yang dimasukin ke dalam kelas, semakin besar kemungkinan kelas itu ngelakuin banyak hal, yang bikin kode jadi berantakan dan susah dipahami.

### 2\. Desain Arsitektur yang Amburadul

Traits sering dipakai sebagai solusi instan untuk nambahin fitur ke kelas tanpa mikirin dampaknya ke desain keseluruhan. Hasilnya? Kode jadi kayak "patchwork", nggak terstruktur dengan baik, dan susah untuk di-maintain atau dikembangkan lagi. Gimana mau paham hubungan antar kelas kalau semua berantakan gitu?

### 3\. Ketergantungan yang Nggak Terlihat

Traits bisa bikin hubungan antar kelas jadi nggak jelas. Kita bisa aja nyambungin banyak traits ke dalam satu kelas, tapi akhirnya bikin ketergantungan yang susah dipetakan. Ini bikin kode jadi lebih rumit dan susah dimengerti, apalagi kalau lagi debugging.

### 4\. Susah untuk Diuji

Traits nggak bisa diinstansiasi langsung, jadi susah banget buat di-test. Kode yang pake traits itu sering kali butuh pengujian unit, tapi karena traits nggak bisa diuji sendiri, akhirnya pengujian jadi lebih sulit dan rumit.

## Alternatif yang Lebih Baik: Dependency Injection

Dibandingkan pake traits, lebih baik pakai **Dependency Injection (DI)**. Dengan DI, kita bisa ngatur dependensi di satu tempat (biasanya di “composition root”), jadi nggak perlu nambahin banyak traits ke kelas. Ini bikin kode lebih fleksibel dan lebih mudah diubah.

Contohnya, di proyek Keestash, aku pake arsitektur berbasis DI dan itu terbukti lebih efektif. Setiap layanan yang kita pakai diinject lewat interface, bukan lewat traits. Jadi, meskipun ada perubahan di satu bagian, nggak akan merusak bagian lain dalam aplikasi.

## Kesimpulan: Hindari Traits untuk Kode yang Lebih Bersih

Meskipun PHP 8.3 bawa beberapa pembaruan di traits, kenyataannya traits tetap bukan solusi terbaik buat desain kode dalam jangka panjang. Untuk sistem yang lebih scalable, fleksibel, dan mudah diprediksi, Dependency Injection (DI) jelas lebih unggul. DI bikin kode kita lebih terstruktur dan mudah diuji.

Jadi, kalau masih pakai traits di proyek kamu, coba deh pikirin lagi. Mungkin saatnya beralih ke Dependency Injection. Lebih enak, lebih bersih, dan lebih mudah dipelihara.

Gimana, udah siap ngeluarin traits dari proyek kamu? Let me know!