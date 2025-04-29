---
coverY: 0
---

# Setup Go Modules

Di bab ini, kita akan mempelajari cara membuat project baru menggunakan **Go Modules**, yang merupakan cara resmi Go untuk mengelola dependensi dalam pengembangan perangkat lunak.

***

### 1. Penjelasan

**Go Modules** adalah alat untuk manajemen dependensi dalam Go. Dengan Go Modules, kamu dapat dengan mudah menginisialisasi sebuah project dan mengelola dependensi pihak ketiga (third-party libraries) yang digunakan dalam project kamu.

Go Modules dioperasikan menggunakan **Command Line Interface (CLI)**, jadi setelah menginstal Go, kamu secara otomatis bisa menggunakan perintah-perintah CLI Go Modules.

Penting untuk diketahui bahwa di Go, istilah **module** (atau module) itu sama artinya dengan **project**. Jadi, kamu tidak perlu bingung, ya! Jika kamu mendengar "module", itu berarti project di Go.

***

### 2. Inisialisasi Project Menggunakan Go Modules

Untuk memulai sebuah project baru dengan Go Modules, kita perlu menginisialisasi project tersebut menggunakan perintah `go mod init`.

Langkah-langkahnya sebagai berikut:

1.  **Buat Folder Project Baru**\
    Kamu bisa membuat folder baru dengan menggunakan perintah CLI atau dengan browser/finder di sistem operasi kamu.

    Misalnya, kita akan membuat folder bernama `project-pertama`:

    ```bash
    mkdir project-pertama
    cd project-pertama
    ```
2.  **Inisialisasi Project dengan Go Modules**\
    Setelah masuk ke folder project yang baru saja dibuat, jalankan perintah `go mod init` diikuti dengan nama project (biasanya sesuai dengan nama folder):

    ```bash
    go mod init project-pertama
    ```

    Dengan perintah ini, kita telah menginisialisasi folder `project-pertama` sebagai sebuah project Go dengan nama yang sama.

#### Penjelasan Command `go mod init`

Perintah `go mod init` digunakan untuk menginisialisasi project Go dan menghasilkan file bernama **`go.mod`**. File ini sangat penting, karena digunakan oleh Go toolchain untuk menandai folder ini sebagai sebuah project Go. Jadi, jangan pernah menghapus file ini.

Skema penulisan command `go mod` adalah sebagai berikut:

```bash
go mod init <nama-project>
```

Di sini, kita menentukan nama project dengan nama folder, yaitu `project-pertama`. Ini adalah praktik terbaik dalam Go, di mana nama project dan nama module sebaiknya sama.

#### Apa Itu `go.mod`?

Setelah menjalankan perintah `go mod init`, Go akan menghasilkan file **`go.mod`** di dalam folder project. File ini berfungsi untuk mendefinisikan module (project) dan menangani dependensi yang digunakan dalam project.

***

Dengan langkah-langkah di atas, kamu telah berhasil menginisialisasi project Go menggunakan Go Modules.

Sebagai informasi tambahan, selain menggunakan **Go Modules**, Go juga mendukung penggunaan **`$GOPATH`** untuk setup project. Namun, penggunaan `GOPATH` sudah ketinggalan zaman dan tidak disarankan lagi, terutama untuk project yang dikembangkan menggunakan Go versi terbaru (1.14 ke atas). Oleh karena itu, menggunakan Go Modules adalah cara yang lebih modern dan dianjurkan.

***
