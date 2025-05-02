# Array

#### Konsep Dasar: Apa Itu Array?

Array adalah struktur data yang menyimpan sejumlah elemen **dengan tipe yang seragam** dalam satu variabel. Jumlah elemen bersifat **tetap** dan ditentukan saat deklarasi. Setiap elemen diakses melalui **indeks numerik**, dimulai dari angka 0.

```go
var names [4]string
names[0] = "trafalgar"
names[1] = "d"
names[2] = "water"
names[3] = "law"
```

Array `names` hanya mampu menampung 4 elemen string. Bila melebihi kapasitas, program akan gagal dikompilasi.

***

#### Ketatnya Alokasi Memori

Go tidak mentolerir pengisian di luar kapasitas. Coba menulis ke indeks kelima pada array yang hanya dialokasikan untuk empat elemen akan memunculkan **error "index out of range"**.

```go
names[4] = "ez" // ❌ Error
```

Jika Kamu memerlukan struktur yang dinamis dan fleksibel, gunakan `slice`, yang akan dibahas di bab selanjutnya.

***

#### Inisialisasi Nilai Langsung

Pengisian elemen array bisa dilakukan saat deklarasi, baik secara horizontal:

```go
var fruits = [4]string{"apple", "grape", "banana", "melon"}
```

Atau vertikal, yang lebih nyaman dibaca saat menangani banyak data:

```go
fruits = [4]string{
    "apple",
    "grape",
    "banana",
    "melon",
}
```

Ingat, tanda koma **wajib** ada di akhir setiap baris, termasuk baris terakhir.

***

#### Array Tanpa Ukuran Eksplisit

Gunakan `...` jika ingin membuat array tanpa menentukan jumlah elemen secara manual:

```go
var numbers = [...]int{2, 3, 2, 4, 3}
```

Go secara otomatis akan menghitung kapasitas berdasarkan jumlah elemen yang ditulis.

***

#### Array Multidimensi: Susun Data Bertingkat

Go mendukung array berdimensi lebih dari satu. Array multidimensi sangat cocok digunakan untuk struktur data seperti matriks.

```go
var matrix = [2][3]int{
    {3, 2, 3},
    {3, 4, 5},
}
```

Penulisan gaya ringkas ini sudah cukup umum dan memudahkan pembacaan.

***

#### Perulangan dengan for: Kendali Penuh

Perulangan manual dengan `for` memungkinkan kontrol indeks penuh atas elemen array:

```go
for i := 0; i < len(fruits); i++ {
    fmt.Printf("Elemen %d: %s\n", i, fruits[i])
}
```

***

#### Perulangan dengan for-range: Ringkas dan Efisien

`for-range` menyederhanakan iterasi tanpa perlu repot mengatur indeks secara manual:

```go
for i, fruit := range fruits {
    fmt.Printf("Elemen %d: %s\n", i, fruit)
}
```

Jika indeks tidak dibutuhkan, cukup ganti dengan `_`:

```go
for _, fruit := range fruits {
    fmt.Println("Buah:", fruit)
}
```

Atau, jika hanya ingin indeksnya:

```go
for i := range fruits {
    fmt.Println("Indeks:", i)
}
```

***

#### Alokasi Dinamis dengan `make()`

Fungsi `make()` memungkinkan Kamu mengalokasikan array secara dinamis:

```go
fruits := make([]string, 2)
fruits[0] = "apple"
fruits[1] = "manggo"
```

Struktur ini secara teknis adalah `slice`, namun cukup berguna saat menangani data yang bersifat sementara atau jumlahnya sudah diketahui sejak awal.

***

#### Penutup

Array di Go adalah struktur data yang **sederhana namun powerful**. Meski sifatnya statis, ia menawarkan performa optimal saat kapasitas data sudah diketahui sejak awal. Namun, jika fleksibilitas adalah kebutuhan utama, `slice` adalah senjata berikutnya yang wajib Kamu kuasai.

***
