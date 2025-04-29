# B.3 Routing Static Assets di Golang

### B.3.1 Struktur Aplikasi

Sebelum masuk ke coding, yuk susun dulu folder dan file yang diperlukan:

```
/project
    /assets
        site.css
        script.js
    main.go
```

Folder `assets` dipakai untuk menaruh file-file statis seperti gambar, CSS, atau JavaScript.

***

### B.3.2 Membuat Routing untuk Static Assets

Sekarang, Kamu tulis kode berikut di `main.go`:

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	http.Handle("/static/",
		http.StripPrefix("/static/",
			http.FileServer(http.Dir("assets"))))

	fmt.Println("server started at localhost:9000")
	http.ListenAndServe(":9000", nil)
}
```

***

### B.3.3 Penjelasan Kode

**1. Routing dengan `http.Handle()`**

Berbeda dengan `http.HandleFunc()`, di sini Kamu pakai `http.Handle()` untuk menentukan rute.

**2. Fungsi `http.FileServer()`**

`http.FileServer()` bertugas melayani file yang ada di folder `assets`.

**3. Fungsi `http.StripPrefix()`**

`http.StripPrefix("/static/", ...)` dipakai supaya URL yang diakses pengguna cocok dengan struktur folder.

Kalau tidak pakai `StripPrefix`, server bakal salah cari file, dan file tidak akan ketemu.

***

### B.3.4 Cara Kerja Routing Static

Saat browser mengakses:

* `http://localhost:9000/static/site.css`

Server akan hapus `/static/`, lalu cari file `assets/site.css`.

Kalau tidak pakai `http.StripPrefix()`, server akan cari file di `assets/static/site.css`, dan pasti gagal.

Makanya, penggunaan `http.StripPrefix()` wajib banget untuk static assets.

***

## B.4 Perbedaan http.HandleFunc dan http.Handle

### B.4.1 Fungsi `http.HandleFunc`

Kalau Kamu mau buat handler untuk menangani **logika** seperti menampilkan halaman HTML dinamis, Kamu pakai `http.HandleFunc()`.

Contoh:

```go
http.HandleFunc("/home", func(w http.ResponseWriter, r *http.Request) {
	w.Write([]byte("Selamat datang di Home"))
})
```

Handler ini berupa fungsi dengan parameter `http.ResponseWriter` dan `*http.Request`.

***

### B.4.2 Fungsi `http.Handle`

Kalau untuk melayani **static files** seperti CSS, gambar, JS, baru pakai `http.Handle()`.

Handler di sini bukan fungsi biasa, tapi harus bertipe `http.Handler`.

Contohnya:

```go
http.Handle("/static/", http.StripPrefix("/static/", http.FileServer(http.Dir("assets"))))
```

***

### B.4.3 Intinya

* **http.HandleFunc()** → untuk logika program (fungsi biasa).
* **http.Handle()** → untuk melayani file statis (menggunakan objek `http.Handler`).

***

## B.5 Kesimpulan&#x20;

* Static assets perlu di-routing dengan rapi supaya bisa diakses dari browser.
* `http.StripPrefix()` wajib digunakan untuk menghindari path error.
* Pahami bedanya `http.HandleFunc()` dan `http.Handle()`.
* Struktur proyek yang rapi memudahkan manajemen file.

***
