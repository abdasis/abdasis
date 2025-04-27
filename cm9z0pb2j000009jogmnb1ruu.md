---
title: "Dokumentasi API Laravel Otomatis dengan Scramble"
datePublished: Sun Apr 27 2025 02:15:48 GMT+0000 (Coordinated Universal Time)
cuid: cm9z0pb2j000009jogmnb1ruu
slug: dokumentasi-api-laravel-otomatis-dengan-scramble
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/XN4T2PVUUgk/upload/dcbe88c0bf5de0db401c5e2c02ef8a14.jpeg
tags: laravel

---

## Pengenalan Laravel

Laravel adalah framework aplikasi web dengan sintaks yang ekspresif dan elegan. Laravel menyediakan struktur dan titik awal yang solid untuk membangun aplikasi, lengkap dengan fitur seperti dependency injection, database abstraction layer, antrian pekerjaan, scheduled jobs, serta unit dan integration testing.

## Apa Itu Scramble?

Scramble adalah generator dokumentasi API berbasis OpenAPI (Swagger) untuk Laravel. Dengan Scramble, dokumentasi API proyek Kamu akan dibuat otomatis tanpa perlu menulis anotasi PHPDoc secara manual.

## Instalasi Laravel dan Scramble

### 1. Membuat Proyek Laravel

```bash
composer create-project laravel/laravel laravel_scramble
cd laravel_scramble
```

### 2. Instalasi dan Publish Scramble

```bash
composer require dedoc/scramble
php artisan vendor:publish --provider="Dedoc\Scramble\ScrambleServiceProvider" --tag="scramble-config"
```

Setelah instalasi, dua route otomatis tersedia:

- `/docs/api` — tampilan UI dokumentasi API
- `/docs/api.json` — file OpenAPI dalam format JSON

Secara default, route ini hanya tersedia di environment lokal. Pengaturan ini bisa diubah melalui gate `viewApiDocs` di file `config/scramble.php`.

## Membuat Model, Migration, dan Controller Buku

### 1. Membuat Model dan Controller

```bash
php artisan make:model Book -mc
```

### 2. Struktur Tabel Books

Buka file migrasi di `database/migrations/xxxx_xx_xx_create_books_table.php` dan atur struktur tabel:

```php
public function up(): void
{
    Schema::create('books', function (Blueprint $table) {
        $table->ulid('id')->primary();
        $table->string('title');
        $table->text('description');
        $table->string('author');
        $table->date('publication_date')->nullable();
    });
}
```

Gunakan ULID sebagai primary key agar ID lebih unik dan fleksibel.

Jalankan migrasi:

```bash
php artisan migrate
```

### 3. Controller CRUD untuk Buku

Di `app/Http/Controllers/BookController.php`, tambahkan:

```php
<?php

namespace App\Http\Controllers;

use App\Models\Book;
use Illuminate\Http\Request;
use App\Http\Resources\BookResource;

class BookController extends Controller
{
    public function index()
    {
        $books = Book::paginate(10);
        return response()->json($books);
    }

    public function store(Request $request)
    {
        $data = $request->validate([
            'title' => ['required', 'max:255', 'string'],
            'description' => ['required', 'string'],
            'author' => ['required', 'max:255', 'string'],
            'publication_date' => ['required', 'date'],
        ]);

        $book = Book::create($data);

        return new BookResource($book);
    }

    public function show($id)
    {
        return Book::findOrFail($id);
    }

    public function update(Request $request, $id)
    {
        $data = $request->validate([
            'title' => ['required', 'max:255', 'string'],
            'description' => ['required', 'string'],
            'author' => ['required', 'max:255', 'string'],
            'publication_date' => ['required', 'date'],
        ]);

        $book = Book::findOrFail($id);
        $book->update($data);

        return new BookResource($book);
    }

    public function destroy($id)
    {
        $book = Book::findOrFail($id);
        $book->delete();
        return response()->json(null, 204);
    }
}
```

### 4. Atur Fillable pada Model Book

Di `app/Models/Book.php`, lengkapi seperti ini:

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Support\Str;

class Book extends Model
{
    use HasFactory;

    protected $table = 'books';
    protected $primaryKey = 'id';
    public $incrementing = false;

    protected $fillable = [
        'title',
        'description',
        'author',
        'publication_date',
    ];
}
```

## Menambahkan Route API

Buka `routes/api.php` dan daftarkan route:

```php
<?php

use Illuminate\Support\Facades\Route;
use App\Http\Controllers\BookController;

Route::prefix('v1')->group(function () {
    Route::resource('books', BookController::class);
});
```

Pada contoh ini, sudah diterapkan sistem **versioning API** menggunakan prefix `v1`.

## Melihat Dokumentasi API

Setelah semua langkah selesai, jalankan server Laravel dan buka URL:

```
http://127.0.0.1:8000/docs/api
```

Kamu akan melihat dokumentasi API yang dihasilkan otomatis!

## Kesimpulan

Dengan Scramble, proses pembuatan dokumentasi API di Laravel menjadi:

- **Selalu up-to-date** mengikuti perubahan API
- **Mempermudah** developer lain memahami endpoint yang tersedia
- **Mengurangi beban** dokumentasi manual

Scramble sangat direkomendasikan untuk mempercepat workflow pembuatan API di Laravel.