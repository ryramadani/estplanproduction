Website ini adalah Sistem Estimasi Produksi dan Perencanaan Mesin berbasis web yang dirancang untuk membantu perencanaan PPIC. Secara garis besar, sistem ini mengubah proses manual penghitungan target dan penjadwalan mesin menjadi digital dan otomatis.

Berikut adalah penjelasan lengkap mengenai fitur dan alur kerjanya:

1. Fungsi Utama
Estimasi Waktu Produksi: Menghitung secara otomatis berapa jam, shift, dan hari yang dibutuhkan untuk menyelesaikan sejumlah pesanan berdasarkan target rate mesin yang sudah tersimpan di database.

Visualisasi Jadwal (Matriks): Menampilkan papan jadwal digital (Mesin vs Tanggal/Shift) untuk memantau mesin mana yang sibuk atau kosong.

2. Tiga Modul Utama (Tab Navigasi)
A. Estimasi Produksi (Kalkulator)
Input: User memasukkan Kode Barang, Jumlah Order (Dus), dan preferensi Shift Mulai.

Output: Sistem menghitung total beban kerja. Jika pesanan terdiri dari banyak komponen berbeda, sistem akan mencari "jalur kritis" (mesin tersibuk) untuk menentukan durasi total proyek.

Simulasi Otomatis: Memiliki fitur "Jadwalkan Otomatis" yang mencari slot kosong di kalender masa depan dan mengisinya secara cerdas tanpa menabrak jadwal yang sudah ada.

Export: Hasil perhitungan bisa diunduh menjadi PDF.

B. Perencanaan Mesin (Matriks Jadwal)
Tampilan: Tabel matriks yang memetakan Mesin Utama (Baris) melawan Tanggal & Shift 1/2/3 (Kolom).

Interaktif:

Drag & Drop: Admin bisa memindahkan jadwal dari satu hari ke hari lain atau menukar posisi jadwal hanya dengan mouse.

Warna & Indikator: Slot libur (akhir pekan) berwarna merah, slot terisi berwarna tebal.

CRUD Jadwal: Admin bisa menambah, mengedit, atau menghapus slot jadwal secara manual.

Export: Matriks jadwal bisa diekspor ke Excel.

C. Data Master (Database)
Tempat menyimpan "Rumus" produksi: Kode Barang, Nama Komponen, Mesin Utama/Optional, Isi per Dus, dan Target Produksi per Shift.

Data inilah yang menjadi acuan dasar perhitungan di modul Estimasi.

3. Teknologi & Keamanan
Database Realtime: Menggunakan Supabase sehingga data tersimpan di cloud dan sinkron antar pengguna.

Akses Kontrol: Terdapat fitur Login Admin. Pengguna biasa hanya bisa melihat (View Only), sedangkan Admin bisa mengedit data, menyimpan jadwal, dan melakukan drag & drop.

Validasi: Sistem mencegah bentrok jadwal (double booking) pada mesin yang sama di shift yang sama.
