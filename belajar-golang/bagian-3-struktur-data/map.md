# Map

### 1. Mengenal Map dan Cara Penggunaan

Map adalah struktur data yang menyimpan pasangan key dan value. Setiap data yang disimpan harus memiliki key yang unik, sedangkan valuenya bebas selama sesuai tipe yang ditentukan. Berbeda dengan slice yang memakai indeks numerik, map memungkinkan Kamu menggunakan tipe data lain sebagai key—yang penting unik.

```go
var chicken = map[string]int{}
chicken["januari"] = 50
chicken["februari"] = 40

fmt.Println(chicken["januari"]) // 50
fmt.Println(chicken["mei"])     // 0 (default int)
```

Jika key yang dipanggil belum tersedia, map akan mengembalikan nilai default dari tipe datanya.

### 2. Inisialisasi Map

Karena default map adalah `nil`, Kamu wajib menginisialisasinya sebelum digunakan agar tidak error. Bisa dengan `{}`, `make()`, atau `new()`.

```go
var chicken1 = map[string]int{"januari": 50, "februari": 40}

var chicken2 = map[string]int{
	"januari":  50,
	"februari": 40,
}

var chicken3 = map[string]int{}
var chicken4 = make(map[string]int)
var chicken5 = *new(map[string]int) // tipe pointer
```

Semua cara di atas sah, tinggal disesuaikan kebutuhan. Gunakan `*` untuk ambil nilai dari hasil `new()` karena berupa pointer.

### 3. Iterasi dengan `for-range`

Kamu bisa menelusuri semua item dalam map menggunakan `for-range`. Hasilnya akan mengembalikan key dan value.

```go
var chicken = map[string]int{
	"januari":  50,
	"februari": 40,
	"maret":    34,
}

for key, val := range chicken {
	fmt.Println(key, "\t:", val)
}
```

Urutan output bisa berbeda karena map tidak memiliki urutan tetap.

### 4. Menghapus Item

Gunakan fungsi `delete()` untuk menghapus elemen berdasarkan key-nya.

```go
delete(chicken, "januari")
```

Setelah dihapus, key tersebut tidak akan ditemukan lagi saat diakses.

### 5. Cek Apakah Key Ada

Untuk mengecek keberadaan key, gunakan dua variabel saat akses:

```go
val, ok := chicken["mei"]

if ok {
	fmt.Println(val)
} else {
	fmt.Println("data tidak ditemukan")
}
```

Variabel `ok` akan bernilai `true` jika key tersedia.

### 6. Gabungan Slice dan Map

Kamu bisa membuat slice yang tiap elemennya berupa map. Kombinasi ini umum digunakan untuk menyimpan kumpulan data dinamis seperti list siswa atau produk.

```go
var chickens = []map[string]string{
	{"name": "chicken blue", "gender": "male"},
	{"name": "chicken red", "gender": "male"},
	{"name": "chicken yellow", "gender": "female"},
}

for _, chicken := range chickens {
	fmt.Println(chicken["gender"], chicken["name"])
}
```

Map dalam slice bisa memiliki key yang berbeda-beda di tiap elemen:

```go
var data = []map[string]string{
	{"name": "chicken blue", "gender": "male", "color": "brown"},
	{"address": "mangga street", "id": "k001"},
	{"community": "chicken lovers"},
}
```

***
