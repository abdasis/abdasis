# Membuat Routing Sederhana

***

### Routing

Routing adalah mekanisme yang menghubungkan URL permintaan pengguna dengan logika aplikasi yang akan dijalankan. Di Laravel, seluruh rute didefinisikan di dua file utama:

* **routes/web.php**: untuk rute yang diakses melalui browser (antarmuka web).
* **routes/api.php**: untuk rute yang melayani permintaan API (biasanya menghasilkan JSON).

***

### 1. Membuat Rute Dasar

Untuk menetapkan rute sederhana, panggil facade `Route`, tentukan metode HTTP dan jalur URI, lalu berikan fungsi penangan (callback):

```php
use Illuminate\Support\Facades\Route;

Route::get('/kelas', function () {
    return 'Selamat datang di Kelas Laravel';
});
```

Penjelasan:

* `get` menunjuk pada metode HTTP GET.
* `/kelas` adalah path yang diakses.
* Closure mengembalikan teks sebagai respons.

***

### 2. Metode HTTP pada Route

Laravel menyediakan beberapa metode untuk menyesuaikan tindakan terhadap permintaan HTTP:

| Metode | Kegunaan Utama                          | Kode Respons Umum |
| ------ | --------------------------------------- | ----------------- |
| GET    | Mengambil atau menampilkan data         | 200 OK            |
| POST   | Mengirim data baru (misalnya dari form) | 201 Created       |
| PUT    | Mengganti seluruh sumber daya           | 200 OK            |
| PATCH  | Memperbarui sebagian data               | 200 OK            |
| DELETE | Menghapus sumber daya                   | 200 OK            |

Contoh penggunaan metode POST dan DELETE:

```php
Route::post('/artikel', [ArticleController::class, 'store']);
Route::delete('/artikel/{id}', [ArticleController::class, 'destroy']);
```

***

### 3. Parameter pada Route

#### 3.1 Parameter Wajib

Untuk menangkap bagian dinamis dari URL, letakkan nama parameter di dalam kurung kurawal:

```php
Route::get('/siswa/{nis}', function ($nis) {
    return "Data siswa dengan NIS: $nis";
});
```

Akses: `http://localhost:8000/siswa/12345`

#### 3.2 Parameter Opsional

Tambahkan tanda tanya `?` setelah nama parameter dan sediakan nilai default pada fungsi:

```php
Route::get('/siswa/{nama?}', function ($nama = 'Tamu') {
    return "Halo, $nama";
});
```

* Jika tanpa parameter, menampilkan “Halo, Tamu”.
* Jika dengan parameter `http://localhost:8000/siswa/Budi`, menampilkan “Halo, Budi”.

***

### 4. Penamaan Route (Named Routes)

Memberi alias pada rute memudahkan pembuatan link atau pengalihan:

```php
Route::get('/profil', [UserController::class, 'show'])->name('user.profil');
```

Di dalam Blade, panggil rute ini dengan:

```blade
<a href="{{ route('user.profil') }}">Lihat Profil</a>
```

Alias harus unik dalam aplikasi agar tidak bentrok.

***

### 5. Mengelompokkan Route (Route Groups)

Route Groups memungkinkan Kamu menerapkan konfigurasi bersama (middleware, namespace, prefix) ke beberapa rute sekaligus.

#### 5.1 Group dengan Middleware

Tanpa grup, middleware ditulis berulang:

```php
Route::get('/dashboard', [DashboardController::class, 'index'])->middleware('auth');
Route::get('/settings', [SettingsController::class, 'index'])->middleware('auth');
```

Dengan grup:

```php
Route::middleware('auth')->group(function () {
    Route::get('/dashboard', [DashboardController::class, 'index']);
    Route::get('/settings', [SettingsController::class, 'index']);
});
```

#### 5.2 Group dengan Prefix

Prefix menambah awalan pada setiap URI di dalam grup:

```php
Route::prefix('admin')->group(function () {
    Route::get('/dashboard', [AdminController::class, 'dashboard']);
    Route::get('/users', [AdminController::class, 'users']);
});
```

Hasil:

* `/admin/dashboard`
* `/admin/users`

***

### 6. Praktik Terbaik Routing

1. **Gunakan Named Routes** untuk kemudahan referensi.
2. **Pisahkan logika** ke Controller, hindari terlalu banyak kode di closure.
3. **Kelompokkan rute** berdasarkan middleware atau prefix guna menjaga file rute tetap ringkas.
4. **Validasi parameter** jika perlu, dengan regular expression pada definisi route.

***

Setelah memahami routing, langkah berikutnya adalah mempelajari bagaimana request disaring dan diamankan menggunakan middleware.
