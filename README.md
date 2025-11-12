Berikut adalah rincian dari setiap fitur:

### Fitur Global & Admin

1.  **Sistem Login Admin:**
    * **Penjelasan:** Ini adalah fitur inti yang mengamankan aplikasi. Menggunakan kata sandi yang tersimpan di kode (`"admin123"`), fitur ini mengaktifkan atau menyembunyikan semua tombol dan formulir penting.
    * **Fungsi:** Mengontrol siapa yang dapat menambah, mengedit, atau menghapus data apa pun di seluruh aplikasi, serta siapa yang dapat mengakses fitur ekspor.

2.  **Notifikasi Real-time (Data Master Produksi):**
    * **Penjelasan:** Aplikasi secara otomatis "mendengarkan" perubahan pada tabel `production_rates` di Supabase.
    * **Fungsi:** Jika ada pengguna lain (atau Anda di tab lain) yang mengubah data master (misal, target shift), tabel di tab "Data Master" akan otomatis diperbarui tanpa perlu me-refresh halaman.

3.  **Notifikasi Umpan Balik (Pop-up):**
    * **Penjelasan:** Setiap kali Anda menyimpan, menghapus, atau mengalami error, sebuah kotak pesan (hijau untuk sukses, merah untuk error) akan muncul di bagian atas layar.
    * **Fungsi:** Memberi konfirmasi instan kepada pengguna atas tindakan mereka.

---

### Tampilan 1: Estimasi Produksi

1.  **Kalkulasi Estimasi Waktu:**
    * **Penjelasan:** Fitur utama di tab ini. Anda memasukkan "Kode Produk" dan "Jumlah Pesanan (Dus)".
    * **Fungsi:** Sistem akan mencari semua komponen yang terkait dengan kode itu di Data Master, menghitung total kebutuhan produksi (total pcs), dan membaginya dengan target per shift. Fitur ini melakukan simulasi mini (paralel/sekuensial) untuk memberikan estimasi Total Jam, Shift, dan Hari yang paling akurat.

2.  **Penjadwalan Otomatis (Simulasi):**
    * **Penjelasan:** Setelah estimasi dihitung, Admin dapat memasukkan "Tanggal Mulai" dan mengklik "Jadwalkan Otomatis".
    * **Fungsi:** Ini adalah algoritma paling canggih di web ini. Ia akan mengambil komponen dari hasil estimasi dan mencoba menempatkannya di jadwal 60 hari ke depan. Ia menggunakan **Logika Konsistensi Mesin** (1 komponen = 1 mesin) dan akan otomatis mencari di mesin opsional jika mesin utama penuh.

3.  **Simpan Jadwal Otomatis ke Database:**
    * **Penjelasan:** Setelah simulasi berhasil, sebuah link "KLIK DI SINI" akan muncul.
    * **Fungsi:** Saat diklik, semua slot yang diusulkan oleh simulasi akan disimpan secara massal ke database Supabase (`production_schedule`) dan Anda akan otomatis diarahkan ke tab Perencanaan Mesin.

4.  **Export Estimasi ke PDF:**
    * **Penjelasan:** Tombol "Export PDF" (hanya Admin) akan muncul setelah estimasi dihitung.
    * **Fungsi:** Mengambil "screenshot" dari area hasil (kartu ringkasan dan tabel rincian), menambahkan logo dan judul, lalu membuatnya menjadi file PDF yang rapi untuk diunduh atau dicetak.

---

### Tampilan 2: Perencanaan Mesin

1.  **Matriks Jadwal Dinamis:**
    * **Penjelasan:** Fitur inti dari tab ini. Anda memilih rentang "Tanggal Mulai" dan "Tanggal Akhir".
    * **Fungsi:** Sistem akan mengambil semua data jadwal yang ada di Supabase dalam rentang tanggal tersebut dan me-render sebuah tabel matriks besar yang menunjukkan semua mesin (baris) dan semua hari/shift (kolom). Slot yang terisi akan menampilkan Kode Produk.

2.  **Ringkasan Beban Harian:**
    * **Penjelasan:** Di atas tabel matriks, terdapat kartu-kartu kecil untuk setiap hari.
    * **Fungsi:** Memberikan gambaran cepat (visual) tentang seberapa penuh kapasitas pabrik setiap hari (menghitung slot "ON" vs "OFF" dan persentase utilisasi).

3.  **Input & Edit Jadwal Manual (Admin):**
    * **Penjelasan:** Admin memiliki akses ke formulir input di atas tabel dan tombol "Edit" (ikon pensil) di dalam setiap slot yang terisi.
    * **Fungsi:** Memungkinkan Admin untuk menambah, mengedit, atau menghapus slot jadwal satu per satu secara manual. Fitur ini memiliki pengecekan konflik (memberi tahu jika slot penuh) dan validasi mesin (memeriksa apakah produk valid untuk mesin itu).

4.  **Export Matriks ke Excel:**
    * **Penjelasan:** Tombol "Export Excel" (hanya Admin) muncul bersamaan dengan tabel matriks.
    * **Fungsi:** Mengonversi seluruh tabel matriks yang sedang Anda lihat (termasuk `rowspan`) menjadi file `.xlsx` yang terformat, lengkap dengan *styling* (misalnya, slot "LIBUR" berwarna merah).

---

### Tampilan 3: Data Master

1.  **Manajemen Data Produksi (CRUD):**
    * **Penjelasan:** Menampilkan tabel `production_rates` (semua data tarif produksi Anda).
    * **Fungsi:** Admin dapat melakukan **C**reate (lewat form di tab Estimasi), **R**ead (melihat tabel), **U**pdate (tombol Edit), dan **D**elete (tombol Hapus) untuk semua data master produksi. Ini adalah "otak" dari semua perhitungan.

2.  **Manajemen Data Jadwal (Log):**
    * **Penjelasan:** Menampilkan tabel `production_schedule` (semua slot yang pernah dijadwalkan).
    * **Fungsi:** Berfungsi sebagai *log* data. Fitur utamanya adalah **Hapus Multi-Jadwal**, di mana Admin dapat mencentang beberapa slot jadwal sekaligus (bahkan setelah difilter) dan menghapusnya secara massal dari database.

3.  **Pencarian Cepat:**
    * **Penjelasan:** Terdapat bar pencarian di atas kedua tabel di tab Data Master.
    * **Fungsi:** Memfilter kedua tabel secara instan saat Anda mengetik, memudahkan pencarian data spesifik.
