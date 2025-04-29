# B.2 Routing dengan http.HandleFunc di Golang

### B.2.1 Penggunaan Dasar http.HandleFunc()

Routing adalah proses menentukan fungsi mana yang akan dipanggil berdasarkan URL yang diakses. Di Go, salah satu cara paling sederhana untuk membuat routing adalah menggunakan fungsi `http.HandleFunc()`.

#### Apa itu http.HandleFunc()?

`http.HandleFunc()` berfungsi untuk:

* **Mendaftarkan** rute (alamat URL) tertentu.
* **Menentukan** handler (fungsi yang akan dijalankan) untuk rute tersebut.

**Parameter dari `http.HandleFunc()`:**

* **Parameter 1**: String yang mewakili rute, seperti `/`, `/index`, `/about`.
* **Parameter 2**: Fungsi (handler) yang dijalankan ketika rute diakses. Harus berbentuk `func(http.ResponseWriter, *http.Request)`.

***

#### Contoh Langsung

Buat file `main.go`, isi dengan:

```go
package main

import (
	"fmt"
	"net/http"
)

func main() {
	handlerIndex := func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("hello"))
	}

	http.HandleFunc("/", handlerIndex)
	http.HandleFunc("/index", handlerIndex)

	http.HandleFunc("/data", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("hello again"))
	})

	fmt.Println("server started at localhost:9000")
	http.ListenAndServe(":9000", nil)
}
```

***

#### Penjelasan Setiap Bagian

* `handlerIndex` adalah **closure** — fungsi yang langsung disimpan dalam variabel — untuk menangani dua rute: `/` dan `/index`.
* Rute `/data` menggunakan **anonymous function** — fungsi tanpa nama — yang langsung dituliskan sebagai handler.
* `fmt.Println` digunakan untuk memberi tahu bahwa server sudah berjalan.
* `http.ListenAndServe(":9000", nil)` adalah perintah untuk **menyalakan server** di port `9000`.

***

### B.2.2 Cara Menjalankan dan Menguji

Setelah kodenya siap:

1.  Jalankan perintah:

    ```bash
    go run main.go
    ```
2. Buka browser dan akses URL berikut:
   * `http://localhost:9000/` ➔ Akan menampilkan `hello`
   * `http://localhost:9000/index` ➔ Akan menampilkan `hello`
   * `http://localhost:9000/data` ➔ Akan menampilkan `hello again`

***

### Ringkasan Penting

* Handler bisa berupa **fungsi biasa**, **closure**, atau **anonymous function**.
*   Yang penting, handler wajib punya format:

    ```go
    func(w http.ResponseWriter, r *http.Request)
    ```
* Semua response ditulis menggunakan `w.Write([]byte("isi response"))`.
* Server Go sangat ringan dan cepat untuk memulai web app sederhana.

***
