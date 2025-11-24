Website **Estimasi Produksi & Perencanaan Mesin** ini adalah aplikasi web terintegrasi yang dirancang untuk membantu PPIC (Production Planning and Inventory Control) atau manajer produksi dalam menghitung estimasi waktu produksi dan menjadwalkan penggunaan mesin secara visual.

Berikut adalah penjelasan detail mengenai fitur-fitur yang tersedia beserta fungsinya, dibagi berdasarkan menu/tab utama:

### 1. Mode Pengguna & Keamanan
* **Login Admin:**
    * **Fungsi:** Mengamankan data sensitif dan mencegah perubahan tidak sah.
    * **Fitur:** Tombol login di pojok kanan atas. Ketika login (password default di kode: `admin123`), pengguna mendapatkan akses penuh untuk menambah/mengedit/menghapus data, melakukan *drag-and-drop* jadwal, dan input manual. Pengguna tamu (tanpa login) hanya bisa melihat data (read-only).

### 2. Tab Estimasi Produksi (Halaman Utama)
Fitur ini digunakan untuk menghitung berapa lama waktu yang dibutuhkan untuk menyelesaikan pesanan tertentu.

* **Kalkulator Estimasi Multi-Item:**
    * **Fungsi:** Menghitung total jam, shift, dan hari yang dibutuhkan berdasarkan target produksi per shift yang tersimpan di Data Master.
    * **Cara Kerja:** Pengguna memasukkan Kode Produk dan Jumlah Pesanan (dalam Dus). Sistem otomatis menarik data *pcs per box* dan *target per shift*, lalu menghitung beban kerjanya.
* **Penjadwalan Otomatis (Simulasi):**
    * **Fungsi:** Mencari slot kosong secara otomatis di mesin yang sesuai mulai dari tanggal yang diinginkan.
    * **Cara Kerja:** Setelah estimasi dihitung, admin bisa mengklik "Jadwalkan Otomatis". Sistem akan memindai database jadwal, melewati slot yang sudah terisi, dan menyarankan slot waktu untuk produksi tersebut.
* **Export PDF:**
    * **Fungsi:** Membuat laporan resmi hasil estimasi.
    * **Fitur:** Menghasilkan file PDF yang berisi ringkasan total waktu dan rincian per item, lengkap dengan kop surat/logo perusahaan.

### 3. Tab Perencanaan Mesin (Planning Board)
Ini adalah "Jantung" dari aplikasi, berupa matriks visual (Gantt Chart sederhana) untuk memantau beban kerja mesin.

* **Matriks Jadwal (Visualisasi):**
    * **Fungsi:** Melihat ketersediaan mesin secara *real-time*.
    * **Tampilan:** Baris mewakili Mesin, Kolom mewakili Tanggal & Shift.
    * **Indikator:**
        * **Warna Putih:** Slot Kosong (Available).
        * **Teks Tebal:** Slot Terisi (menampilkan Kode Produk).
        * **Warna Merah:** Hari Libur/Akhir Pekan (Weekend).
* **Drag & Drop Jadwal (Fitur Admin):**
    * **Fungsi:** Memindahkan jadwal dengan cepat tanpa input ulang.
    * **Fitur:** Admin dapat menyeret (drag) kotak jadwal dari satu tanggal/shift ke tanggal/shift lain. Fitur ini juga mendukung **Swap (Tukar Posisi)** jika slot tujuan sudah terisi, dengan konfirmasi pop-up.
* **Input Manual & Validasi Konflik:**
    * **Fungsi:** Menambahkan jadwal secara manual.
    * **Validasi:** Sistem akan mengecek apakah mesin tersebut sudah penuh di tanggal/shift yang dipilih. Sistem juga akan memberi peringatan jika pengguna mencoba menjadwalkan di hari libur.
* **Export Excel:**
    * **Fungsi:** Mengunduh tampilan matriks jadwal ke dalam format `.xlsx` untuk keperluan laporan fisik atau arsip.

### 4. Tab Data Master
Pusat database untuk mengelola standar produksi dan data referensi.

* **Manajemen Produk (CRUD):**
    * **Fungsi:** Menyimpan data standar setiap produk.
    * **Data yang Disimpan:** Kode Barang, Nama Komponen, Mesin Utama, Mesin Optional, Isi per Dus, dan Target Output per Shift.
    * **Kapasitas:** Menghitung otomatis kapasitas produksi dalam 3 shift.
* **Manajemen Jadwal Terpusat (List View):**
    * **Fungsi:** Melihat seluruh daftar jadwal dalam bentuk tabel (bukan matriks).
    * **Fitur:** Pencarian (Search), Hapus Massal (Multi-delete), dan Export Data Jadwal ke Excel.

### 5. Fitur Teknis & UX (User Experience)
* **Database Cloud (Supabase):** Data tersimpan secara online/persisten, sehingga tidak hilang saat browser di-refresh.
* **Responsif:** Tampilan menyesuaikan layar (desktop atau mobile).
* **Sticky Header:** Saat menggulir tabel jadwal yang panjang, nama mesin (kiri) dan tanggal (atas) tetap terlihat agar pengguna tidak bingung membaca data.
* **Pencarian Real-time:** Fitur pencarian di Data Master langsung menyaring data saat pengguna mengetik.
