Laporan Fitur & Fungsi: Estimasi Produksi & Perencanaan Mesin

1. Pendahuluan

Aplikasi web ini dirancang sebagai alat bantu komprehensif untuk Manufaktur (PPIC/Produksi) yang berfungsi untuk:

Mengestimasi kebutuhan waktu produksi (jam, shift, hari) berdasarkan pesanan.

Merencanakan dan memvisualisasikan alokasi jadwal pada mesin-mesin produksi.

Mengelola data master yang menjadi dasar semua perhitungan.

Aplikasi ini terhubung langsung ke database Supabase untuk pengelolaan data yang persisten dan (pada Data Master) real-time.

2. Fitur Utama (Berdasarkan Tampilan/Tab)

Fungsionalitas aplikasi dibagi menjadi tiga tab utama untuk alur kerja yang jelas.

A. Tab: Estimasi Produksi (Tampilan Utama)

Ini adalah halaman awal dan pusat kalkulasi.

Formulir Estimasi (Untuk Umum & Admin):

Input Kode Produk: Pengguna memasukkan kode produk (misal: "309MM"). Sistem menyediakan autocomplete dari Data Master.

Input Jumlah Pesanan (Dus): Pengguna memasukkan jumlah pesanan dalam satuan dus.

Tombol "Hitung Estimasi Produksi":

Fungsi: Memicu kalkulasi inti.

Logika Cerdas: Sistem mengambil semua komponen yang terkait dengan "309MM" dari Data Master. Sistem melakukan simulasi mini untuk menghitung total waktu, dengan mempertimbangkan komponen yang berjalan paralel di mesin berbeda dan komponen yang berjalan sekuensial (antri) di mesin yang sama.

Output: Menampilkan 3 kartu hasil utama (Total Jam, Total Shift, Total Hari) yang sudah dibulatkan.

Panel Hasil & Detail:

Tabel Detail Perhitungan: Muncul setelah estimasi, dapat disembunyikan/ditampilkan. Merinci perhitungan untuk setiap komponen (Total PCS, Target Shift, Kebutuhan Shift Murni (desimal), Kebutuhan Jam).

Tombol Export PDF (Hanya Admin): Admin dapat mengunduh laporan PDF dari hasil estimasi dan rincian perhitungannya. Laporan ini menyertakan logo perusahaan dan format yang rapi untuk dibagikan.

Panel Penjadwalan Otomatis (Hanya Admin):

Daftar Pilihan Komponen (Checklist): Fitur ini memungkinkan Admin untuk memilih komponen mana saja dari hasil estimasi yang ingin dijadwalkan. Secara default, semua komponen terpilih.

Input Tanggal Mulai: Admin memilih tanggal dimulainya produksi.

Tombol "Jadwalkan Otomatis":

Fungsi: Memicu simulasi penjadwalan hanya untuk komponen yang dicentang.

Logika: Sistem akan mencari slot kosong (Senin-Jumat) di mesin utama (atau mesin opsional jika utama penuh) secara konsisten untuk setiap komponen, mulai dari tanggal yang dipilih.

Output: Menampilkan ringkasan simulasi (misal: "3 dari 3 komponen terjadwal, selesai pada [Tanggal]") dan sebuah link konfirmasi.

Konfirmasi Simpan: Mengklik link "KLIK DI SINI" akan menyimpan semua slot yang disimulasikan ke database (Tabel production_schedule).

Panel Penjadwalan (Pengguna Biasa):

Fungsi: Jika pengguna bukan Admin, panel ini berubah fungsi. Input tanggal mulai di sini akan berfungsi sebagai pintasan (shortcut) untuk melihat jadwal 7 hari ke depan di Tab "Perencanaan Mesin".

B. Tab: Perencanaan Mesin

Tab ini berfokus pada visualisasi dan manajemen slot jadwal yang sudah ada.

Formulir Periode Tanggal (Untuk Umum & Admin):

Fungsi: Pengguna memasukkan rentang tanggal (Mulai dan Akhir) untuk melihat matriks jadwal. Jika tanggal akhir dikosongkan, sistem otomatis mengaturnya ke 7 hari setelah tanggal mulai.

