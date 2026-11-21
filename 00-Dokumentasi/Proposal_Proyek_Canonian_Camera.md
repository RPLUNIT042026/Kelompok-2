# Proposal Proyek — Canonian Camera

## 1. Latar Belakang

Membeli kamera digital secara online sering membuat pembeli ragu: spesifikasi teknis (sensor, resolusi, ISO, aperture) sulit dipahami, bentuk dan ukuran kamera tidak bisa dirasakan lewat foto biasa, dan risiko produk tidak sesuai deskripsi atau tanpa garansi resmi cukup tinggi. Banyak toko online hanya menampilkan foto statis dan daftar spesifikasi, sehingga pembeli sulit membandingkan dan mengambil keputusan. Diperlukan toko kamera online yang informatif, terpercaya, dan interaktif, yaitu **Canonian Camera**, dengan fitur **digital twin** agar pembeli bisa melihat dan mencoba kamera secara virtual sebelum membeli.

## 2. Tujuan

- Menyediakan katalog kamera digital dengan informasi lengkap (merek, tipe, sensor, resolusi, harga, stok, foto)
- Ruang lingkup produk dibatasi pada kamera digital dalam tiga kategori:
  - Mirrorless: sensor, resolusi, jenis mount, kemampuan video
  - DSLR: sensor, resolusi, jumlah titik fokus, kecepatan burst
  - Pocket/compact: ukuran, zoom optik, cocok untuk pemula dan vlog
- Menyediakan digital twin tiap kamera: model 3D yang bisa diputar 360° dan di-zoom, serta simulasi pengaturan (ISO, aperture, shutter speed) dengan perkiraan hasil foto
- Menyediakan sistem transaksi yang aman (keranjang, checkout, payment gateway, status pesanan)
- Memudahkan pencarian, pemfilteran, dan perbandingan kamera sesuai kebutuhan pembeli
- Memberikan notifikasi otomatis untuk status pesanan dan pembayaran

## 3. Keputusan Sprint 1

### a. Agile Methodology

- Metodologi yang digunakan: **Scrum**
- Durasi sprint: ± 1 bulan per sprint (mengikuti timeline Sp1–Sp5)
- Role tim: 1 orang sebagai **Scrum Master** (koordinator), sisanya **Development Team**
- Tools tracking task: **GitHub Projects**

### b. UX Design

- Antarmuka dirancang dengan wireframe sederhana (Figma/sketsa) sebelum masuk development
- Elemen utama halaman:
  - Beranda: pilihan kategori (Mirrorless / DSLR / Pocket), kamera terlaris, dan pencarian
  - Katalog: filter merek, tipe, rentang harga, resolusi, dan jenis sensor
  - Detail produk: galeri foto, spesifikasi lengkap, harga, stok, viewer digital twin 3D, tombol beli
  - Simulator digital twin: panel pengaturan ISO, aperture, dan shutter speed beserta pratinjau hasil
  - Perbandingan: 2–3 kamera berdampingan
  - Keranjang, checkout & pembayaran: pilihan metode bayar, ongkos kirim, status pesanan
  - Notifikasi/alert (contoh: banner "Pembayaran berhasil, pesanan sedang diproses")
- Alur pengguna: buka toko → cari & filter kamera → lihat detail & coba digital twin → masuk keranjang → checkout → bayar → pesanan dikirim → konfirmasi diterima

### c. Project Setup

- Struktur folder awal repository:

  ```
  canonian-camera/
  ├── backend/        # API server (Flask/Node.js)
  ├── frontend/       # Halaman web (HTML/JS/CSS)
  ├── database/       # Skema & seed data dummy
  ├── assets/models/  # Model 3D kamera (digital twin)
  ├── docs/           # Wireframe, proposal, dokumentasi API
  └── README.md
  ```

- Tech stack awal: Python Dummy Data Generator (data kamera contoh), Flask/Node.js (backend), HTML/JS + Bootstrap/Tailwind (frontend awal), Three.js atau model-viewer (tampilan 3D)

