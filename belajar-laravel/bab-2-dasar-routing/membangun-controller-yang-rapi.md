# Membangun Controller yang Rapi

***

### Mengenal Route di Laravel

Route adalah gerbang utama aplikasi Kamu. Setiap kali user membuka URL tertentu, Laravel akan mencocokkannya dengan route yang sudah ditentukan, lalu menjalankan fungsinya.

```php
Route::get('/', function () {
    return 'Selamat datang di Laravel!';
});
```

Kamu bisa menggunakan berbagai method HTTP seperti `GET`, `POST`, `PUT`, `DELETE`, dan lainnya.

***

### Jenis-Jenis Route

#### Route Dasar

```php
Route::get('/home', function () {
    return view('home');
});
```

#### Route dengan Parameter

```php
Route::get('/user/{id}', function ($id) {
    return "User ID: $id";
});
```

#### Route dengan Parameter Opsional

```php
Route::get('/kategori/{slug?}', function ($slug = 'umum') {
    return "Kategori: $slug";
});
```

***

### Membuat Controller

Untuk membuat controller baru, gunakan perintah artisan berikut:

```bash
php artisan make:controller ArticleController
```

Perintah ini akan membuat file `ArticleController.php` di folder `app/Http/Controllers`.

#### Contoh Controller

```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class ArticleController extends Controller
{
    public function index()
    {
        return view('articles.index');
    }

    public function show($id)
    {
        return "Menampilkan artikel dengan ID: $id";
    }
}
```

***

### Menghubungkan Route ke Controller

Setelah controller dibuat, Kamu bisa menghubungkannya ke route seperti ini:

```php
use App\Http\Controllers\ArticleController;

Route::get('/articles', [ArticleController::class, 'index']);
Route::get('/articles/{id}', [ArticleController::class, 'show']);
```

***

### Resource Controller

Laravel menyediakan cara cepat untuk membuat seluruh route CRUD dengan satu baris:

```bash
php artisan make:controller PostController --resource
```

Lalu daftarkan route-nya:

```php
Route::resource('posts', PostController::class);
```

Laravel akan otomatis membuat route untuk method seperti:

* `index`
* `create`
* `store`
* `show`
* `edit`
* `update`
* `destroy`

***

### Route Group

#### Group dengan Prefix

```php
Route::prefix('admin')->group(function () {
    Route::get('/dashboard', [AdminController::class, 'index']);
});
```

#### Group dengan Middleware

```php
Route::middleware(['auth'])->group(function () {
    Route::get('/profile', [UserController::class, 'profile']);
});
```

***

### Memberi Nama pada Route

Agar mudah digunakan, Kamu bisa memberi nama pada route:

```php
Route::get('/login', [AuthController::class, 'showLogin'])->name('login');
```

Penggunaannya:

```php
return redirect()->route('login');
```

***

### Kesimpulan

Dengan menggunakan route dan controller, Kamu bisa membangun struktur aplikasi yang rapi dan terorganisir. Gunakan `make:controller` untuk mempercepat pekerjaan, dan manfaatkan fitur seperti resource controller serta route grouping agar aplikasi Laravel Kamu semakin efisien.
