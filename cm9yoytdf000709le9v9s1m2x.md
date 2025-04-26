---
title: "📚 Membangun Aplikasi dengan Event-Driven Architecture di Golang"
datePublished: Sat Apr 26 2025 20:47:16 GMT+0000 (Coordinated Universal Time)
cuid: cm9yoytdf000709le9v9s1m2x
slug: membangun-aplikasi-dengan-event-driven-architecture-di-golang
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1745700321293/1bd55f55-d63a-4af8-89a8-09d5c5ca58a0.png
tags: golang

---

## 🚀 Pendahuluan

Event-driven architecture (EDA) adalah sebuah pendekatan yang memungkinkan aplikasi untuk bereaksi terhadap berbagai peristiwa (events) yang terjadi. Dalam pola ini, aplikasi lebih modular, fleksibel, dan lebih mudah untuk di-scale. Pada artikel ini, kita akan membahas bagaimana membangun aplikasi menggunakan **Event-Driven Architecture** dengan **Golang**.

---

## 🛠️ Apa itu Event-Driven Architecture?

Event-driven architecture adalah paradigma di mana aplikasi dibangun di sekitar **event** atau peristiwa yang memicu proses atau aksi tertentu. Sebuah event bisa berupa:

* **User Action** (misalnya pengguna klik tombol)
    
* **System State Changes** (misalnya data berhasil disimpan di database)
    
* **External Events** (misalnya menerima data dari API eksternal)
    

Komponen utama dalam EDA adalah:

1. **Producer (Publisher)**: Menghasilkan event.
    
2. **Consumer (Subscriber)**: Mendengarkan dan merespons event.
    
3. **Message Broker**: Meneruskan event antara producer dan consumer.
    

---

## 📦 Struktur Folder Aplikasi Event-Driven di Golang

Untuk memudahkan pengembangan aplikasi dengan Event-Driven Architecture, kita perlu memecah aplikasi ke dalam folder dan file yang terorganisir dengan baik. Berikut adalah contoh struktur folder yang cocok untuk aplikasi berbasis event-driven di Golang:

```plaintext
plaintextCopyEdit/go-event-driven-app
├── cmd/
│   └── app/
│       └── main.go             # Main entry point aplikasi
├── internal/
│   ├── event/
│   │   ├── publisher.go        # Event publisher untuk mengirimkan event
│   │   └── subscriber.go       # Event subscriber untuk menerima dan menangani event
│   ├── handler/
│   │   ├── order_handler.go    # Handler untuk event order
│   │   └── payment_handler.go  # Handler untuk event pembayaran
│   ├── model/
│   │   ├── order.go            # Model untuk order
│   │   └── payment.go          # Model untuk payment
│   ├── service/
│   │   ├── order_service.go    # Service yang menangani logika bisnis order
│   │   └── payment_service.go  # Service yang menangani logika pembayaran
│   ├── infra/
│   │   ├── db.go              # Koneksi database
│   │   └── nats.go            # Koneksi dengan message broker (misalnya NATS)
│   └── config/
│       └── config.go           # Konfigurasi aplikasi (DB, Broker, dll)
├── go.mod
├── go.sum
└── README.md
```

---

## 🧱 Penjelasan Struktur Folder

### 1\. **cmd/app/main.go**

File utama yang digunakan untuk menjalankan aplikasi. Di sini, kita melakukan inisialisasi koneksi ke message broker (seperti NATS atau Kafka), konfigurasi, dan mendaftarkan event handler.

### 2\. **internal/event/publisher.go**

Berisi kode untuk mempublikasikan event ke message broker. Misalnya, ketika sebuah transaksi order terjadi, kita akan mengirimkan event `order.created` ke message broker.

### 3\. **internal/event/subscriber.go**

Menangani event yang diterima dari message broker. Subscriber mendengarkan event seperti `order.created` dan menjalankan tindakan yang sesuai, misalnya memproses pembayaran atau mengirim notifikasi.

### 4\. **internal/model/**

