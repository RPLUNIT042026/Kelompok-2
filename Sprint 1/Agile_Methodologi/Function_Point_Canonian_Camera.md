# Dokumen Perhitungan Function Point & Product Backlog
## Canonian Camera: Aplikasi Web Toko Kamera Digital Berbasis Digital Twin

---

## A. Perhitungan Function Point (FP)

Function Point digunakan untuk mengestimasi ukuran/kompleksitas aplikasi berdasarkan fitur yang direncanakan, sebelum development dimulai.

### 1. Identifikasi Komponen Fungsional

| No | Komponen | Tipe | Kompleksitas | Bobot |
|----|----------|------|--------------|-------|
| 1 | Registrasi & login pengguna (pembeli/admin) | External Input (EI) | Low | 3 |
| 2 | Input & kelola produk kamera oleh admin (merek, tipe, spesifikasi, harga, stok, foto, model 3D) | External Input (EI) | Average | 4 |
| 3 | Keranjang belanja & checkout pembeli | External Input (EI) | Average | 4 |
| 4 | Konfirmasi pembayaran & update status pesanan oleh admin | External Input (EI) | Low | 3 |
| 5 | Input simulasi pengaturan kamera pada digital twin (ISO, aperture, shutter speed, mode) | External Input (EI) | Average | 4 |
| 6 | Notifikasi otomatis status pesanan & pembayaran | External Output (EO) | Average | 5 |
| 7 | Dashboard penjualan, laporan transaksi & stok real-time (admin) | External Output (EO) | Average | 5 |
| 8 | Tampilan digital twin 3D kamera (putar 360°, zoom, perkiraan hasil foto sesuai simulasi) | External Output (EO) | Average | 5 |
| 9 | Katalog kamera dengan pencarian & filter (merek, tipe, harga, resolusi, jenis sensor) | External Inquiry (EQ) | Average | 4 |
| 10 | Halaman detail produk (spesifikasi lengkap & galeri foto) | External Inquiry (EQ) | Low | 3 |
| 11 | Perbandingan 2–3 kamera secara berdampingan | External Inquiry (EQ) | Average | 4 |
| 12 | Riwayat pesanan pengguna | External Inquiry (EQ) | Low | 3 |
| 13 | Data pengguna (database) | Internal Logical File (ILF) | Average | 10 |
| 14 | Data produk & stok (database) | Internal Logical File (ILF) | Average | 10 |
| 15 | Data pesanan & transaksi (database) | Internal Logical File (ILF) | Average | 10 |
| 16 | Data digital twin (model 3D & preset simulasi per kamera) | Internal Logical File (ILF) | Low | 7 |
| 17 | Koneksi ke payment gateway eksternal (Midtrans/Xendit sandbox) | External Interface File (EIF) | Average | 7 |
| 18 | Koneksi ke layanan cek ongkos kirim eksternal (mis. RajaOngkir) | External Interface File (EIF) | Low | 5 |

### 2. Tabel Ringkasan Unadjusted Function Point (UFP)

| Tipe Komponen | Jumlah | Bobot Rata-rata | Total |
|---------------|--------|-----------------|-------|
| External Input (EI) | 5 | 3,6 | 18 |
| External Output (EO) | 3 | 5 | 15 |
| External Inquiry (EQ) | 4 | 3,5 | 14 |
| Internal Logical File (ILF) | 4 | 9,25 | 37 |
| External Interface File (EIF) | 2 | 6 | 12 |
| **Total UFP** | | | **96** |

### 3. Value Adjustment Factor (VAF) — Sederhana

Untuk proyek skala kelas/kuliah, VAF bisa diasumsikan netral (VAF = 1.0), karena belum ada 14 faktor kompleksitas teknis yang dinilai secara detail. Jika ingin lebih presisi, VAF dapat dihitung dari 14 General System Characteristics (GSC) dengan skala 0–5 untuk tiap faktor.

**Rumus:**

```
FP = UFP x VAF
FP = 96 x 1.0 = 96
```

