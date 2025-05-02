# Map

### 1. Mengenal Map dan Cara Penggunaan

Map adalah struktur data berisi pasangan key dan value. Setiap key harus unik, dan digunakan sebagai identifier untuk mengakses valuenya.

```go
var chicken = map[string]int{}
chicken["januari"] = 50
chicken["februari"] = 40

fmt.Println(chicken["januari"])
fmt.Println(chicken["mei"])
```

**Output:**

```
50
0
```

Key `"mei"` belum pernah dimasukkan, maka menghasilkan nilai default `0` untuk `int`.

### 2. Inisialisasi Map

```go
var data map[string]int
data["one"] = 1 // error: assignment to entry in nil map

data = map[string]int{}
data["one"] = 1
fmt.Println(data)
```

**Output:**

```
map[one:1]
```

Contoh inisialisasi:

```go
var chicken1 = map[string]int{"januari": 50, "februari": 40}
var chicken2 = map[string]int{
	"januari":  50,
	"februari": 40,
}
```

Semua bentuk di atas menghasilkan map yang siap digunakan.

### 3. Iterasi dengan `for-range`

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

**Output (urutan bisa berbeda):**

```
januari     : 50
februari    : 40
maret       : 34
```

### 4. Menghapus Item

```go
var chicken = map[string]int{"januari": 50, "februari": 40}

fmt.Println(len(chicken))
fmt.Println(chicken)

delete(chicken, "januari")

fmt.Println(len(chicken))
fmt.Println(chicken)
```

**Output:**

```
2
map[februari:40 januari:50]
1
map[februari:40]
```

### 5. Cek Keberadaan Key

```go
var chicken = map[string]int{"januari": 50, "februari": 40}
val, exist := chicken["mei"]

if exist {
	fmt.Println(val)
} else {
	fmt.Println("data tidak ditemukan")
}
```

**Output:**

```
data tidak ditemukan
```

### 6. Kombinasi Slice dan Map

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

**Output:**

```
male chicken blue
male chicken red
female chicken yellow
```

Contoh dengan key berbeda-beda:

```go
var data = []map[string]string{
	{"name": "chicken blue", "gender": "male", "color": "brown"},
	{"address": "mangga street", "id": "k001"},
	{"community": "chicken lovers"},
}

for _, item := range data {
	fmt.Println(item)
}
```

**Output:**

```
map[color:brown gender:male name:chicken blue]
map[address:mangga street id:k001]
map[community:chicken lovers]
```

***
