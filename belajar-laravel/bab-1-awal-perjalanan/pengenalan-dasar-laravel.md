# Pengenalan Dasar Laravel

### Ringkasan Bab

Pada bab ini, Kamu akan memahami apa itu Laravel, latar belakang pembuatannya, filosofi utama, serta struktur arsitektur MVC yang menjadi fondasi kerjanya. Laravel diperkenalkan pertama kali oleh Taylor Otwell pada 2011 sebagai alternatif modern untuk framework PHP yang ada saat itu, membawa sintaks yang elegan dan ekosistem lengkap untuk mempercepat pengembangan aplikasi web. Kamu juga akan diperkenalkan pada komponen inti Laravel—seperti routing, Eloquent ORM, dan Blade—serta peran komunitas dalam menjaga framework ini selalu up-to-date dan aman.

***

### 1. Definisi Laravel

Laravel adalah framework aplikasi web berbasis PHP yang bersifat open-source dan dirancang untuk membuat proses pengembangan web menjadi lebih cepat, terstruktur, dan menyenangkan bagi pengembang. Framework ini mengintegrasikan berbagai modul dan pustaka—mulai dari routing hingga manajemen database—sehingga pengembang tidak perlu menulis semuanya dari nol.

***

### 2. Sejarah Singkat

Taylor Otwell merilis versi pertama Laravel pada Juni 2011 sebagai jawaban atas keterbatasan framework CodeIgniter—khususnya ketiadaan fitur autentikasi dan otorisasi bawaan. Sejak itu, Laravel berkembang pesat dengan rilis mayor setiap tahun dan rilis minor serta patch secara rolling release, memastikan fitur baru dan perbaikan bug selalu tersedia.

***

### 3. Filosofi dan Tujuan

Laravel dibangun dengan filosofi “kode yang elegan melahirkan aplikasi yang kuat”. Framework ini berfokus pada:

* **Ekspresivitas sintaks** agar kode mudah dibaca dan dipelajari.
* **Produktivitas tinggi** lewat alat seperti Artisan CLI dan Eloquent ORM.
* **Keamanan bawaan** dengan proteksi CSRF, enkripsi, dan middleware otentikasi.

***

### 4. Arsitektur MVC di Laravel

Laravel mengadopsi pola **Model-View-Controller (MVC)** untuk memisahkan tanggung jawab kode:

* **Model**: Berinteraksi dengan database melalui Eloquent ORM, menyimpan logika bisnis dan aturan validasi.
* **View**: Menghasilkan tampilan antarmuka menggunakan Blade templating engine yang Mendukung pewarisan layout dan komponen ulang.
* **Controller**: Menangani alur permintaan pengguna, memproses data via Model, dan memilih View yang sesuai.

Pemisahan ini membuat kode lebih terstruktur, mudah diuji, dan dipelihara seiring pertumbuhan aplikasi.

***

### 5. Komponen Inti Laravel

#### 5.1 Routing

Routing di Laravel memungkinkan Kamu mendefinisikan jalur URL dengan sintaks yang ringkas dan fleksibel.

#### 5.2 Eloquent ORM

Eloquent adalah sistem Object-Relational Mapping yang intuitif, memungkinkan operasi database tanpa menulis SQL mentah.

#### 5.3 Blade Templating

Blade menyediakan sintaks ringan untuk membuat tampilan dinamis, mendukung directive seperti `@if`, `@foreach`, dan pewarisan template.

#### 5.4 Middleware

Middleware berfungsi menyaring request masuk—misalnya untuk otentikasi atau logging—sebelum mencapai aplikasi inti.

#### 5.5 Artisan CLI

Artisan adalah command-line interface Laravel yang mempermudah otomatisasi tugas pengembangan, seperti pembuatan controller, model, migration, dan queue management.

***

### 6. Ekosistem dan Komunitas

Laravel didukung oleh ekosistem luas, meliputi:

* **Laracasts**: Platform tutorial video resmi.
* **Packalyst**: Direktori package komunitas.
* **Laracon**: Konferensi tahunan Laravel di berbagai belahan dunia.

Komunitas aktif ini memastikan dokumentasi selalu diperbarui dan banyak solusi tersedia di forum, blog, serta kanal media sosial.

***

Dengan memahami dasar-dasar di atas, Kamu sudah siap melangkah ke bab selanjutnya: **Persiapan Tools Development**, di mana kita akan menyiapkan lingkungan pengembangan agar bisa langsung membangun aplikasi Laravel secara optimal.
