### **1. Header & Akses Pengguna**
* **Navigasi Tab:** Terdiri dari 3 menu utama: *Estimasi Produksi*, *Perencanaan Mesin*, dan *Data Master*.
* **Tombol Login:** Terletak di pojok kanan atas.
    * **Mode Tamu (Default):** Hanya bisa melihat data, menghitung estimasi, dan melihat jadwal.
    * **Mode Admin:** Membuka fitur "tulis" (Input data baru, Edit, Hapus, Drag & Drop jadwal, Export PDF/Excel, Penjadwalan Otomatis).
    * *Password default: "admin123"*.

---

### **2. Menu 1: Estimasi Produksi (Tab Default)**
Fitur ini digunakan untuk menghitung berapa lama waktu yang dibutuhkan untuk menyelesaikan pesanan berdasarkan kapasitas mesin.

* **Input Pesanan (Daftar Pesanan):**
    * **Baris Input Dinamis:** Anda bisa memasukkan banyak jenis produk sekaligus.
    * **Tombol "+ Tambah Item Lain":** Menambah baris input baru untuk menghitung pesanan campuran (multi-item).
    * **Autocomplete Kode Produk:** Saat mengetik kode, sistem akan menyarankan produk yang ada di *Data Master* beserta mesin utamanya.
    * **Input Jumlah:** Masukkan jumlah pesanan dalam satuan Dus (Sistem otomatis mengonversi ke Pcs berdasarkan data master).
* **Tombol "Hitung Estimasi Produksi":** Melakukan kalkulasi total beban kerja.
* **Hasil Perhitungan:**
    * **Kartu Ringkasan:** Menampilkan Total Jam, Total Shift, dan Total Hari yang dibutuhkan.
    * **Detail Perhitungan:** Tabel rinci per produk (Target per shift, jam yang dibutuhkan, dll).
    * **Export PDF (Admin Only):** Mencetak hasil estimasi ke format PDF resmi dengan logo perusahaan.
* **Penjadwalan Otomatis (Admin Only):**
    * Muncul setelah estimasi dihitung.
    * **Simulasi Jadwal:** Sistem mencari slot kosong di mesin yang sesuai mulai dari "Tanggal Mulai Ideal" yang Anda input.
    * **Tombol Simpan:** Menyimpan hasil simulasi langsung ke database jadwal.

---

### **3. Menu 2: Perencanaan Mesin**
Fitur ini adalah visualisasi jadwal (Visual Control Board) untuk melihat beban kerja mesin.

* **Filter Tanggal:** Pilih "Tanggal Mulai" dan "Tanggal Akhir" untuk melihat matriks jadwal pada periode tertentu.
* **Form Input Slot Jadwal (Admin Only):**
    * Form manual untuk memasukkan jadwal satu per satu jika tidak menggunakan fitur otomatis.
    * Sistem otomatis mengecek ketersediaan mesin (mencegah bentrok jadwal).
* **Matriks Jadwal (Tabel Visual):**
    * **Kolom Sticky:** Nama Mesin dan Shift tetap terlihat saat tabel digeser ke kanan (scroll horizontal).
    * **Indikator Warna:**
        * **Merah Muda:** Hari libur/akhir pekan.
        * **Teks Merah:** Jadwal yang diletakkan di hari libur.
        * **Teks Biru/Hitam:** Jadwal normal.
    * **Drag & Drop (Admin Only):** Admin dapat memindahkan jadwal dari satu sel ke sel lain (misal: memindahkan dari Shift 1 ke Shift 2, atau ke tanggal lain) hanya dengan menarik (drag) item jadwal.
    * **Edit & Hapus Cepat (Admin Only):** Ikon pensil dan sampah muncul di setiap slot jadwal untuk pengeditan cepat.
* **Ringkasan Harian:** Di atas tabel, terdapat ringkasan utilisasi harian (berapa slot mesin yang aktif vs menganggur).
* **Export Excel:** Mengunduh tampilan matriks jadwal ke file `.xlsx`.

---

### **4. Menu 3: Data Master**
Pusat database aplikasi.

* **Panel Admin (Input Data Baru):**
    * Formulir untuk menambah produk baru ke database (Kode, Nama, Mesin Utama, Mesin Optional, Isi Dus, Target Shift).
    * Hanya muncul jika sudah login.
* **Tabel Data Master Produksi:**
    * Daftar semua produk yang terdaftar, kapasitas per shift, dan mesinnya.
    * Fitur Pencarian cepat.
    * **Aksi (Admin):** Edit data dan Hapus data produk.
* **Tabel Master Jadwal Mesin:**
    * Daftar "mentah" seluruh jadwal yang tersimpan di database (List View).
    * **Fitur Hapus Massal (Admin):** Checkbox untuk memilih banyak jadwal sekaligus dan menghapusnya secara bersamaan.
    * **Export Excel:** Mengunduh database jadwal lengkap.

---

### **5. Fitur Teknis & UX (User Experience)**
* **Validasi Jadwal:** Sistem akan memberi peringatan jika Anda mencoba menjadwalkan di mesin yang sudah penuh atau di hari libur (bisa di-bypass dengan konfirmasi).
* **Responsif:** Tampilan menyesuaikan layar (tabel bisa di-scroll horizontal pada layar kecil).
* **Supabase Realtime:** Data disimpan di cloud (Supabase), sehingga jika ada perubahan data di satu komputer, data di komputer lain juga akan terupdate (jika di-refresh/re-fetch).
