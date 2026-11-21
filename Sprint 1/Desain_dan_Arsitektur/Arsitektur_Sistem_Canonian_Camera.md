# ARSITEKTUR SISTEM — Canonian Camera

Aplikasi web toko kamera digital berbasis digital twin.

## 1. Diagram Arsitektur

```mermaid
graph TB
    subgraph PRESENTASI[Lapisan Presentasi]
        A[Browser - HTML + CSS + JavaScript]
        A1[Halaman Pembeli - Katalog, Detail, Keranjang, Riwayat]
        A2[Viewer Digital Twin - Three.js atau model-viewer]
        A3[Halaman Admin - Kelola Produk, Pesanan & Laporan]
    end

    subgraph APLIKASI[Lapisan Aplikasi]
        B[Flask Backend - Python]
        B1[Autentikasi & Role]
        B2[Manajemen Katalog Kamera]
        B3[Logika Order & Stok]
        B4[Layanan Digital Twin & Simulasi]
        B5[API /api/produk, /api/order, /api/twin]
    end

    subgraph DATA[Lapisan Data]
        C[(SQLite Database)]
        G[Penyimpanan Model 3D - folder assets/models]
    end

    subgraph EKSTERNAL[Layanan Eksternal]
        D[Simulasi Pembayaran - Dummy]
        E[Payment Gateway - Future]
        F[Notifikasi Email - Future]
        H[API Ongkir - Future]
    end

    A --> A1
    A --> A2
    A --> A3
    A -->|HTTP Request| B
    B --> B1
    B --> B2
    B --> B3
    B --> B4
    B --> B5
    B -->|Query| C
    B4 -->|Ambil model GLB| G
    B -->|Konfirmasi Bayar| D
    E -.->|Future| B
    B -.->|Future| F
    H -.->|Future| B
```

## 2. Penjelasan Layer

| Layer | Komponen | Fungsi |
|-------|----------|--------|
| **Presentasi** | HTML, CSS, JavaScript, Three.js/model-viewer | Menampilkan katalog kamera, viewer digital twin 3D, keranjang, dan dashboard admin |
| **Aplikasi** | Flask (Python) | Memproses request, autentikasi, logika order dan stok, serta data simulasi digital twin |
| **Data** | SQLite + folder model 3D | Menyimpan data user, produk, pesanan, transaksi, dan preset digital twin; file model 3D (GLB) disimpan di folder aset |
| **Layanan Eksternal** | Simulasi Pembayaran / Payment Gateway / API Ongkir | Memproses pembayaran dan menghitung ongkos kirim |

## 3. Alur Komunikasi

### 3.1 Alur Pembelian Kamera

```mermaid
sequenceDiagram
    participant U as Pembeli
    participant B as Browser
    participant F as Flask
    participant S as SQLite
    participant P as Pembayaran

    U->>B: Pilih kamera & klik Beli
    B->>F: POST /api/order
    F->>S: Cek stok produk
    S-->>F: Stok tersedia
    F->>S: INSERT INTO orders dan order_items (status: pending)
    F->>P: Minta pembayaran
    P-->>F: Pembayaran sukses
    F->>S: UPDATE orders (paid), UPDATE produk (stok berkurang)
    F-->>B: JSON (detail pesanan)
    B-->>U: Tampilkan konfirmasi pesanan
```

### 3.2 Alur Digital Twin dan Simulasi Kamera

```mermaid
sequenceDiagram
    participant U as Pembeli
    participant B as Browser
    participant F as Flask
    participant S as SQLite
    participant M as Folder Model 3D

    U->>B: Buka detail kamera
    B->>F: GET /api/twin/id
    F->>S: Ambil data digital twin dan preset simulasi
    S-->>F: model_url, rentang ISO, aperture, shutter
    F-->>B: JSON (data digital twin)
    B->>M: Muat file model GLB
    M-->>B: Model 3D kamera
    B-->>U: Tampilkan kamera 3D yang bisa diputar dan di-zoom
    U->>B: Atur ISO, aperture, shutter speed
    B->>B: Hitung perkiraan hasil foto sesuai preset
    B-->>U: Tampilkan pratinjau hasil simulasi
```

### 3.3 Alur Admin Menambah Produk

```mermaid
sequenceDiagram
    participant A as Admin
    participant B as Browser
    participant F as Flask
    participant S as SQLite

    A->>B: Login & isi form produk baru
    B->>F: POST /api/produk
    F->>F: Validasi role admin
    F->>S: INSERT INTO produk dan digital_twin
    F-->>B: JSON (berhasil)
    B-->>A: Kamera tampil di katalog
```

## 4. Rancangan Tabel Database

```mermaid
erDiagram
    USERS ||--o{ ORDERS : membuat
    ORDERS ||--|{ ORDER_ITEMS : berisi
    PRODUK ||--o{ ORDER_ITEMS : dipesan_pada
    KATEGORI ||--o{ PRODUK : memiliki
    PRODUK ||--o| DIGITAL_TWIN : memiliki

    USERS {
        int id PK
        string nama
        string email
        string password_hash
        string role
    }
    KATEGORI {
        int id PK
        string nama_kategori
    }
    PRODUK {
        int id PK
        int kategori_id FK
        string merek
        string tipe
        string deskripsi
        string jenis_sensor
        float resolusi_mp
        int harga
        int stok
        string foto_url
    }
    DIGITAL_TWIN {
        int id PK
        int produk_id FK
        string model_url
        int iso_min
        int iso_max
        float aperture_min
        float aperture_max
        string shutter_min
        string shutter_max
    }
    ORDERS {
        int id PK
        int user_id FK
        int total_harga
        string status
        datetime created_at
    }
    ORDER_ITEMS {
        int id PK
        int order_id FK
        int produk_id FK
        int jumlah
        int harga_satuan
    }
```

## 5. Teknologi yang Digunakan

| Komponen | Teknologi | Alasan |
|----------|-----------|--------|
| Backend | Flask | Ringan, mudah dipelajari |
| Database | SQLite | Tidak perlu server, portable |
| Frontend | HTML + CSS + JavaScript | Sederhana, tanpa framework berat |
| Digital Twin 3D | Three.js atau model-viewer (format GLB) | Menampilkan model 3D langsung di browser tanpa plugin |
| Keamanan | Werkzeug (hash password) | Password tidak disimpan sebagai teks biasa |
| Pembayaran | Simulasi (dummy) | Bisa didemokan tanpa akun merchant |
| Version Control | Git + GitHub | Standar industri |
| Diagram | Mermaid | Render langsung di GitHub |

## 6. Kelebihan Arsitektur Ini

- **Modular** - Setiap layer terpisah, mudah dikembangkan
- **Interaktif** - Digital twin membuat pembeli bisa melihat dan mencoba kamera secara virtual sebelum membeli
- **Tanpa Layanan Berbayar** - Bisa jalan dengan simulasi pembayaran
- **Future-proof** - Siap diintegrasikan dengan payment gateway (mis. Midtrans), API ongkir (mis. RajaOngkir), dan email notifikasi
- **Aman** - Ada pemisahan role (pembeli/admin) dan password ter-hash
- **Ringan** - Tidak butuh server besar
