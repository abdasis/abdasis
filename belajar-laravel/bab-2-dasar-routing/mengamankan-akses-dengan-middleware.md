# Mengamankan Akses dengan Middleware

### Bab: Mengamankan Akses dengan Middleware

Middleware adalah lapisan pengecekan yang dijalankan sebelum permintaan HTTP mencapai logika aplikasi. Dengan middleware, Kamu dapat menerapkan aturan seperti autentikasi, otorisasi, atau validasi kondisi khusus—misalnya memblokir pengguna yang belum memenuhi syarat usia—sehingga akses ke rute tertentu dapat dikendalikan dengan rapi.

***

#### 1. Membuat Middleware Baru

Untuk menghasilkan kelas middleware di Laravel 12, gunakan perintah Artisan berikut:

```bash
php artisan make:middleware VerifyAge
```

Perintah ini menciptakan file `app/Http/Middleware/VerifyAge.php`. Di dalamnya terdapat metode `handle(Request $request, Closure $next)` yang menjadi tempat menuliskan logika penyaringan permintaan.

```php
namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;

class VerifyAge
{
    public function handle(Request $request, Closure $next)
    {
        // logika akan ditambahkan di sini
        return $next($request);
    }
}
```

***

#### 2. Menambahkan Logika pada Middleware

Misalkan Kamu ingin memastikan hanya pengguna berumur minimal 21 tahun yang boleh mengakses rute tertentu. Ubah metode `handle` menjadi:

```php
public function handle(Request $request, Closure $next)
{
    if ($request->user_age < 21) {
        return redirect()->route('home')
                         ->with('error', 'Usia minimal 21 tahun diperlukan');
    }

    return $next($request);
}
```

Di sini `$request->user_age` mewakili data usia yang dikirim lewat request—bisa dari form, header, atau session.

***

#### 3. Mendaftarkan Middleware di Laravel 12

Semua konfigurasi middleware sekarang berada di file `bootstrap/app.php`. Untuk mendaftarkan middleware sebagai alias rute, tambahkan di dalam closure `withMiddleware`:

```php
use App\Http\Middleware\VerifyAge;

->withMiddleware(function ($middleware) {
    $middleware->alias([
        'verify.age' => VerifyAge::class,
    ]);
})
```

***

#### 4. Mengaitkan Middleware dengan Rute

Setelah alias tercipta, Kamu bisa melindungi rute dengan memanggil alias tersebut:

```php
Route::get('/member-area', [MemberController::class, 'index'])
     ->middleware('verify.age');
```

Hanya request yang lolos pengecekan usia di `VerifyAge` yang akan diteruskan ke `MemberController@index`.

***

#### 5. Middleware dengan Parameter Dinamis

Untuk skenario otorisasi berbasis peran (role), middleware dapat menerima argumen tambahan:

```php
public function handle(Request $request, Closure $next, $role)
{
    if (! $request->user()->hasRole($role)) {
        return redirect()->route('home')
                         ->with('error', 'Akses terbatas untuk role: '.$role);
    }

    return $next($request);
}
```

Penerapannya di rute:

```php
Route::get('/admin/dashboard', [AdminController::class, 'dashboard'])
     ->middleware('verify.role:admin');
```

***

#### 6. Middleware Global vs Rute Spesifik

*   **Global Middleware**: dijalankan pada setiap permintaan. Daftarkan dengan `append` atau `prepend` pada `withMiddleware` tanpa alias:

    ```php
    ->withMiddleware(function ($middleware) {
        $middleware->append(\App\Http\Middleware\LogRequest::class);
    })
    ```
* **Route Middleware**: hanya diaplikasikan pada rute atau grup yang ditentukan via `->middleware('alias')`.

***

#### 7. Praktik Terbaik

1. **Kelompokkan rute** yang memerlukan middleware sama menggunakan `Route::middleware()->group(...)`.
2. **Letakkan logika berat** di service atau policy, bukan langsung di middleware.
3. **Gunakan named middleware** untuk kemudahan pembacaan kode.
4. **Beri penamaan alias** yang deskriptif, misalnya `auth.user`, `throttle.api`, atau `verify.age`.

Dengan memahami dan menerapkan middleware secara tepat di Laravel 12, Kamu dapat menjaga keamanan dan konsistensi alur aplikasi sekaligus memisahkan tanggung jawab pengecekan dari logika bisnis utama.
