---
title: "🔥 Evolusi Arsitektur Laravel: Saatnya Atomic Query Construction (AQC) Ambil Alih"
datePublished: Sat Apr 26 2025 04:21:24 GMT+0000 (Coordinated Universal Time)
cuid: cm9xpqzmm000b09jp1o1h4tod
slug: evolusi-arsitektur-laravel-saatnya-atomic-query-construction-aqc-ambil-alih
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1745641248707/3eb53ed7-feda-48b0-bb69-dd4e24f83b1d.jpeg
tags: laravel, php

---

## 💡 AQC vs FormRequest: Sebuah Lompatan Arsitektur

Dulu, banyak developer Laravel — termasuk Aku — memanfaatkan method `handle()` di dalam `FormRequest`. Tujuannya jelas: menyatukan validasi, otorisasi, dan penyimpanan data dalam satu tempat.

Tapi makin ke sini, pendekatan itu mulai terasa membatasi. Kenapa? Karena logika bisnis jadi terjebak di layer HTTP. Artinya, kalau Kamu ingin pakai logika yang sama untuk WebSocket, CLI, atau job terjadwal — ya nggak bisa, atau minimal jadi ribet.

Solusinya? Tarik logika itu keluar dari `FormRequest`, dan pindahkan ke class khusus yang lebih fleksibel: **AQC (Atomic Query Construction)**.

---

## 🚀 Apa Itu AQC (Atomic Query Construction)?

AQC adalah pola desain super ringan — tanpa instalasi, tanpa binding — yang memisahkan setiap aksi query ke dalam satu class tunggal.

Struktur folder-nya pun rapi dan predictable:

```plaintext
app/
└── AQC/
    └── Product/
        ├── CreateProduct.php
        ├── UpdateProduct.php
        ├── GetAllProducts.php
        ├── GetProduct.php           
        └── DeleteProduct.php
```

Contoh isi `GetAllProducts.php`:

```php
namespace App\AQC\Product;

use App\Models\Product;

class GetAllProducts
{
    public static function handle($params = [], $paginate = true, $scenario = 'default')
    {
        $productObj = Product::latest('id');

        if (isset($params['category_id']) && $params['category_id'] > 0) {
            $productObj->where('category_id', $params['category_id']);
        }

        if (isset($params['brand_id']) && $params['brand_id'] > 0) {
            $productObj->where('brand_id', $params['brand_id']);
        }

        switch ($scenario) {
            case 'minimal':
                $productObj->select(['id', 'name']);
                break;
            case 'compact':
                $productObj->select(['id', 'name', 'price', 'image']);
                break;
            case 'admin':
                $productObj->select(['id', 'name', 'price', 'sku', 'image', 'stock', 'cost']);
                break;
            default:
                $productObj->select('*');
        }

        return $paginate
            ? $productObj->paginate(Product::PAGINATE)
            : $productObj->get();
    }
}
```

---

## 🧠 Gimana Cara Pakainya?

AQC bisa dipanggil dari mana aja. Contoh di controller:

```php
use App\Http\Requests\Product\GetAllProductsRequest;
use App\AQC\Product\GetAllProducts;

class ProductController extends Controller
{
    public function index(GetAllProductsRequest $request)
    {
        $params = $request->all();
        $product = GetAllProducts::handle($params);
        return ResponseHelper::handle('index', $data);
    }
}
```

---

## 🌐 Cocok Buat Web, API, WebSocket, CLI — Apa Aja!

* ✅ **Web/API route**
    
    ```php
    Route::get('/products', [ProductController::class, 'index']);
    ```
    
* ✅ **WebSocket**
    
    ```php
    use App\AQC\Product\GetAllProducts;
    
    class GetProductsHandler implements MessageComponentInterface
    {
        public function onMessage(ConnectionInterface $from, MessageInterface $message)
        {
            $filters = json_decode($message->getPayload(), true);
            $products = GetAllProducts::handle($filters);
            $from->send(json_encode($products));
        }
    }
    ```
    

---

## 🧅 Mengikuti Prinsip Onion Architecture

Dengan pola ini, kita menciptakan arsitektur yang bersih dan scalable:

* **UI Layer** = Web, API, WebSocket
    
* **Controller/Handler** = Intermediary tipis
    
* **AQC** = Pusat logika bisnis
    

---

## 🤔 Kenapa Nggak Pakai Service Class?

Kamu mungkin berpikir, "Bukannya ini kayak service biasa?"

Masalahnya, banyak service class di Laravel itu jadi keranjang statis yang isinya campur aduk. AQC memaksa disiplin:

* 🔹 **Atomic** – satu class = satu tugas
    
* 🔹 **Query-centric** – fokus ke aksi data
    
* 🔹 **Reusable** – nggak terikat layer tertentu
    

Dengan penamaan AQC, struktur jadi lebih jelas dan terorganisir.

---

## ✅ Keuntungan AQC

* 💎 Kode lebih bersih, fokus, reusable
    
* 🧪 Mudah di-test
    
* 📦 Tanpa package tambahan
    
* 🌱 Siap scaling tanpa glue code
    
* 👀 Semua aksi query terpusat, gampang tracking
    

---

## ✍️ Penutup

AQC bukan satu-satunya cara, tapi sejauh ini ini adalah **cara paling bersih** yang Aku temukan untuk membangun arsitektur Laravel yang scalable, fleksibel, dan minim duplikasi kode.

Kalau Kamu lagi membangun aplikasi Laravel yang kompleks, coba deh terapin AQC. Sekali coba, bakal ketagihan.

---

Kalau Kamu suka artikel ini dan pengen lebih banyak insight seputar Laravel, teknologi, dan open source — tinggal bilang, kita gas bareng tulis artikel-artikel kerennya 😎

Mau lanjut ke topik AQC lanjutan atau eksplor hal lain?