# Slice

### 1. Pengertian Slice

Slice adalah tipe data dinamis yang mengacu ke sebagian data array. Slice membawa tiga informasi penting: pointer ke data awal, jumlah elemen (length), dan kapasitas maksimal (capacity). Slice tidak menyimpan data, tapi hanya menunjuk ke array sebagai sumbernya.

### 2. Membuat Slice

Slice bisa dibuat langsung tanpa mendeklarasikan array terlebih dahulu:

```go
buah := []string{"apel", "jeruk", "pisang"}
```

Slice juga bisa dibentuk dari array:

```go
var data = [5]int{1, 2, 3, 4, 5}
var potong = data[1:4] // hasil: [2 3 4]
```

### 3. Teknik Slicing

Slice menggunakan format `[start:end]`, di mana `start` adalah indeks awal (inklusif) dan `end` adalah indeks akhir (eksklusif).

Contoh variasi slicing:

* `data[1:]`: dari indeks ke-1 hingga akhir
* `data[:3]`: dari awal sampai sebelum indeks ke-3
* `data[:]`: mengambil semua elemen

### 4. Slice Bersifat Referensi

Slice tidak membuat salinan data baru, tetapi menunjuk ke sumber aslinya. Karena itu, perubahan pada satu slice bisa memengaruhi slice lain yang menunjuk ke data yang sama.

```go
x := data[0:2]
y := data[1:3]
y[0] = 100
```

Perubahan pada `y` akan terlihat juga pada `x` dan `data`.

### 5. Fungsi `len()` dan `cap()`

* `len(slice)`: menghitung jumlah elemen aktif
* `cap(slice)`: kapasitas maksimal dari posisi awal slice ke ujung array

```go
fmt.Println(len(potong)) // 3
fmt.Println(cap(potong)) // 4
```

### 6. Menambah Elemen Slice dengan `append()`

Fungsi `append()` digunakan untuk menambah elemen ke slice. Bila kapasitas tidak cukup, Golang akan otomatis membuat array baru di belakang layar.

```go
buahBaru := append(buah, "semangka")
```

Jika `append()` memicu alokasi array baru, maka slice hasilnya akan memiliki referensi yang berbeda.

### 7. Duplikasi Slice dengan `copy()`

Gunakan `copy()` jika ingin menggandakan slice tanpa hubungan data:

```go
asli := []string{"apel", "melon"}
salinan := make([]string, len(asli))
copy(salinan, asli)
```

Kini `salinan` dan `asli` benar-benar independen.

### 8. Slice dengan Tiga Parameter

Slice bisa dibuat menggunakan tiga indeks `[start:end:capacity]` untuk mengatur kapasitas secara manual.

```go
data := [...]int{1, 2, 3, 4, 5}
potong := data[0:2:2]
```

Hasilnya: `len(potong) = 2`, `cap(potong) = 2`

***
