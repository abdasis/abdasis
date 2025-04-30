# Persiapan Tools Development

***

## Persiapan Tools Development

Sebelum mulai membangun aplikasi dengan Laravel, pastikan lingkungan pengembangan (development environment) Kamu sudah lengkap. Di bab ini, kita akan menyiapkan semua tools penting: PHP, Composer, Node.js, web server, database, Git, dan editor kode.

***

### 1. Instalasi PHP

Laravel 12 memerlukan **PHP versi minimum 8.2**, sedangkan Laravel 10–11 membutuhkan PHP ≥ 8.1\
Pastikan juga memasang ekstensi–ekstensi standar PHP seperti OpenSSL, PDO, Mbstring, Tokenizer, XML, dan Ctype. Cek versi PHP di terminal dengan:

```bash
php -v
```

***

### 2. Instalasi Composer

Composer adalah dependency manager untuk PHP. Laravel menggunakan Composer untuk mengelola paket dan framework-nya.\
Pasang Composer secara global:

```bash
# Linux/macOS
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer

# Windows
# Unduh Composer-Setup.exe dari situs resmi Composer
```

Cek instalasi:

```bash
composer --version
```

***

### 3. Node.js dan NPM

Laravel Mix (Webpack wrapper) memerlukan **Node.js** dan **NPM** untuk mengompilasi aset (CSS/JS).\
Unduh dan pasang Node.js (termasuk NPM) dari situs resmi Node.js. Setelah terpasang, verifikasi dengan:

```bash
node -v
npm -v
```

***

### 4. Web Server: Laravel Herd atau Sail

* **Laravel Herd**: Solusi all-in-one untuk Windows dan macOS—termasuk PHP, nginx, dan database—siap pakai.
* **Laravel Sail**: Docker-based environment resmi Laravel, cocok di Linux, macOS, dan Windows.

Pilih salah satu sesuai sistem operasi dan preferensi Kamu. Keduanya menghemat waktu konfigurasi manual.

***

### 5. Database

Laravel mendukung beberapa database populer:

* MySQL ≥ 5.7 (atau MariaDB ≥ 10.3)
* PostgreSQL ≥ 10.0
* SQLite ≥ 3.26.0
* SQL Server ≥ 2017

Untuk pemula, MySQL atau MariaDB adalah pilihan umum. Instal MySQL/MariaDB, lalu konfigurasikan di file `.env`:

```dotenv
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nama_database
DB_USERNAME=user
DB_PASSWORD=password
```

***

### 6. Git

Git diperlukan untuk version control dan kolaborasi.\
Pasang Git dan atur identitas:

```bash
git --version
git config --global user.name "Nama Kamu"
git config --global user.email "email@kamu.com"
```

Untuk memulai proyek Laravel dari repository:

```bash
git clone <repo-url>
cd nama-proyek
composer install
npm install
cp .env.example .env
php artisan key:generate
```

***

### 7. Editor Kode

Pilih editor yang mendukung PHP dan Laravel. Dua opsi populer:

* **Visual Studio Code** dengan extension Laravel (autocomplete, navigation)
* **PhpStorm** atau IDE JetBrains dengan fitur canggih untuk PHP/Laravel

Pasang extension PHP Intellisense, Blade snippets, dan Git integration agar workflow lebih efisien.

***

Dengan semua tools di atas siap, lingkungan development Kamu telah optimal untuk memulai pembangunan aplikasi Laravel. Selanjutnya, kita akan membuat proyek pertama dan memahami struktur direktori Laravel.
