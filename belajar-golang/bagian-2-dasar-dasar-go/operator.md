# Operator

### 1. Pengertian Operator

Operator di Golang adalah simbol atau karakter yang digunakan untuk melakukan operasi terhadap nilai atau variabel. Terdapat tiga kategori utama: **aritmatika**, **perbandingan**, dan **logika**.

***

### 2. Operator Aritmatika di Golang

Operator aritmatika digunakan untuk melakukan operasi perhitungan dasar.

| Tanda |      Keterangan     |
| :---: | :-----------------: |
|   +   |     Penjumlahan     |
|   -   |     Pengurangan     |
|   \*  |      Perkalian      |
|   /   |      Pembagian      |
|   %   | Modulus (sisa bagi) |

**Contoh Penggunaan:**

```go
var hasil = (((2 + 6) % 3) * 4 - 2) / 3
fmt.Println(hasil) // Output: 0
```

Operator ini sangat berguna dalam membuat perhitungan cepat dan efisien.

***

### 3. Operator Perbandingan di Golang

Operator perbandingan digunakan untuk membandingkan dua nilai dan menghasilkan nilai boolean (`true` atau `false`).

| Tanda |          Keterangan          |
| :---: | :--------------------------: |
|   ==  |          Sama dengan         |
|   !=  |       Tidak sama dengan      |
|   <   |       Lebih kecil dari       |
|   <=  | Lebih kecil atau sama dengan |
|   >   |       Lebih besar dari       |
|   >=  | Lebih besar atau sama dengan |

**Contoh Penggunaan:**

```go
var nilai = (((2 + 6) % 3) * 4 - 2) / 3
var apakahSama = (nilai == 2)

fmt.Printf("Nilai: %d, Apakah sama 2? %t\n", nilai, apakahSama)
```

Gunakan `%t` untuk menampilkan nilai boolean dengan `fmt.Printf()`.

***

### 4. Operator Logika di Golang

Operator logika digunakan untuk menggabungkan ekspresi boolean.

| Tanda |  Keterangan  |
| :---: | :----------: |
|   &&  |   Dan (AND)  |
|       |              |
|   !   | Negasi (NOT) |

**Contoh Penggunaan:**

```go
var kiri = false
var kanan = true

var dan = kiri && kanan
fmt.Printf("kiri && kanan: %t\n", dan)

var atau = kiri || kanan
fmt.Printf("kiri || kanan: %t\n", atau)

var negasi = !kiri
fmt.Printf("!kiri: %t\n", negasi)
```

* `&&` akan menghasilkan `true` jika kedua nilai `true`.
* `||` akan menghasilkan `true` jika salah satu nilai `true`.
* `!` akan menghasilkan nilai kebalikan.

***

### 5. Kesimpulan

Memahami penggunaan operator aritmatika, perbandingan, dan logika di Golang sangat penting untuk membangun program yang efektif dan logis. Penerapannya akan membantu Kamu menulis kode yang lebih bersih, efisien, dan mudah dipahami.

***
