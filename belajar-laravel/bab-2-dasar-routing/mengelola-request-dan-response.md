# Mengelola Request dan Response

***

### Memahami Objek Request

Laravel menyediakan objek `Illuminate\Http\Request` untuk menangani data masuk dari klien—mulai dari isian form, parameter URL, file, hingga cookie. Dengan objek ini, Kamu bisa mengakses berbagai jenis input secara terstruktur.

```php
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class CustomerController extends Controller
{
    public function save(Request $req)
    {
        $fullName = $req->input('fullname');
        // proses selanjutnya...
    }
}
```

* `Request $req` di-method memastikan Kamu dapat memanggil metode pengambil data.
* `$req->input('fullname')` mengambil nilai field `fullname` dari form.

***

### Metode Umum pada Request

| Metode                  | Keterangan                                             |
| ----------------------- | ------------------------------------------------------ |
| `$req->all()`           | Mengambil seluruh data input, query string, dan file   |
| `$req->input('key')`    | Mengambil satu nilai berdasarkan nama field            |
| `$req->query('q')`      | Mengakses parameter pada URL seperti `?q=laravel`      |
| `$req->only([...])`     | Mengambil subset data sesuai daftar field yang diminta |
| `$req->except([...])`   | Mengambil semua kecuali field tertentu                 |
| `$req->file('avatar')`  | Mengambil file upload bernama `avatar`                 |
| `$req->cookie('token')` | Membaca cookie bernama `token`                         |

***

### Menyiapkan Data untuk Simpan

Contoh menyimpan data artikel:

```php
public function store(Request $req)
{
    $data = $req->only(['title', 'content']);
    Article::create($data);
    return redirect()->route('articles.index');
}
```

* Gunakan `$req->only` untuk meminimalkan mass assignment.
* Setelah penyimpanan, redirect ke daftar artikel.

***

### Membentuk Response

Setiap rute atau controller harus mengembalikan respons. Laravel menawarkan beberapa tipe respons:

#### 1. Teks atau View

```php
Route::get('/', function () {
    return view('welcome');
});
```

Atau sekadar teks:

```php
Route::get('/ping', function () {
    return 'pong';
});
```

#### 2. Pengalihan (Redirect)

Redirect ke rute bernama atau URL:

```php
return redirect()->route('home');
```

Kembali ke halaman sebelumnya, misalnya setelah validasi gagal:

```php
return back()->withErrors(['email' => 'Email tidak valid'])->withInput();
```

#### 3. JSON

Cocok untuk API:

```php
return response()->json([
    'status' => 'success',
    'data'   => $user
]);
```

Header `Content-Type: application/json` otomatis ditetapkan.

#### 4. Unduhan File

Memaksa browser mengunduh berkas:

```php
$file = storage_path('exports/report.pdf');
return response()->download($file, 'laporan.pdf');
```

***

### Ringkasan Alur Request–Response

1. **Request** masuk ke aplikasi →
2. **Route** menentukan handler (closure atau controller) →
3. **Controller** menggunakan `$request` untuk mengambil data →
4. **Controller** memproses data dan mengembalikan **Response** berupa view, redirect, JSON, atau download.

Dengan pemahaman ini, Kamu siap menyajikan fungsionalitas aplikasi yang interaktif dan terstruktur. Selanjutnya, kita akan mempelajari cara menata logika di Controller agar kode tetap bersih dan terpisah dengan baik.
