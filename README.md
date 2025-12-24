Sistem Estimasi Produksi & Perencanaan Mesin
Aplikasi Web untuk Estimasi Produksi, Penjadwalan Mesin, dan Optimasi Shift Kerja Sistem ini merupakan aplikasi berbasis web (Single Page Application) yang dirancang khusus untuk membantu proses perencanaan produksi manufaktur secara terintegrasi. Fokus utama sistem adalah menghitung estimasi kapasitas produksi, mengatur jadwal penggunaan mesin, serta memastikan distribusi beban kerja yang optimal berdasarkan shift kerja harian.

Deskripsi Sistem
Aplikasi ini menyediakan dua mode akses utama, yaitu Pengunjung dan Administrator, guna memastikan keamanan data serta pembagian wewenang yang jelas. Pengunjung dapat memantau data master dan jadwal produksi secara transparan, sementara Administrator memiliki akses penuh untuk mengelola data, melakukan perencanaan, serta memperbarui jadwal produksi sesuai kebutuhan operasional.
Melalui fitur estimasi kapasitas produksi, sistem mampu menghitung target output secara otomatis untuk tiga shift kerja, termasuk dukungan perhitungan batch untuk banyak produk sekaligus. Hal ini memudahkan tim produksi dalam melakukan simulasi dan evaluasi kapasitas sebelum jadwal diterapkan.
Pada sisi perencanaan mesin, sistem menyajikan tampilan tabel visual berbentuk grid yang intuitif, menampilkan penugasan produk ke mesin berdasarkan tanggal dan shift. Administrator dapat dengan mudah menambah, mengedit, maupun menduplikasi jadwal menggunakan modal interaktif, sehingga proses penjadwalan menjadi lebih cepat dan minim kesalahan. Sistem juga dilengkapi logika otomatis untuk mendeteksi hari libur akhir pekan dan memberikan peringatan apabila terdapat jadwal yang tidak sesuai.

Fitur Unggulan
Manajemen Peran & Keamanan Akses
Pemisahan hak akses antara pengunjung dan administrator dengan sistem login terproteksi.
Estimasi Kapasitas Produksi Otomatis
Perhitungan target produksi berbasis shift dan multi-produk dalam satu proses.
Perencanaan Mesin yang Visual & Interaktif
Tabel jadwal dengan fitur sticky column, sinkronisasi scroll, serta copy–paste jadwal antar mesin dan shift.
Data Master Terpusat
Penyimpanan informasi produk lengkap dengan pencarian real-time tanpa reload halaman.
Pelaporan & Analitik
Ekspor data ke Excel (.xlsx) dengan format rapi, visualisasi grafik menggunakan Chart.js, serta notifikasi sistem untuk setiap aksi pengguna.

Ringkasan Arsitektur Sistem
Aplikasi ini dibangun dengan pendekatan ringkas, cepat, dan modern, mengandalkan:
Frontend:
Vanilla JavaScript (ES6+), HTML5 Semantic, dan Tailwind CSS untuk UI responsif dan performa tinggi.
Backend & Database:
Supabase sebagai Backend-as-a-Service (BaaS) dengan database real-time berbasis PostgreSQL.
Integrasi Library:
SheetJS untuk ekspor Excel, Chart.js untuk visualisasi data, serta Inter Font untuk tampilan profesional.
State Management:
Sinkronisasi local state dengan database Supabase (optimistic UI) sehingga perubahan data langsung terlihat oleh pengguna.

Kesimpulan
Sistem ini dirancang sebagai alat manajemen internal yang efektif untuk mendukung perencanaan produksi, meningkatkan akurasi estimasi kapasitas, serta mempermudah pengambilan keputusan operasional melalui tampilan yang intuitif, responsif, dan profesional.
