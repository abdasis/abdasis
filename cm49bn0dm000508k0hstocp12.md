---
title: "Panduan Lengkap Commit Convention untuk Pengembangan Proyek"
datePublished: Wed Dec 04 2024 03:21:24 GMT+0000 (Coordinated Universal Time)
cuid: cm49bn0dm000508k0hstocp12
slug: panduan-lengkap-commit-convention-untuk-pengembangan-proyek
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1733282424985/8d3a9132-910f-4fe1-be16-d2aa4fea3125.webp
tags: frontend, backend, git

---

Commit convention adalah standar penulisan pesan commit yang terstruktur dan konsisten. Dengan mengikuti konvensi ini, kolaborasi dalam tim pengembang menjadi lebih efisien, riwayat commit lebih terorganisir, dan memudahkan proses debugging. Artikel ini akan membahas commit types yang sering digunakan, lengkap dengan contoh penggunaannya.

---

## **Mengapa Commit Convention Penting?**

Commit convention membantu:

* Memahami perubahan tanpa harus membaca seluruh kode.
    
* Mempermudah generasi otomatis *changelogs*.
    
* Meningkatkan kolaborasi dalam tim pengembangan.
    

---

## **Jenis Commit dan Penggunaannya**

Berikut adalah daftar jenis commit beserta kapan dan bagaimana menggunakannya:

### **1\.** `build`

Gunakan untuk perubahan yang memengaruhi sistem build atau alat eksternal.  
**Contoh Penggunaan**:

* Memperbarui dependensi.
    
* Mengubah konfigurasi *build tools* seperti Webpack, Gradle, atau Gulp.  
    **Contoh Commit**:
    

```plaintext
build: update webpack to version 5
```

---

### **2\.** `chore`

Digunakan untuk tugas-tugas pemeliharaan proyek yang tidak memengaruhi kode sumber atau pengujian.  
**Contoh Penggunaan**:

* Memperbarui file `package-lock.json`.
    
* Membersihkan file yang tidak relevan.  
    **Contoh Commit**:
    

```plaintext
chore: update package-lock.json
```

---

### **3\.** `ci`

Gunakan untuk perubahan yang terkait dengan konfigurasi CI/CD seperti Jenkins, GitHub Actions, atau Travis.  
**Contoh Penggunaan**:

* Menambahkan langkah pengujian otomatis.
    
* Mengoptimalkan pipeline CI/CD.  
    **Contoh Commit**:
    

```plaintext
ci: add linting step to GitHub Actions
```

---

### **4\.** `docs`

Gunakan untuk perubahan yang hanya memengaruhi dokumentasi.  
**Contoh Penggunaan**:

* Menambahkan panduan kontribusi.
    
* Memperbaiki typo pada dokumentasi.  
    **Contoh Commit**:
    

```plaintext
docs: fix typo in contributing guide
```

---

### **5\.** `feat`

Gunakan untuk menambahkan fitur baru ke aplikasi.  
**Contoh Penggunaan**:

* Membuat halaman baru di frontend.
    
* Menambahkan endpoint API baru.  
    **Contoh Commit**:
    

```plaintext
feat: add user profile page
```

---

### **6\.** `fix`

Gunakan untuk memperbaiki bug di aplikasi.  
**Contoh Penggunaan**:

* Memperbaiki crash aplikasi.
    
* Menangani error pada validasi data.  
    **Contoh Commit**:
    

```plaintext
fix: resolve login authentication issue
```

---

### **7\.** `perf`

Gunakan untuk meningkatkan performa atau efisiensi aplikasi.  
**Contoh Penggunaan**:

* Mengurangi waktu respons API.
    
* Mengoptimalkan query database.  
    **Contoh Commit**:
    

```plaintext
perf: improve data fetch speed by caching
```

---

### **8\.** `refactor`

Gunakan untuk mengubah struktur kode tanpa memengaruhi fungsionalitas.  
**Contoh Penggunaan**:

* Menghapus kode duplikat.
    
* Mengubah nama variabel agar lebih deskriptif.  
    **Contoh Commit**:
    

```plaintext
refactor: rename variables for better readability
```

---

### **9\.** `revert`

Gunakan untuk membatalkan perubahan yang telah dilakukan sebelumnya.  
**Contoh Penggunaan**:

* Menghapus commit yang menyebabkan bug.  
    **Contoh Commit**:
    

```plaintext
revert: revert "feat: add user profile page"
```

---

### **10\.** `style`

Gunakan untuk perubahan yang hanya memengaruhi tampilan kode (tanpa memengaruhi logika).  
**Contoh Penggunaan**:

* Memperbaiki indentasi.
    
* Menambahkan spasi atau menghapus komentar yang tidak relevan.  
    **Contoh Commit**:
    

```plaintext
style: format code according to ESLint rules
```

---

### **11\.** `test`

Gunakan untuk menambahkan atau memperbaiki pengujian.  
**Contoh Penggunaan**:

* Menambahkan pengujian unit baru.
    
* Memperbaiki pengujian yang gagal.  
    **Contoh Commit**:
    

```plaintext
test: add tests for login API
```

---

## **Manfaat Menggunakan Commit Convention**

* **Riwayat yang Jelas**: Commit convention membuat log git lebih mudah dipahami.
    
* **Automasi**: Dapat digunakan untuk membuat *changelogs* otomatis.
    
* **Kolaborasi yang Efisien**: Semua anggota tim dapat memahami tujuan commit dengan mudah.
    

---

Mengadopsi commit convention bukan hanya soal kebiasaan, tetapi juga investasi untuk mempermudah pengembangan di masa depan. Mulailah dari sekarang untuk membuat commit yang lebih bermakna!