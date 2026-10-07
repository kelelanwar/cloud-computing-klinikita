# PRODUCT REQUIREMENTS DOCUMENT (PRD)
# SISTEM MANAJEMEN RUMAH SAKIT & KLINIK "KLINIKITA"
**Mata Kuliah:** Cloud Computing  
**Nama Produk:** Klinikita (Smart Hospital & Clinic Management System)  
**Versi Dokumen:** 1.0.0  
**Status:** Approved / Development Ready  
**Tanggal:** Oktober 2026  

---

## 1. EXECUTIVE SUMMARY & IDENTITAS PRODUK

### 1.1 Latar Belakang
Dalam era transformasi digital dan komputasi awan (*Cloud Computing*), fasilitas pelayanan kesehatan dituntut untuk menyajikan integrasi data yang cepat, handal, transparan, dan mudah diakses oleh pasien maupun tenaga medis. **Klinikita** dirancang sebagai solusi *web-based Hospital & Clinic Management System* modern yang mengonsolidasikan seluruh siklus operasional klinik—mulai dari pendaftaran pasien mandiri, pemantauan antrean *real-time*, manajemen jadwal dokter, estimasi kalkulasi biaya transparan, hingga pelaporan transaksi dan rekapitulasi medis berbasis cloud.

### 1.2 Identitas Website & Nilai Inti
- **Nama Platform:** Klinikita
- **Tagline:** *"Modern Healthcare at Your Fingertips — Solusi Cerdas Manajemen Klinik Terintegrasi Cloud"*
- **Tema Desain Visual:** Mengadopsi bahasa visual medis terpercaya berbasis tema *MedService Template* dengan palet warna dominan *Steel Blue* (`#1d3557` / `#2b3990`), *Medical Cyan/Blue* (`#0284c7` / `#00a3c8`), latar belakang *Soft Grey* higienis (`#f8fafc`), serta aksen hijau sukses (`#10b981`) dan merah darurat (`#ef4444`).
- **Target Pengguna:**
  1. **Pasien / Pengunjung Umum:** Melakukan registrasi online, cek jadwal dokter, kalkulasi estimasi biaya pengobatan, dan memantau antrean secara live.
  2. **Petugas Medis / Admin:** Mengelola alur pendaftaran, memanggil nomor antrean, memantau utilisasi poli dan tempat tidur, serta menganalisis laporan data transaksi.

---

## 2. ARSITEKTUR TEKNOLOGI & BATASAN SISTEM (SYSTEM CONSTRAINTS)

Berdasarkan spesifikasi teknis proyek Cloud Computing Klinikita:
1. **Zero External CSS/JS File Constraint:** Sistem dibangun murni menggunakan 5 berkas `.html` mandiri tanpa berkas terpisah `.css` maupun `.js`. Seluruh *styling* dan *scripting* disematkan secara *inline* (*embedded*) di dalam setiap berkas HTML.
2. **Framework CSS via CDN:** Menggunakan **Tailwind CSS CDN** (`https://cdn.tailwindcss.com`) dengan kustomisasi konfigurasi tema MedService warna korporat medis.
3. **Penyedia Aset & Grafis Cloud:**
   - Ikonografi: Font Awesome 6 CDN (`https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css`).
   - Visual & Banner: Unsplash Cloud Image CDN dengan parameter optimasi resolusi dan webp compression.
   - Grafik Interaktif: Chart.js CDN (`https://cdn.jsdelivr.net/npm/chart.js`).
   - Notifikasi & Alert: SweetAlert2 CDN (`https://cdn.jsdelivr.net/npm/sweetalert2@11`).
   - Animasi UI: Animate On Scroll (AOS) CDN (`https://unpkg.com/aos@2.3.1/dist/aos.js` & `aos.css`).
4. **Mekanisme Autentikasi Role-Based:**
   - Autentikasi berbasis status sesi peramban (*Client-Side Session Storage & LocalStorage*).
   - Menampilkan menu `dashboard.html` dan `laporan-data.html` **hanya** jika terautentikasi sebagai **Admin**.
   - Menyembunyikan menu restricted jika pengguna berstatus Tamu/Pasien.
   - Dilengkapi *Route Guard*: redirect ramah dengan modal login cepat jika URL rahasia diakses langsung sebelum login.
   - **Kredensial Demo Admin:**
     - Email / Username: `admin@klinikita.id` (atau `admin`)
     - Password: `admin123`
   - **Kredensial Demo Pasien:**
     - Email / Username: `pasien@klinikita.id`
     - Password: `pasien123`