## 4. Arsitektur Sistem

### a. Pengguna & Peran (Sumber Data)

- **Pembeli:** mencari, mencoba digital twin, membandingkan, membeli, dan mengonfirmasi pesanan
- **Admin:** mengelola produk (harga, stok, foto, model 3D), memverifikasi pembayaran, memperbarui status pesanan, dan memantau laporan penjualan

### b. Sistem Toko (Representasi Digital)

- **Frontend web:** katalog, detail produk, viewer digital twin, keranjang/checkout, dashboard admin
- **Backend REST API:** autentikasi, manajemen produk & stok, pesanan, pembayaran, dan data digital twin
- **Digital twin:** tiap kamera punya model 3D dan preset simulasi (rentang ISO, aperture, shutter speed sesuai kemampuan kamera aslinya) yang tersimpan di database
- **Opsi data awal (tanpa data nyata):** Dummy Data Generator berbasis Python untuk mengisi katalog kamera pada tahap pengembangan

### c. Fitur Tambahan

- Perbandingan 2–3 kamera secara berdampingan
- Rating & ulasan produk
- Rekomendasi kamera berdasarkan kebutuhan (pemula, vlog, fotografi) dan anggaran pembeli
- Stok real-time yang tersinkron dengan tampilan digital twin
- Notifikasi otomatis (email/WhatsApp/in-app) untuk status pesanan

### d. Catatan Risiko

- **Merek dagang:** nama "Canonian" mirip dengan merek Canon; tim perlu memastikan tidak memakai logo, nama model, atau aset resmi Canon tanpa izin, dan mencantumkan disclaimer bahwa proyek ini adalah tugas perkuliahan
- **Model 3D:** gunakan model buatan sendiri atau yang berlisensi bebas; model resmi dari produsen tidak boleh dipakai sembarangan
- **Keaslian produk & garansi:** untuk implementasi nyata, pastikan stok berasal dari distributor resmi dan sertakan informasi garansi pada halaman produk
- **Performa:** model 3D yang berat dapat memperlambat halaman di perangkat dengan spesifikasi rendah; gunakan model yang dioptimalkan dan pemuatan bertahap
- **Keamanan pembayaran:** transaksi hanya lewat payment gateway (sandbox pada tahap pengembangan), data pengguna tersimpan terenkripsi

## 5. Tech Stack (Rencana Awal)

| Komponen | Teknologi |
|----------|-----------|
| Sumber Data | Python Dummy Data Generator / input admin via form |
| Backend | (isi sesuai kesepakatan tim, contoh: Node.js/Express atau Flask) |
| Database | (contoh: MySQL/PostgreSQL/Firebase) |
| Frontend | HTML + JS + Bootstrap/Tailwind (atau React) |
| Digital Twin 3D | Three.js atau model-viewer (format model glTF/GLB) |
| Pembayaran | Payment gateway sandbox (contoh: Midtrans/Xendit) |
| Ongkos Kirim | API ongkir (contoh: RajaOngkir) |
| Komunikasi | HTTP REST API |

## 6. Rencana Sprint

| Sprint | Bulan | Fokus |
|--------|-------|-------|
| Sp1 | September | Tentukan arsitektur & tech stack, UX wireframe, setup repo |
| Sp2 | October | Backend (autentikasi, CRUD produk) + katalog & detail produk dasar |
| Sp3 | November | Digital twin 3D & simulator, keranjang, checkout, pembayaran (sandbox), notifikasi, refinement |
| Sp4 | December | Testing, dashboard admin, perbandingan kamera, rating & ulasan, upgrade tampilan |
| Sp5 | December | Final testing, bug fixing, persiapan demo Expo |

## 7. Anggota Tim

| Nama | NIM | Peran |
|------|-----|-------|
| Fauzan Azima | 250504109 | Ketua 1 |
| M Ihsan Ramadhani | 240504101 | Anggota 2 |
| Sherilda Ardianti | 250504027 | Anggota 3 |
| M Fahri Faqih | 250504017 | Anggota 4 |