> Catatan: Angka-angka di atas adalah estimasi awal. Sesuaikan kembali dengan fitur final yang disepakati tim sebelum development dimulai.

---

## B. Product Backlog (Keseluruhan Proyek)

Daftar fitur/User Stories yang direncanakan untuk seluruh proyek (Sp1–Sp5):

| ID | User Story | Prioritas |
|----|-----------|-----------|
| US-01 | Sebagai pembeli, saya ingin melihat katalog kamera digital (mirrorless, DSLR, pocket) agar bisa memilih kamera yang sesuai | Tinggi |
| US-02 | Sebagai pembeli, saya ingin mencari dan memfilter kamera berdasarkan merek, tipe, harga, resolusi, dan jenis sensor | Tinggi |
| US-03 | Sebagai pembeli, saya ingin melihat detail produk (spesifikasi lengkap, foto, stok) agar yakin sebelum membeli | Tinggi |
| US-04 | Sebagai pembeli, saya ingin memutar dan men-zoom model 3D kamera (digital twin) agar bisa melihat bentuk kamera dari semua sisi | Tinggi |
| US-05 | Sebagai pembeli, saya ingin mengatur ISO, aperture, dan shutter speed pada digital twin untuk melihat perkiraan hasil fotonya | Tinggi |
| US-06 | Sebagai admin, saya ingin menambah, mengubah, dan menghapus produk beserta harga, stok, foto, dan model 3D | Tinggi |
| US-07 | Sebagai pembeli, saya ingin memasukkan kamera ke keranjang dan melakukan checkout serta pembayaran secara aman | Tinggi |
| US-08 | Sebagai pengguna, saya ingin registrasi dan login agar data dan transaksi saya aman | Sedang |
| US-09 | Sebagai pengguna, saya ingin menerima notifikasi otomatis saat status pesanan atau pembayaran berubah | Sedang |
| US-10 | Sebagai admin, saya ingin memverifikasi pembayaran dan memperbarui status pesanan (diproses, dikirim, selesai) | Sedang |
| US-11 | Sebagai pembeli, saya ingin membandingkan 2–3 kamera secara berdampingan agar mudah menentukan pilihan | Sedang |
| US-12 | Sebagai pembeli, saya ingin melihat riwayat pesanan saya | Sedang |
| US-13 | Sebagai admin, saya ingin melihat dashboard penjualan, laporan transaksi, dan stok real-time | Rendah |
| US-14 | Sebagai pembeli, saya ingin memberi rating dan ulasan untuk produk yang sudah dibeli | Rendah |
| US-15 | Sebagai pembeli, saya ingin mendapat rekomendasi kamera berdasarkan kebutuhan (pemula, vlog, fotografi) dan anggaran saya | Rendah |

---

## C. Sprint 1 Backlog

Target kerja spesifik yang harus diselesaikan pada Sprint 1 (bukan development fitur, tetapi tahap persiapan):

| Task | Deskripsi | Penanggung Jawab |
|------|-----------|------------------|
| Project Charter | Menyusun latar belakang, tujuan, ruang lingkup (toko kamera digital Canonian Camera: katalog, digital twin, keranjang, checkout, manajemen produk), struktur tim | Ketua |
| Perhitungan Function Point | Estimasi ukuran aplikasi berdasarkan fitur yang direncanakan | Anggota 1 |
| Product Backlog & Sprint 1 Backlog | Menyusun daftar User Stories dan target Sprint 1 | Anggota 2 |
| Rancangan UX/UI | Membuat wireframe/mockup beranda, katalog, detail produk beserta viewer digital twin, keranjang, dan checkout | Anggota 3 |
| Rancangan Sistem | Membuat flowchart/diagram arsitektur/ERD (pengguna, produk, pesanan, transaksi, data digital twin) serta memilih library 3D (mis. Three.js/model-viewer) | Ketua/Anggota (dibagi) |
| Inisialisasi Kode Proyek | Setup struktur folder & boilerplate awal | Ketua |