5. **Kepatuhan SEO & Keamanan:**
   - Wajib menyertakan meta tag: `<meta name="robots" content="noindex, nofollow">` pada seluruh 5 berkas HTML untuk mencegah indeksasi publik data simulasi internal klinik.

---

## 3. STRUKTUR DAN FUNGSI 5 BERKAS HTML UTAMA

| No | Nama Berkas | Peran / Kategori | Fungsi Spesifik |
|:---|:---|:---|:---|
| 1 | `index.html` | **Landing Page & Portal Hub Utama** | Gerbang utama informasi publik Klinikita, perkenalan profil klinik berstandar MedService, jam operasional darurat, counter pencapaian klinik, live preview antrean, ikhtisar poli, dan modal login sentral. |
| 2 | `dashboard.html` | **Tampilan Utama Sistem Berbasis Tema** *(Protected - Admin Only)* | Antarmuka pusat kendali klinik (*executive clinical dashboard*), metrik kunjungan, live occupancy bed rawat inap, status dokter aktif, visualisasi beban poli (Chart.js), dan monitor antrean aktif. |
| 3 | `fitur-sistem.html` | **Modul Fitur Interaktif** *(Public & Interactive)* | Area simulasi kerja 4 fitur utama: (1) Form Pendaftaran Pasien Mandiri & Generate No. Antrean, (2) Jadwal Dokter Dinamis dengan filter poli, (3) Kalkulator Estimasi Biaya Medis Transparan, (4) Simulator Pemanggilan Antrean dengan Audio Chime Synth. |
| 4 | `detail-layanan.html` | **Modul Fitur Pendukung** | Katalog komprehensif poliklinik (Umum, Gigi, Anak, Penyakit Dalam, dll.), paket Medical Check-Up (MCU), fasilitas penunjang medis (UGD 24 Jam, Farmasi Digital, Ambulans Cloud Fleet, Lab Patologi), dan FAQ pasien. |
| 5 | `laporan-data.html` | **Modul Rekapitulasi & Riwayat Transaksi** *(Protected - Admin Only)* | Rekapitulasi data transaksi keuangan, log riwayat kunjungan antrean pasien, filter rentang tanggal, ringkasan pendapatan harian/bulanan, fitur cetak invoice/laporan (*Print View*), dan ekspor data langsung ke file CSV/Excel. |

---

## 4. SPESIFIKASI FITUR FUNGSIONAL UTAMA

### 4.1 Dashboard Layanan (`dashboard.html`)
- **Metrik KPI Utama:** 4 Kartu indikator: Total Kunjungan Pasien Hari Ini, Antrean Sedang Berjalan, Dokter Spesialis Bertugas, Estimasi Pendapatan Harian.
- **Grafik Beban Pelayanan:** Chart batang/garis interaktif mingguan untuk tren kunjungan rawat jalan vs rawat inap.
- **Grafik Distribusi Poli:** Chart donat menunjukkan persentase kunjungan di Poli Umum, Spesialis Anak, Gigi, Penyakit Dalam, dan UGD.
- **Live Queue Controller:** Tabel antrean aktif dengan aksi: *Panggil Pasien*, *Selesai Dilayani*, dan *Lewati Antrean*.
- **Indikator Cloud Sync:** Tampilan status konektivitas cloud node (Cloud Computing simulation).

### 4.2 Pendaftaran Pasien Online (`fitur-sistem.html` - Modul 1)
- Form registrasi pasien baru/lama: NIK, Nama Lengkap, No. Telepon, Jenis Kelamin, Tanggal Kunjungan, Pilihan Poliklinik, Pilihan Dokter Spesialis, dan Metode Penjamin (Umum / BPJS / Asuransi Swasta).
- Validasi data instan dan penyimpanan ke *LocalStorage*.
- Pencetakan tiket pendaftaran digital dengan barcode/QR mock-up dan nomor antrean berurutan otomatis (A-001, B-001, dsb.).

### 4.3 Jadwal Dokter (`fitur-sistem.html` - Modul 2 & `detail-layanan.html`)
- Grid interaktif dokter spesialis dengan foto berstandar MedService, spesialisasi, hari praktik, dan jam operasional.
- Filter pencarian instan berdasarkan poliklinik.
- Indikator status kehadiran *real-time*: "Sedang Praktik", "Tersedia", atau "Selesai".
- Aksi langsung: Tombol "Pilih & Buat Janji" yang langsung mengisi poli dan dokter di form registrasi.

