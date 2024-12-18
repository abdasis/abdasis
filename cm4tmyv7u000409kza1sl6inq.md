---
title: "Lazy Objects di PHP 8.4: Era Baru Pengelolaan Objek yang Efisien"
datePublished: Wed Dec 18 2024 08:33:56 GMT+0000 (Coordinated Universal Time)
cuid: cm4tmyv7u000409kza1sl6inq
slug: lazy-objects-di-php-84-era-baru-pengelolaan-objek-yang-efisien
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1734510823661/c4e2124a-d0a4-4e26-9667-4b5947c0362a.jpeg
tags: laravel, php

---

PHP 8.4 memperkenalkan **lazy objects**, fitur inovatif yang memungkinkan inisialisasi objek ditunda hingga objek tersebut benar-benar diakses. Pendekatan ini mengoptimalkan penggunaan sumber daya, terutama untuk objek dengan logika inisialisasi berat yang mungkin jarang digunakan.

---

## Apa Perbedaan Objek Biasa dan Lazy Object?

Lazy objects menggunakan **proxy object** yang dibuat secara dinamis untuk menunda eksekusi konstruktor objek target. Dengan memanfaatkan **Reflection**, proxy ini meniru kelas asli sehingga objek sebenarnya tetap tidak diinisialisasi hingga dibutuhkan.

### Contoh Objek Biasa

```php
<?php

class MyClass
{
    public function __construct(private int $foo)
    {
        echo 'Akses metode memicu inisialisasi'.PHP_EOL;
    }

    public function getFoo(): int
    {
        return $this->foo;
    }
}

$object = new MyClass(1);

echo 'Objek dibuat'.PHP_EOL;
echo 'Memanggil metode: ' . $object->getFoo(). PHP_EOL;
```

**Output:**

```plaintext
Akses metode memicu inisialisasi
Objek dibuat
Memanggil metode: 1
```

Pada contoh ini, konstruktor dipanggil segera setelah objek dibuat, menghasilkan inisialisasi properti `$foo`.

---

### Contoh Lazy Object

```php
<?php

class MyClass
{
    public function __construct(private int $foo)
    {
        echo 'Akses metode memicu inisialisasi'.PHP_EOL;
    }

    public function getFoo(): int
    {
        return $this->foo;
    }
}

$initializer = static function (MyClass $ghost): void {
    $ghost->__construct(123);
};

$reflector = new ReflectionClass(MyClass::class);
$object = $reflector->newLazyGhost($initializer);

echo 'Lazy object dibuat'.PHP_EOL;
echo 'Memanggil metode: ' . $object->getFoo(). PHP_EOL;
```

**Output:**

```plaintext
Lazy object dibuat
Akses metode memicu inisialisasi
Memanggil metode: 123
```

Pada contoh ini, metode `newLazyGhost` membuat lazy object. Konstruktor baru dipanggil hanya ketika metode `getFoo()` diakses, sehingga objek tetap tidak diinisialisasi hingga benar-benar dibutuhkan.

---

## Keuntungan Lazy Objects

### 1\. **Peningkatan Performa**

Inisialisasi yang ditunda mengurangi penggunaan memori dan meningkatkan performa, terutama untuk objek yang hanya digunakan dalam kondisi tertentu.

### 2\. **Proxy Transparan**

Pengembang dapat menggunakan lazy objects seperti objek biasa tanpa perlu penyesuaian khusus.

### 3\. **Manajemen Sumber Daya yang Optimal**

Bermanfaat dalam konteks seperti dependency injection, ORM, atau integrasi API, di mana inisialisasi bisa ditunda hingga benar-benar diperlukan.

---

## Keterbatasan

1. **Serialization** Lazy objects bisa menyulitkan proses serialisasi karena statusnya yang belum diinisialisasi.
    
2. **Debugging yang Lebih Rumit** Proxy object dapat memperpanjang stack trace, membuat proses debugging lebih kompleks.
    

---

## Kesimpulan

Lazy objects di PHP 8.4 menawarkan cara yang efisien untuk meningkatkan performa dan pengelolaan sumber daya pada aplikasi modern. Dengan menunda inisialisasi hingga diperlukan, fitur ini memberikan pendekatan yang lebih bersih dan skalabel untuk mengelola siklus hidup objek yang kompleks.

**Apakah Kamu siap mengintegrasikan lazy objects dalam proyekmu?**