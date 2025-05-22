# Cara Clone Private Repository GitHub di cPanel

***

### 🔐 Apa Itu Private Repository GitHub?

Private repository adalah repositori yang hanya bisa diakses oleh pemiliknya atau oleh user yang diberi izin. Untuk meng-clone repo jenis ini ke dalam hosting seperti cPanel, dibutuhkan akses khusus melalui SSH key, bukan sekadar URL seperti public repo.

> Fitur clone private repo ini biasanya hanya tersedia pada hosting tipe **Medium**, **Large**, atau **Cloud Hosting**.

***

### ✨ Langkah-Langkah Clone Private Repository GitHub di cPanel

#### 1. Membuat SSH Key di Terminal cPanel

1. Login ke **cPanel**, lalu buka menu **Terminal**.
2.  Jalankan perintah berikut (ganti `username` dengan username GitHub Kamu):

    ```bash
    ssh-keygen -t rsa -b 4096 -C "username@github.com"
    ```
3.  Saat diminta nama file, ketik misalnya:

    ```
    /home/username/.ssh/private_github
    ```
4. **Kosongkan passphrase** dengan menekan `Enter` dua kali.
5.  Lihat SSH key yang telah dibuat:

    ```bash
    cat ~/.ssh/private_github.pub
    ```
6. **Copy seluruh isi key** yang muncul di terminal.

***

#### 2. Menambahkan Konfigurasi SSH

1. Masuk ke **File Manager** di cPanel.
2. Buka folder `.ssh` dan buat file baru bernama `config`.
3.  Isi file `config` dengan:

    ```bash
    Host *
      IdentityFile ~/.ssh/private_github
    ```
4. Ubah permission file `config` ke `700`.

***

#### 3. Tambahkan SSH Key ke GitHub

1. Login ke GitHub.
2. Masuk ke halaman repository privat yang ingin di-clone.
3. Klik **Settings** > **Deploy Keys** > **Add deploy key**.
4. Masukkan judul dan paste SSH Key yang sudah dicopy sebelumnya.
5. (Opsional) Centang **Allow write access** jika Kamu juga ingin melakukan push dari cPanel.

***

#### 4. Clone Repository via Git Version Control

1. Kembali ke cPanel > buka menu **Git Version Control**.
2. Ambil URL clone **SSH** dari GitHub (contoh: `git@github.com:user/repo.git`).
3. Klik tombol **Create** > isikan data project.
4. Paste URL tadi pada kolom **Clone URL**, lalu klik **Create**.

> ✅ Proses cloning akan berjalan. Jika repo besar, tunggu beberapa saat hingga selesai.

***

### 🔁 Update dan Deploy Repo dari GitHub

Jika ada update di GitHub dan ingin menarik (pull) perubahan ke server:

1. Klik menu **Manage** di project Git Version Control.
2. Buka tab **Pull or Deploy**.
3. Scroll ke bawah, klik **Update From Remote**.

Setelah proses ini selesai, folder di server Kamu akan berisi versi terbaru dari repository GitHub.

***

### ✅ Kesimpulan

Dengan mengikuti langkah-langkah di atas, Kamu bisa:

* Clone private repository GitHub dengan aman ke cPanel
* Menghindari error autentikasi dengan SSH
* Sinkronisasi update GitHub ke hosting hanya dengan beberapa klik

Jangan lupa pastikan Kamu tidak menggunakan passphrase saat generate SSH key agar proses cloning bisa berjalan dengan lancar di GitHub.

Selanjutnya, kita akan bahas bab penting lainnya tentang **Continuous Deployment Otomatis dengan Git di cPanel** — tetap semangat!