### 4.4 Kalkulator Biaya Medis Transparan (`fitur-sistem.html` - Modul 3)
- Kalkulator dinamis multi-komponen:
  - Biaya Administrasi & Konsultasi Dokter (Umum, Spesialis, Sub-Spesialis).
  - Pilihan Tindakan Medis Tambahan (Cek Darah Lengkap, Rontgen Thorax, USG 4D, Nebulizer, EKG Jantung, Tambal Gigi Estetik).
  - Pemilihan Akomodasi/Perawatan (Rawat Jalan, Rawat Inap Kelas III, Kelas II, Kelas I, VIP Deluxe).
  - Skema Penjaminan (Mandiri/Umum diskon 0%, Asuransi Rekanan diskon 80%, BPJS Kesehatan cover 100% item tertentu).
- Rincian kalkulasi instan (*live breakdown calculation*) dan tombol "Simpan Estimasi" atau "Cetak Rincian".

### 4.5 Sistem Manajemen Antrean Live (`fitur-sistem.html` - Modul 4)
- Display layar antrean ala monitor rumah sakit besar dengan display nomor yang sedang dipanggil per poli.
- Dilengkapi efek suara audio synthesizer web (*chime notification*) saat nomor antrean dipanggil.
- Mode Kiosk Mandiri: Pasien dapat mengambil nomor antrean baru hanya dengan 1 klik.
- Sinkronisasi status antrean antara modul pendaftaran, antrean display, dan dashboard admin.

### 4.6 Rekapitulasi & Riwayat Transaksi (`laporan-data.html`)
- Tabel data dinamis transaksi pasien: ID Registrasi, Waktu Kunjungan, Nama Pasien, Poli, Dokter, Total Biaya, Status Pembayaran (Lunas/Klaim Asuransi), dan Aksi.
- Filter pencarian kata kunci dan filter status pembayaran.
- Tombol **Ekspor CSV** (mengunduh berkas `.csv` langsung di browser tanpa backend) dan **Print Report** (cetak PDF ramah printer).
- Fitur reset data simulasi kembali ke kondisi default.

---

## 5. DESAIN SISTEM VISUAL & IDENTITAS MEDSERVICE

Sistem mengadopsi standar visual template medis MedService:
- **Header Top Strip:** Menampilkan nomor darurat 24 jam (`(021) 500-KLINIK / 0812-3456-7890`), alamat lokasi, jam operasional, dan info integrasi Cloud Node.
- **Navigasi Utama:**
  - Logo Klinikita (Ikon Palang Medis Modern + Tipografi Tegas).
  - Menu Publik: Beranda (`index.html`), Simulasi Fitur (`fitur-sistem.html`), Detail Layanan (`detail-layanan.html`).
  - Menu Admin (Khusus Login): Dashboard (`dashboard.html`), Laporan Data (`laporan-data.html`).
  - Tombol Autentikasi Dinamis: Jika belum login menampilkan tombol `Masuk (Login Demo)`, jika sudah login menampilkan `Admin (Logout)`.
- **Palet Warna:**
  - `primary-dark`: `#1d3557` (Steel Blue korporat)
  - `primary-blue`: `#0284c7` (Medical Blue)
  - `primary-hover`: `#0369a1` (Darker Sky)
  - `accent-cyan`: `#06b6d4`
  - `bg-light`: `#f8fafc` & `#f1f5f9` (Soft Hospital White)
  - `text-dark`: `#1e293b` & `#334155`
  - `emergency-red`: `#dc2626`
- **Tipografi:** Menggunakan Google Fonts *Roboto* dan *Lato* untuk keterbacaan tinggi data klinis.

---

## 6. MEKANISME KEAMANAN & AUTENTIKASI DEMO

1. **Tag Wajib SEO:**
   ```html
   <meta name="robots" content="noindex, nofollow">
   ```
2. **Session Persistence:**
   Disimpan di `localStorage.getItem('klinikita_session')`:
   - Jika terisi `{"role":"admin", "name":"Administrator Klinikita"}`:
     - Menu `dashboard.html` dan `laporan-data.html` ditampilkan di navbar dan mobile menu.
     - Akses halaman `dashboard.html` dan `laporan-data.html` diizinkan penuh.
   - Jika kosong atau `role !== "admin"`:
     - Menu `dashboard.html` dan `laporan-data.html` disembunyikan.
     - Jika pengguna membuka langsung file `dashboard.html` atau `laporan-data.html`, script akan menampilkan layar pelindung (*Access Protected Modal*) dan menawarkan tombol login cepat dengan akun demo admin.
3. **Akun Demo Login Tersedia:**
   - **Admin:** `admin@klinikita.id` | Sandi: `admin123`
   - **Pasien:** `pasien@klinikita.id` | Sandi: `pasien123`

