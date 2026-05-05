# StockMonitor Pro - Monitoring Stock Carton & Pallet

StockMonitor Pro adalah aplikasi web berbasis Progressive Web App (PWA) untuk memantau stok kardus, layer, dan palet besi secara real-time. Aplikasi ini mendukung mode offline (local storage) dan sinkronisasi ke Google Spreadsheet melalui Google Apps Script.

## Fitur Utama

- Dashboard ringkas untuk melihat total stok dan kondisi item (Layak/Tidak Layak).
- Transaksi stok masuk/keluar dengan validasi stok otomatis.
- Riwayat transaksi lengkap dengan filter, hapus data, dan export CSV.
- Snapshot stok mingguan (per minggu dalam bulan) dengan export CSV.
- Integrasi Google Spreadsheet (sinkronisasi data stok dan transaksi).
- PWA siap install ke home screen (Android/iOS) + Service Worker caching.
- Tema gelap/terang dengan preferensi tersimpan.

## Item yang Dimonitor

- Kardus Besar
- Kardus Kecil
- Layer Besar
- Layer Kecil
- Palet A1 ADM
- Palet 3D FLOOR

## Teknologi yang Digunakan

- HTML5
- CSS3 + Bootstrap 5
- JavaScript (Vanilla)
- Font Awesome
- Google Apps Script (backend sederhana untuk Spreadsheet)
- Service Worker + Web App Manifest (PWA)

## Struktur Proyek

```text
.
|- index.html
|- manifest.json
|- service-worker.js
|- css/
|  |- bootstrap*.css
|  |- custom.css
|- js/
|  |- app.js
|  |- bootstrap*.js
|- icons/
|  |- icon-192.png
|  |- icon-512.png
|  |- apple-touch-icon.png
|  |- splash-*.png
|- generate-splash.py
|- generate-splash.js
`- splash-generator.html
```

## Cara Menjalankan Lokal

Karena proyek ini menggunakan Service Worker, jalankan lewat server lokal (bukan buka file `index.html` langsung).

Contoh menggunakan Python:

```bash
python3 -m http.server 8000
```

Lalu buka:

```text
http://localhost:8000
```

## Integrasi Google Spreadsheet

1. Buka halaman **Pengaturan** di aplikasi.
2. Klik **Salin Kode Apps Script**, lalu tempelkan ke Google Apps Script pada Spreadsheet Anda.
3. Deploy Apps Script sebagai **Web App**.
4. Salin URL Web App, tempel ke input URL pada halaman Pengaturan, lalu simpan.

Disarankan menyiapkan sheet:

- `Stock`
- `Riwayat`
- `StockMingguan`

## Mode Penyimpanan Data

- **Offline/Lokal:** data disimpan di browser via `localStorage`.
- **Online/Sinkron:** transaksi dan snapshot mingguan dikirim ke Google Spreadsheet.

Jika sinkronisasi gagal, data tetap aman di penyimpanan lokal.

## PWA dan Deployment

Proyek ini dikonfigurasi memakai base path:

- `start_url`: `/Monitoring-Kardus/`
- `scope`: `/Monitoring-Kardus/`

Jika deploy di path berbeda, sesuaikan path di:

- `index.html` (manifest, icons, service worker register path)
- `manifest.json` (`id`, `start_url`, `scope`, path icon)
- `service-worker.js` (aset static yang di-cache)

## Generator Splash Screen iOS

Tersedia 3 opsi untuk membuat ulang splash screen iOS:

- Python script: `generate-splash.py` (Pillow)
- Node script: `generate-splash.js` (canvas)
- Tool browser: `splash-generator.html`

Semua generator menggunakan `icons/icon-512.png` sebagai sumber logo.

## Catatan Pengembangan

- Tidak membutuhkan proses build, aplikasi bersifat static-first.
- Gunakan cache versioning di `service-worker.js` setiap ada perubahan asset penting.
- Pastikan path asset konsisten dengan target hosting.

## Lisensi

Belum ditentukan. Tambahkan file `LICENSE` jika proyek akan dipublikasikan secara terbuka.
