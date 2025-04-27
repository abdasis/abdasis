---
title: "Best Practice Enum di PHP 8."
datePublished: Sun Apr 27 2025 07:12:51 GMT+0000 (Coordinated Universal Time)
cuid: cm9zbbbup000009kz3ev38ezw
slug: best-practice-enum-di-php-8
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1745737948566/d66a775a-1431-4d5b-bf59-6bd2983c1d87.webp
tags: php

---


## Apa Itu Enum di PHP?

Enum adalah fitur yang semakin populer di PHP, diperkenalkan sejak versi 8.1. Dengan enum, kita bisa membatasi nilai ke satu set yang telah ditentukan, menjadikannya alat yang sangat berguna untuk menulis kode yang lebih bersih dan lebih terstruktur. Dengan kemampuan untuk berfungsi seperti objek, enum di PHP memberikan berbagai keuntungan, seperti penggunaan trait, implementasi interface, dan bahkan memiliki method.

Berikut adalah contoh penggunaan enum di PHP:

```php
trait X {}

interface StatusInterface {}

enum Status implements StatusInterface
{
    use X;

    case ACTIVE;
    case INACTIVE;
    case PENDING;
}
```

Pada artikel ini, kita akan membahas praktik terbaik dalam menggunakan enum di PHP, serta mengapa enum jauh lebih baik daripada konstanta biasa.

## Pure Enum vs Backed Enum

Ada dua jenis enum yang perlu diperhatikan di PHP: **Pure Enum** dan **Backed Enum**.

- **Pure Enum** hanya mendeklarasikan case tanpa memberikan nilai:

```php
enum Status
{
    case ACTIVE;
    case INACTIVE;
    case PENDING;
}
```

- **Backed Enum** memberikan nilai yang mendasari setiap case:

```php
enum Status: string
{
    case ACTIVE = "active";
    case INACTIVE = "inactive";
    case PENDING = "pending";
}
```

Penting untuk dicatat bahwa kita tidak dapat mencampur pure dan backed enum dalam satu enum.

## Membandingkan Enum di PHP

Salah satu keuntungan besar dari enum adalah kemampuan untuk membandingkan mereka dengan lebih mudah. Sebelumnya, kita harus membuat objek dan membandingkan mereka menggunakan `===`, yang akan selalu mengembalikan `false` jika objeknya berbeda. Dengan enum, perbandingan menjadi sangat langsung:

```php
enum Status: string
{
    case ACTIVE = "active";
    case INACTIVE = "inactive";
    case PENDING = "pending";
}

$c = Status::ACTIVE;
$d = Status::ACTIVE;
var_dump($c === $d); // true
```

Perbandingan ini akan mengembalikan `true` jika kedua nilai enum tersebut sama, sebuah peningkatan besar dibandingkan dengan pendekatan lama.

## Sebelum PHP 8.1: Menyimulasi Enum

Sebelum enum resmi diperkenalkan, banyak pengembang menggunakan konstanta dalam interface untuk meniru perilaku enum. Berikut adalah contoh cara lama dalam meniru enum:

```php
interface EnumInterface
{
    public const ACTIVE = 'active';
    public const INACTIVE = 'inactive';
    public const PENDING = 'pending';
}

class MyEnum implements EnumInterface
{
    private string $value;

    public function __construct(string $value)
    {
        $this->value = $value;
    }
}
```

Meskipun kode ini valid, ia memiliki kelemahan. Misalnya, kita bisa saja mengirimkan nilai yang tidak valid tanpa peringatan atau pengecekan.

## Best Practices untuk Enum di PHP

Berikut adalah beberapa praktik terbaik yang harus kamu pertimbangkan saat bekerja dengan enum di PHP:

### 1. Hindari Menggunakan Backed Enum Terlalu Banyak

Penggunaan backed enum yang berlebihan bisa membawa kita kembali ke pendekatan menggunakan konstanta. Jika kamu perlu menggunakan backed enum, pertimbangkan untuk menggunakan metode kecil untuk menerjemahkan nilai atau menulis layanan eksplisit untuk menangani hal ini.

### 2. Jangan Bandingkan Enum dengan Nilai Skalar

Jika kamu menggunakan backed enum, hindari membandingkan nilai enum dengan nilai skalar. Sebaiknya, buat enum lain yang sesuai dengan nilai tersebut dan bandingkan kedua enum tersebut.

### 3. Jangan Memasukkan Logika Bisnis ke dalam Enum

Enum seharusnya tidak digunakan untuk menyimpan logika bisnis. Hindari menambah terlalu banyak metode dalam enum. Enum hanya bertujuan untuk mendeskripsikan nilai, bukan untuk menangani logika yang rumit. Jika perlu, gunakan metode sederhana seperti `match` atau `transform`.

### 4. Jangan Gunakan Nilai Enum dalam Logika Bisnis

Nilai dalam backed enum sebaiknya hanya digunakan untuk membuat enum dari nilai tersebut. Menggunakan nilai tersebut langsung dalam logika aplikasi dapat membuat kode tergantung pada nilai tertentu, yang bisa memperburuk pemeliharaan aplikasi dalam jangka panjang.

### 5. Migrasi dari Simulasi Enum ke Enum Sebenarnya

Saat memigrasi dari konstanta yang mensimulasikan enum ke enum asli, perhatikan dengan seksama. Meskipun sebagian besar kasus dapat digantikan, beberapa mungkin memerlukan penanganan khusus, terutama jika enum tersebut digunakan secara luas dalam logika aplikasi.

## Kesimpulan

Enum di PHP menawarkan cara yang jauh lebih elegan dan aman untuk menangani nilai-nilai tetap daripada menggunakan konstanta biasa. Dengan pemahaman yang tepat tentang kapan dan bagaimana menggunakan enum, kamu bisa menulis kode yang lebih bersih dan lebih terstruktur. Namun, seperti halnya setiap fitur baru, penting untuk memahami kapan menggunakan enum dan kapan menghindarinya agar tidak menambah kompleksitas yang tidak perlu dalam aplikasi.

Apakah kamu sudah mulai menggunakan enum dalam proyek PHP-mu? Atau, apakah ada aspek lain dari enum yang ingin kamu ketahui lebih lanjut? Jangan ragu untuk berbagi pendapat dan pengalamanmu di kolom komentar!