Folder ini berisi model data yang digunakan di aplikasi, seperti `order.go` dan `payment.go`. Model ini digunakan untuk mewakili struktur data yang dipertukarkan dalam event.

### 5\. **internal/service/**

Berisi layanan yang menangani logika bisnis aplikasi. Contohnya adalah `order_service.go` untuk menangani order, dan `payment_service.go` untuk menangani logika pembayaran.

### 6\. **internal/handler/**

Handler bertanggung jawab untuk memproses event yang diterima dari subscriber. Misalnya, `order_handler.go` akan menangani event `order.created` dan melakukan proses lebih lanjut, seperti memanggil service payment.

### 7\. **internal/infra/**

Menyediakan infrastruktur yang dibutuhkan aplikasi, seperti koneksi ke database dan message broker (misalnya NATS).

---

## 🧩 Alur Kerja Event-Driven di Golang

1. **Event Publish**: Saat suatu event terjadi (misalnya order dibuat), aplikasi akan mem-publish event tersebut ke message broker.
    
2. **Event Subscribe**: Subscriber akan mendengarkan event yang dipublish dan mengeksekusi tindakan tertentu. Misalnya, setelah event `order.created` diterima, subscriber akan memproses pembayaran dan mem-publish event `payment.completed`.
    
3. **Communication**: Event yang dikirimkan melalui message broker memungkinkan komunikasi asinkron antar komponen tanpa ketergantungan langsung.
    

---

## 🏗️ Implementasi Dasar

### 1\. **Publisher Event:**

```go
package event

import (
    "encoding/json"
    "go-event-driven-app/internal/model"
    "github.com/nats-io/nats.go"
)

var nc *nats.Conn

func InitPublisher(conn *nats.Conn) {
    nc = conn
}

func PublishOrderCreated(order model.Order) error {
    data, err := json.Marshal(order)
    if err != nil {
        return err
    }

    return nc.Publish("order.created", data)
}
```

### 2\. **Subscriber Event:**

```go
package event

import (
    "log"
    "go-event-driven-app/internal/handler"
    "github.com/nats-io/nats.go"
)

func SubscribeOrderCreated(nc *nats.Conn) {
    nc.Subscribe("order.created", func(msg *nats.Msg) {
        handler.HandleOrderCreated(msg.Data)
    })
}
```

### 3\. **Handler:**

```go
package handler

import (
    "encoding/json"
    "log"
    "go-event-driven-app/internal/model"
    "go-event-driven-app/internal/service"
)

func HandleOrderCreated(data []byte) {
    var order model.Order
    if err := json.Unmarshal(data, &order); err != nil {
        log.Printf("Error unmarshaling order: %v", err)
        return
    }

    if err := service.ProcessPayment(order); err != nil {
        log.Printf("Failed to process payment: %v", err)
    }
}
```

---

## 🚀 Keuntungan Event-Driven Architecture

1. **Scalability**: Sistem mudah di-scale, karena setiap service dapat berdiri sendiri dan saling berkomunikasi melalui event.
    
2. **Resilience**: Event-driven membuat aplikasi lebih tahan terhadap gangguan. Event dapat diproses ulang jika terjadi kegagalan.
    
3. **Flexibility**: Penambahan fitur baru bisa dilakukan dengan menambahkan event dan handler tanpa merusak sistem yang ada.
    
4. **Asynchronous**: Proses yang memakan waktu lama (seperti pembayaran atau pengiriman email) dapat dijalankan secara asinkron.
    

---

## 🎯 Kesimpulan

Dengan memanfaatkan **Event-Driven Architecture**, aplikasi kamu menjadi lebih fleksibel dan mudah berkembang seiring waktu. Struktur folder yang baik sangat membantu dalam memisahkan concerns antara berbagai komponen aplikasi, mulai dari event publishing, event handling, hingga pengolahan logika bisnis.

Ini adalah pondasi yang sangat baik untuk membangun aplikasi berbasis event-driven yang scalable dan mudah dikelola.