---

## 7. 10 TAHAPAN DEVELOPMENT & PANDUAN EKSEKUSI BUILD

Berikut adalah 10 tahapan terstruktur untuk membangun dan memverifikasi platform Klinikita dari awal hingga siap dipresentasikan:

### Tahap 1: Inisialisasi Arsitektur & Perancangan Desain Berbasis MedService
- Menetapkan skema warna korporat (*Steel Blue* `#1d3557`, *Medical Blue* `#0284c7`, *Soft White* `#f8fafc`).
- Menyiapkan CDN dependencies: Tailwind CSS, FontAwesome 6, Google Fonts (Roboto & Lato), SweetAlert2, Chart.js, dan AOS Animation.
- Menentukan standar layout master: Header Top Strip, Main Navigasi Responsif, Footer Informatif 4-Kolom.
- Memastikan tag `<meta name="robots" content="noindex, nofollow">` menjadi template standar.

### Tahap 2: Pembangunan Core Shared State & Modul Autentikasi Client-Side
- Merancang modul JavaScript *inline* untuk pengelolaan `localStorage` (`klinikita_session`, `klinikita_patients`, `klinikita_queues`, `klinikita_transactions`).
- Mengimplementasikan fungsi *login helper*, *logout handler*, dan *checkAuthStatus()* yang sinkron di seluruh halaman.
- Membuat komponen modal login interaktif yang dapat dipanggil dari header di kelima file HTML.
- Menyediakan tombol cepat "Gunakan Akun Demo Admin" untuk pengujian tanpa repot mengetik.

### Tahap 3: Konstruksi `index.html` (Landing Page & Portal Hub Utama)
- Membangun Top Header Strip lengkap dengan info kontak darurat, alamat, dan indikator cloud status.
- Membangun Hero Section bertema MedService dengan tajuk utama kesehatan dan tombol aksi cepat (*Book Appointment*).
- Menambahkan 4 Info Box Cepat: Jam Kerja Poliklinik, Jadwal Dokter, Pendaftaran Online, dan Kontak Darurat 24 Jam.
- Membangun blok statistik pencapaian klinik (Pasien, Dokter, Kamar, Kepuasan).
- Menyematkan widget Live Antrean Mini agar pengunjung beranda dapat melihat nomor antrean terkini.
- Menyusun Showcase Departemen / Poliklinik dan Testimonial Pasien.

### Tahap 4: Konstruksi `fitur-sistem.html` — Modul 1 & 2 (Pendaftaran Pasien & Jadwal Dokter)
- Mengembangkan Tab Navigasi Fitur Interaktif dengan animasi transisi mulus.
- Membangun form registrasi pasien lengkap dengan kalkulasi nomor antrean otomatis berdasarkan poli yang dipilih.
- Menyimpan data pendaftaran baru ke `localStorage` agar sinkron dengan antrean dan laporan.
- Membuat kartu digital jadwal dokter dengan filter poliklinik dan tombol aksi reservasi langsung ke form.

### Tahap 5: Konstruksi `fitur-sistem.html` — Modul 3 & 4 (Kalkulator Biaya & Simulator Antrean Live)
- Membangun Kalkulator Biaya Medis Transparan dengan *real-time calculation engine*: tarif dokter + tindakan medis + kelas rawat inap - subsidi asuransi.
- Menyediakan tombol "Cetak Estimasi" dan "Simpan ke Rekap".
- Membangun Display Antrean Interaktif dengan audio synthesizer Web Audio API untuk efek suara panggilan bel klinik ("Ting Tung").
- Menyediakan tombol interaktif "Panggil Nomor Berikutnya", "Lewati", dan "Ambil Antrean Baru (Kiosk Pasien)".

### Tahap 6: Konstruksi `dashboard.html` (Tampilan Utama Sistem Berbasis Tema - Admin Protected)
- Memasang *Route Guard* autentikasi: proteksi halaman jika pengguna belum terautentikasi sebagai Admin.
- Membuat 4 Kartu KPI Ringkasan Eksekutif: Kunjungan Hari Ini, Antrean Berjalan, Dokter Aktif, dan Pendapatan Harian.
- Mengintegrasikan Chart.js CDN untuk grafik mingguan kunjungan pasien dan grafik donat utilisasi poliklinik.
- Menyusun tabel kontrol antrean pasien *live* dengan tombol aksi status (Panggil, Selesai, Lewati).
- Menampilkan status ketersediaan tempat tidur (Bed Management) dan simulasi node Cloud Computing.

