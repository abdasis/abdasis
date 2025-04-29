# B.1. Golang Web App: Hello World

### B.1.1 Membuat Aplikasi Web Pertama

#### Membuat Struktur Project

Langkah pertama, buat sebuah folder baru untuk project Kamu. Di dalamnya, buat file bernama `main.go`.

Lalu isi file tersebut dengan deklarasi package dan import dua library penting:

```go
package main

import (
	"fmt"
	"net/http"
)
```

**Penjelasan:**

* `package main` menandakan bahwa ini adalah program utama yang bisa dijalankan.
* `import` digunakan untuk memanggil library. `fmt` untuk menampilkan teks, `net/http` untuk membuat server web.

***

#### Membuat Handler

Handler adalah fungsi yang bertugas merespons permintaan dari browser. Setiap kali ada request masuk ke server, handler inilah yang akan dipanggil.

Contoh dua buah handler:

```go
func handlerIndex(w http.ResponseWriter, r *http.Request) {
	message := "Welcome"
	w.Write([]byte(message))
}

func handlerHello(w http.ResponseWriter, r *http.Request) {
	message := "Hello world!"
	w.Write([]byte(message))
}
```

**Penjelasan:**

* `w http.ResponseWriter`: objek untuk mengirimkan response ke browser.
* `r *http.Request`: objek yang membawa semua informasi tentang request.
* `w.Write([]byte(message))`: mengubah teks biasa menjadi `[]byte` supaya bisa dikirim sebagai response.

***

#### Membuat Routing dan Menjalankan Server

Routing digunakan untuk menentukan fungsi mana yang harus dijalankan berdasarkan URL yang diakses.

```go
func main() {
	http.HandleFunc("/", handlerIndex)
	http.HandleFunc("/index", handlerIndex)
	http.HandleFunc("/hello", handlerHello)

	address := "localhost:9000"
	fmt.Printf("server started at %s\n", address)
	err := http.ListenAndServe(address, nil)
	if err != nil {
		fmt.Println(err.Error())
	}
}
```

**Penjelasan:**

* `http.HandleFunc("/path", handler)`: menghubungkan URL ke fungsi handler tertentu.
* `http.ListenAndServe(address, nil)`: membuat dan menjalankan web server di alamat `localhost:9000`.
* Jika server gagal dijalankan, error akan ditampilkan.

***

#### Cara Mengakses Web Server

Setelah menjalankan dengan perintah `go run main.go`, buka browser dan coba akses:

| URL                           | Hasil Tampil |
| ----------------------------- | ------------ |
| `http://localhost:9000/`      | Welcome      |
| `http://localhost:9000/index` | Welcome      |
| `http://localhost:9000/hello` | Hello world! |

***

### B.1.2 Menjalankan Server dengan http.Server

#### Alternatif Membuat Server

Kamu juga bisa membuat server menggunakan objek `http.Server` supaya lebih fleksibel.

Berikut contohnya:

```go
package main

import (
	"fmt"
	"net/http"
	"time"
)

func main() {
	address := ":9000"
	fmt.Printf("server started at %s\n", address)

	server := new(http.Server)
	server.Addr = address

	server.ReadTimeout = 10 * time.Second
	server.WriteTimeout = 10 * time.Second

	err := server.ListenAndServe()
	if err != nil {
		fmt.Println(err.Error())
	}
}
```

**Penjelasan:**

* `server.Addr`: menentukan alamat server.
* `server.ReadTimeout`: batas waktu maksimal membaca request, misalnya 10 detik.
* `server.WriteTimeout`: batas waktu maksimal untuk mengirim response.
* `server.ListenAndServe()`: menjalankan server.

Dengan pendekatan ini, Kamu bisa mengatur lebih banyak pengaturan server, misalnya timeout, ukuran maksimal header, TLS, dan sebagainya.

***
