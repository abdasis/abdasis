# Variabel dan Tipe Data

### 1Variabel

Variabel adalah wadah untuk menyimpan nilai atau data dalam program. Dengan variabel, Kamu bisa menyimpan informasi seperti angka, teks, atau kondisi tertentu untuk digunakan kembali di dalam kode.\
Dalam Go, setiap variabel harus punya tipe data yang jelas, supaya program berjalan lebih aman dan terstruktur.

***

### 1.1. Deklarasi Variabel dengan Tipe Data (Manifest Typing)

Go mewajibkan deklarasi variabel eksplisit dengan tipe data menggunakan **manifest typing**. Contohnya:

```go
package main

import "fmt"

func main() {
    var firstName string = "budi"
    var lastName string
    lastName = "santoso"

    fmt.Printf("Halo %s %s!\n", firstName, lastName)
}
```

Kata kunci `var` digunakan untuk mendeklarasikan variabel. Nilai bisa diberikan langsung saat deklarasi atau diisi nanti.

***

### 1.2. Penggunaan Keyword `var`

Format dasar deklarasi menggunakan `var`:

```go
var <nama-variabel> <tipe-data>
var <nama-variabel> <tipe-data> = <nilai>
```

Contoh:

```go
var lastName string
var firstName string = "budi"
```

Untuk menampilkan variabel:

```go
fmt.Printf("Halo %s %s!\n", firstName, lastName)
fmt.Println("Halo", firstName, lastName+"!")
```

Gunakan  di `fmt.Printf()` untuk membuat baris baru.

***

### 1.3. Deklarasi Variabel Tanpa Menulis Tipe Data (Type Inference)

Go juga mendukung **type inference**, sehingga tipe data variabel otomatis mengikuti nilai.

```go
var firstName string = "budi"
lastName := "santoso"

fmt.Printf("Halo %s %s!\n", firstName, lastName)
```

Saat deklarasi pertama, gunakan `:=`. Untuk assignment berikutnya cukup `=`:

```go
lastName := "santoso"
lastName = "pratama"
lastName = "wijaya"
```

Deklarasi menggunakan `:=` hanya bisa dilakukan di dalam fungsi.

***

### 1.4. Deklarasi Multi Variabel

Go mendukung deklarasi beberapa variabel sekaligus menggunakan tanda koma:

```go
var first, second, third string
first, second, third = "satu", "dua", "tiga"

var fourth, fifth, sixth string = "empat", "lima", "enam"

seventh, eighth, ninth := "tujuh", "delapan", "sembilan"
```

Variabel bisa bertipe berbeda:

```go
jumlah, hariLibur, suhu, sapaan := 1, true, 29.5, "selamat pagi"
```

***

### 1.5. Variabel Underscore (`_`)

Go tidak mengizinkan variabel yang tidak digunakan. Solusinya, gunakan `_` untuk membuang nilai:

```go
_ = "belajar Golang"
_ = "Golang itu mudah"

nama, _ := "andi", "wijaya"
```

Isi variabel `_` tidak bisa diakses lagi.

***

### 1.6. Deklarasi Variabel dengan `new`

Fungsi `new()` digunakan untuk membuat pointer dengan tipe tertentu:

```go
nama := new(string)

fmt.Println(nama)   // output alamat memori
fmt.Println(*nama)  // output nilai default ""
```

Gunakan `*` untuk mengambil nilai dari pointer.

***

### 7. Deklarasi Variabel dengan `make`

Fungsi `make()` dipakai khusus untuk membuat:

* `channel`
* `slice`
* `map`

***

### 2. Tipe Data

Golang menawarkan beragam tipe data bawaan untuk memenuhi berbagai kebutuhan pemrosesan, mulai dari angka bulat hingga teks dan kondisi logika. Memilih tipe data yang tepat membuat penggunaan memori lebih efisien dan menghindarkan munculnya bug. Di bawah ini kita bahas tipe data standar di Go.

### 2.1. Numerik Non-Desimal

Tipe numerik non-desimal (integer) di Go ada dua kategori utama:

* **`uint`** untuk bilangan cacah (hanya positif)
* **`int`** untuk bilangan bulat (negatif & positif)

Keduanya dibagi menurut lebar bit:

| Tipe   | Cakupan Nilai                                          | Alias |
| ------ | ------------------------------------------------------ | ----- |
| uint8  | 0 … 255                                                | byte  |
| uint16 | 0 … 65.535                                             | —     |
| uint32 | 0 … 4.294.967.295                                      | —     |
| uint64 | 0 … 18.446.744.073.709.551.615                         | —     |
| uint   | sama dengan uint32/uint64 tergantung OS                | —     |
| int8   | –128 … 127                                             | —     |
| int16  | –32.768 … 32.767                                       | —     |
| int32  | –2.147.483.648 … 2.147.483.647                         | rune  |
| int64  | –9.223.372.036.854.775.808 … 9.223.372.036.854.775.807 | —     |
| int    | sama dengan int32/int64 tergantung OS                  | —     |

```go
var a uint8  = 89
var b        = -1243423644  // otomatis jadi int32

fmt.Printf("positif: %d\n", a)
fmt.Printf("negatif: %d\n", b)
```

Gunakan format `%d` untuk mencetak bilangan bulat.

### 2.2. Numerik Desimal

Go mendukung dua tipe floating-point: **`float32`** dan **`float64`**, sesuai standar IEEE-754.

```go
var x = 2.62       // default float32
fmt.Printf("nilai x: %f\n", x)    // 6 angka di belakang koma
fmt.Printf("x 3 desimal: %.3f\n", x)
```

Untuk mengatur jumlah digit di belakang koma, gunakan `%.nf` (n = jumlah digit).

### 2.3. Boolean

Tipe **`bool`** hanya memiliki dua nilai: `true` atau `false`. Sering dipakai di kondisi dan perulangan (lihat Bab A.13 & A.14).

```go
var ok bool = true
fmt.Printf("exist? %t\n", ok)
```

Gunakan `%t` untuk mencetak nilai boolean.

### 2.4. String

String di Go diapit oleh tanda kutip ganda (`"..."`). Untuk teks multi-baris atau yang berisi banyak karakter khusus tanpa escape, gunakan backticks (`` `...` ``).

```go
var s1 string = "Halo"
fmt.Printf("s1: %s\n", s1)

var s2 = `Nama saya "Ali".
Baris baru muncul di sini.
Belajar Go seru!`
fmt.Println(s2)
```

Format `%s` mencetak nilai string apa adanya.

### 2.5. Nil & Zero Value

**Zero value** adalah nilai default variabel jika tidak diinisialisasi:

* string → `""`
* bool → `false`
* numerik → `0` atau `0.0`

Beberapa tipe (pointer, slice, map, channel, fungsi, interface) memiliki zero value `nil`, yang artinya “kosong sekali”.

```go
var p *int       // pointer, default nil
var sl []int     // slice, default nil
var m  map[string]int  // map, default nil

fmt.Println(p, sl, m)  // semua tercetak: <nil> [] map[]  
```

***

Dengan pemahaman tipe data di atas, Kamu siap menyusun variabel tepat sesuai kebutuhan. Selanjutnya di Bab A.11 kita akan mempelajari bagaimana menggunakan variabel ini dalam operasi dan ekspresi.