### Tahap 7: Konstruksi `detail-layanan.html` (Modul Fitur Pendukung & Fasilitas Medis)
- Membangun katalog lengkap poliklinik spesialis dengan rincian tindakan medis dan dokter penanggung jawab.
- Menampilkan paket Medical Check-Up (MCU Basic, MCU Eksekutif, MCU Jantung, MCU Ibu & Anak) beserta rincian fasilitasnya.
- Menyusun galeri fasilitas penunjang medis (UGD 24 Jam, Radiologi Digital, Laboratorium Otomatis, Ambulans Cloud Dispatch).
- Menyediakan bagian FAQ interaktif (akordeon) dan formulir konsultasi cepat.

### Tahap 8: Konstruksi `laporan-data.html` (Modul Rekapitulasi & Riwayat Transaksi - Admin Protected)
- Memasang *Route Guard* autentikasi khusus Admin.
- Menyusun tabel rekapitulasi data transaksi dan kunjungan pasien dengan filter rentang tanggal dan pencarian.
- Mengintegrasikan fungsi **Ekspor CSV** di sisi klien agar laporan dapat diunduh langsung menjadi file spreadsheet.
- Membuat fitur **Cetak Laporan / Print View** yang dioptimasi khusus untuk format cetak printer/PDF.
- Menyediakan ringkasan total pendapatan dan statistik metode pembayaran (BPJS vs Tunai vs Asuransi Swasta).

### Tahap 9: Integrasi Data Antar-Modul & Verifikasi Navigasi Terpadu
- Memastikan navigasi navbar dan footer di kelima file HTML konsisten 100%.
- Menguji alur end-to-end:
  *Pendaftaran pasien di `fitur-sistem.html` -> Muncul di Antrean `fitur-sistem.html` -> Muncul di Dashboard `dashboard.html` -> Tercatat di Laporan Transaksi `laporan-data.html`*.
- Memverifikasi perilaku tampilan menu saat status:
  - **Belum Login (Guest):** Menu Dashboard & Laporan Data tersembunyi.
  - **Login Admin:** Menu Dashboard & Laporan Data tampil di navigasi.

### Tahap 10: Pengujian Cross-Browser, Responsivitas Mobile, dan Finalisasi
- Melakukan audit responsivitas pada resolusi Mobile (375px), Tablet (768px), dan Desktop (1200px+).
- Memastikan tidak ada berkas `.js` dan `.css` terpisah di repositori (memenuhi Aturan 3).
- Memverifikasi keberadaan tag `<meta name="robots" content="noindex, nofollow">` pada kelima berkas HTML (memenuhi Aturan 6).
- Melakukan verifikasi seluruh CDN asset (gambar Unsplash, ikon FontAwesome, Chart.js, SweetAlert2, Tailwind) dapat dimuat dengan cepat dan stabil.

---

## 8. MATRIKS TRACEABILITY PERSYARATAN & FITUR

| Persyaratan User | Berkas Terkait | Status Implementasi |
|:---|:---|:---|
| Landing Page & Portal Hub | `index.html` | Selesai & Terintegrasi |
| Tampilan Utama Dashboard | `dashboard.html` | Selesai (Chart.js & Live Queue) |
| Fitur Interaktif (Daftar, Jadwal, Biaya, Antrean) | `fitur-sistem.html` | Selesai (4 Modul Simulasi) |
| Modul Fitur Pendukung & Layanan | `detail-layanan.html` | Selesai (Poli, MCU, Fasilitas, FAQ) |
| Modul Rekapitulasi & Laporan | `laporan-data.html` | Selesai (Ekspor CSV, Filter, Print) |
| Tailwind CSS via CDN | Semua file HTML | Selesai via cdn.tailwindcss.com |
| Gambar & Ikon Cloud CDN | Semua file HTML | Unsplash & FontAwesome 6 |
| Tanpa file terpisah `.js` dan `.css` | Repositori Klinikita | Terpenuhi (Hanya berkas HTML) |
| Animasi Website via CDN | Semua file HTML | AOS & CSS transitions |
| Autentikasi Demo (Admin vs Tamu) | Semua file HTML | Terpasang dengan LocalStorage & Modal |
| Tag SEO Wajib `noindex, nofollow` | Semua 5 file HTML | Terpasang pada `<head>` |
| 10 Tahapan Development Markdown | `PRD-KLINIKITA.md` | Dokumen ini |
| Desain & Skema Warna MedService | Semua file HTML | Steel Blue, Medical Cyan, Soft Grey |

---
*Dokumen ini merupakan panduan resmi spesifikasi produk dan acuan implementasi kode sumber Klinikita.*

