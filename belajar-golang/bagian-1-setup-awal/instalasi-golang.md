# Instalasi Golang

Sebelum mulai menulis kode dengan Go, langkah pertama yang perlu dilakukan adalah menginstal bahasa pemrograman ini di perangkat kamu. Panduan instalasi lengkap sebenarnya sudah tersedia di situs resmi Go ([https://golang.org/doc/install#install](https://golang.org/doc/install#install)), namun di bab ini, kami akan memberikan ringkasan langkah-langkah yang lebih sederhana agar kamu bisa mengikuti proses instalasi dengan mudah, terutama jika kamu baru pertama kali menggunakan Go.

Go yang digunakan di sini adalah versi **1.22**. Direkomendasikan untuk menggunakan versi tersebut agar dapat mengikuti tutorial dengan lancar.

#### URL untuk Mengunduh Installer Go

Kamu dapat mengunduh installer Go dari link berikut:\
[https://golang.org/dl/](https://golang.org/dl/)

Setelah mengunduh, silakan ikuti langkah-langkah instalasi sesuai dengan sistem operasi yang kamu gunakan.

***

### 1. Instalasi Go di Windows

1. **Unduh Installer Go**\
   Kunjungi [https://golang.org/dl/](https://golang.org/dl/) dan pilih installer untuk Windows sesuai dengan jenis bit (32-bit atau 64-bit) yang digunakan.
2. **Jalankan Installer**\
   Setelah file installer terunduh, jalankan installer dan ikuti petunjuk hingga instalasi selesai. Secara default, Go akan terinstal di `C:\go`. Jika tidak mengubah path selama instalasi, Go akan secara otomatis didaftarkan dalam variabel lingkungan `PATH`.
3.  **Verifikasi Instalasi**\
    Buka Command Prompt (CMD) dan jalankan perintah berikut untuk memeriksa versi Go yang terinstal:

    ```bash
    go version
    ```

    Jika output menunjukkan versi Go yang terpasang, itu berarti instalasi berhasil.

    **Catatan:** Jika perintah `go version` tidak dikenali meskipun instalasi berhasil, coba restart Command Prompt (tutup dan buka kembali), lalu jalankan kembali perintah tersebut.

***

### 2. Instalasi Go di macOS

Cara termudah untuk menginstal Go di macOS adalah dengan menggunakan **Homebrew**.

1.  **Install Homebrew**\
    Jika belum memiliki Homebrew, jalankan perintah berikut di terminal untuk menginstalnya:

    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
2.  **Instal Go Menggunakan Homebrew**\
    Setelah Homebrew terinstal, jalankan perintah berikut untuk menginstal Go:

    ```bash
    brew install go
    ```
3.  **Tambahkan Go ke PATH**\
    Agar Go dapat dikenali dari terminal, tambahkan Go ke variabel lingkungan `PATH`:

    ```bash
    echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.bash_profile
    source ~/.bash_profile
    ```
4.  **Verifikasi Instalasi**\
    Untuk memastikan Go telah terinstal dengan benar, jalankan perintah berikut:

    ```bash
    go version
    ```

    Jika output menampilkan versi Go yang terinstal, berarti instalasi berhasil.

***

### 3. Instalasi Go di Linux

1.  **Unduh Arsip Installer**\
    Kunjungi [https://golang.org/dl/](https://golang.org/dl/) dan unduh arsip Go untuk Linux sesuai dengan arsitektur sistem kamu (32-bit atau 64-bit). Kamu bisa mengunduhnya melalui terminal menggunakan `wget` atau `curl`.

    Contoh perintah menggunakan `wget`:

    ```bash
    wget https://storage.googleapis.com/golang/go1.22.linux-amd64.tar.gz
    ```
2.  **Ekstrak Arsip ke Direktori `/usr/local`**\
    Setelah arsip terunduh, ekstrak file ke dalam direktori `/usr/local`:

    ```bash
    tar -C /usr/local -xzf go1.22.linux-amd64.tar.gz
    ```
3.  **Tambahkan Go ke PATH**\
    Agar Go dapat dikenali dari terminal, tambahkan Go ke dalam variabel lingkungan `PATH` dengan menambahkan baris berikut ke dalam file `~/.bashrc`:

    ```bash
    echo "export PATH=$PATH:/usr/local/go/bin" >> ~/.bashrc
    source ~/.bashrc
    ```
4.  **Verifikasi Instalasi**\
    Terakhir, periksa apakah Go telah terinstal dengan benar dengan menjalankan perintah:

    ```bash
    go version
    ```

    Jika Go terinstal dengan benar, output yang muncul akan menunjukkan versi Go yang baru saja terpasang.

***

### 4. Variabel GOROOT

Setelah berhasil menginstal Go, secara otomatis sebuah variabel lingkungan bernama **GOROOT** akan diatur. Variabel ini menunjukkan lokasi di mana Go terinstal. Sebagai contoh, di Windows, jika Go diinstal di `C:\go`, maka nilai GOROOT adalah `C:\go`.

Untuk memverifikasi konfigurasi ini, kamu bisa menjalankan perintah berikut di terminal atau CMD:

```bash
go env
```

Perintah tersebut akan menampilkan konfigurasi lingkungan, termasuk nilai dari GOROOT.

***

### 5. Instalasi Go Versi Unstable/Development

Jika kamu tertarik untuk mencoba fitur-fitur terbaru dari Go yang belum dirilis secara resmi, kamu bisa menginstal versi **unstable** atau **development**.

1. **Build dari Source**\
   Kamu bisa mengikuti panduan instalasi dari source code yang disediakan di [Go Install Source](https://go.dev/doc/install/source).
2.  **Menggunakan Perintah Go Install**\
    Alternatif lainnya adalah menggunakan perintah `go install` untuk menginstal versi Go tertentu yang belum stabil, seperti contoh berikut:

    ```bash
    go install golang.org/dl/go1.18beta1@latest
    ```

    Untuk melihat daftar versi unstable yang bisa diinstal, kamu bisa merujuk ke [Go Downloads](https://go.dev/dl/#unstable).

***