Formulir Input Slot Jadwal (Hanya Admin):

Fungsi: Memungkinkan Admin untuk memesan (booking) satu slot jadwal secara manual.

Fitur Cerdas:

Auto-fill Komponen: Admin mengisi Kode Barang, dan sistem otomatis mengisi dropdown Nama Komponen.

Auto-fill Mesin: Setelah Nama Komponen dipilih, sistem otomatis memilih Mesin Utama yang sesuai.

Validasi Hari Libur: Jika Admin memilih tanggal di hari Sabtu/Minggu, sistem otomatis memindahkannya ke hari Senin berikutnya saat disimpan.

Validasi Slot: Sistem akan menampilkan status real-time ("Slot Tersedia", "Slot Penuh", atau "Dialihkan ke Mesin Opsional") sebelum Admin menekan simpan.

Matriks Jadwal (Tabel Utama):

Visualisasi: Menampilkan tabel besar dengan Mesin di baris dan Tanggal di kolom.

Kolom "Sticky": Kolom "Mesin" dan "Shift" akan tetap terlihat (terkunci) saat pengguna melakukan scroll horizontal.

Visualisasi Slot:

Slot Terisi: Menampilkan Kode Barang dan Nama Komponen.

Slot Kosong: Ditandai "Slot Kosong".

Hari Libur: Sel di hari Sabtu/Minggu ditandai "LIBUR" dengan latar merah.

Aksi Cepat (Hanya Admin): Admin dapat mengklik ikon pensil (Edit) atau sampah (Hapus) langsung di dalam slot yang terisi untuk manajemen cepat.

Tombol Export Excel (Matriks):

Fungsi: Mengekspor tampilan matriks jadwal yang sedang dilihat ke file Excel (.xlsx).

Fitur: Laporan Excel ini mempertahankan styling (misal: sel "LIBUR" tetap berwarna merah) dan struktur merge-cell untuk kolom mesin.

C. Tab: Data Master

Tab ini berfungsi sebagai "database" yang dapat dilihat dan dikelola oleh Admin.

Tabel Master Produksi:

Fungsi: Menampilkan semua data dari tabel production_rates.

Fitur: Dilengkapi search bar untuk memfilter data berdasarkan Kode, Nama, atau Mesin (Utama/Opsional).

Manajemen (via Tab Estimasi): Admin dapat menambah, mengedit, atau menghapus data ini menggunakan "Formulir Data Produksi Baru" yang terletak di Tab Estimasi.

Tabel Master Jadwal:

Fungsi: Menampilkan semua data jadwal yang pernah dibuat dari tabel production_schedule.

Pencarian Lanjutan: Dilengkapi search bar yang dapat memfilter berdasarkan Mesin, Kode, Nama Komponen, atau Nomor Shift (misal: "Shift 1" atau "1").

Manajemen Multi-Hapus (Hanya Admin):

Admin dapat mencentang beberapa slot jadwal.

Tersedia checkbox "Pilih Semua" untuk memilih semua hasil yang sedang difilter.

Tombol "Hapus Item Terpilih" muncul untuk menghapus semua data yang dicentang dalam satu kali aksi.

Tombol Export Excel (Master Jadwal): Mengekspor daftar jadwal yang sedang difilter ke file Excel.

3. Fitur Latar Belakang & Teknis

Otentikasi Admin: Sistem menggunakan password sederhana (admin123) untuk membuka fitur-fitur kritis (CRUD data, ekspor, dan penjadwalan otomatis).

Integrasi Supabase: Seluruh aplikasi terhubung ke database Supabase untuk menyimpan dan mengambil data.

Listener Real-time (Data Master): Aplikasi mendengarkan perubahan real-time pada tabel production_rates. Jika ada data master yang diubah (misal: oleh Admin lain), tabel di Data Master akan otomatis ter-update tanpa perlu refresh.

Desain Responsif: Dibangun dengan Tailwind CSS, aplikasi dapat beradaptasi dengan baik di perangkat mobile maupun desktop.
