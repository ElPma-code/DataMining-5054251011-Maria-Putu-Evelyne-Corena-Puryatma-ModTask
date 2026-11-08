Tugas Praktikum 5: Sequential Pattern Analysis

Deskripsi Singkat
Pada praktikum ini, mahasiswa menemukan pola pembelian yang berurutan dari waktu ke waktu dalam dataset transaksi menggunakan Sequential Pattern Mining. Pola berurutan diekstraksi dengan algoritma PrefixSpan atau GSP, lalu dievaluasi berdasarkan metrik support dan confidence.

Tujuan Praktikum
Memahami konsep Sequential Pattern Analysis dan aplikasinya dalam data mining.
Menerapkan algoritma Sequential Pattern Mining seperti PrefixSpan atau GSP pada dataset transaksi.
Mengevaluasi pola berurutan yang ditemukan berdasarkan metrik support dan confidence.

Ketentuan Dataset
Dataset: Online Retail (UCI Machine Learning Repository), berisi transaksi ritel online sebuah toko di Inggris periode Desember 2010 sampai Desember 2011, meliputi nomor invoice, kode dan deskripsi produk, jumlah, harga, tanggal transaksi, ID pelanggan, serta negara.
Link: https://archive.ics.uci.edu/dataset/352/online+retail
Gunakan file Online Retail.xlsx (541.909 baris, 8 kolom).
Kolom CustomerID dan InvoiceDate dipakai untuk menyusun urutan (sequence) pembelian tiap pelanggan.

Langkah-Langkah Praktikum
1. Unduh dan Import Dataset
Unduh Online Retail.xlsx dari link di atas, lalu impor menggunakan pandas (pd.read_excel).
Tampilkan .head(), .shape, dan .info() untuk memahami struktur dan atribut dataset.
2. Eksplorasi dan Pembersihan Data
Identifikasi kolom yang relevan untuk analisis pola berurutan (misalnya CustomerID, InvoiceDate, dan Description).
Hapus baris dengan Description kosong dan transaksi yang dibatalkan (InvoiceNo diawali huruf "C").
Hapus baris dengan Quantity bernilai negatif atau nol.
Hapus baris dengan CustomerID kosong, karena sequence disusun per pelanggan.
Tampilkan jumlah baris, jumlah invoice, dan jumlah pelanggan sebelum dan sesudah pembersihan.
3. Persiapan Data untuk Sequential Pattern Mining
Urutkan data berdasarkan CustomerID dan InvoiceDate, lalu kelompokkan item pada satu invoice menjadi satu itemset.
Susun setiap pelanggan menjadi satu sequence berisi daftar itemset yang urut secara waktu, lalu simpan dalam bentuk list of list agar dapat diproses dengan pustaka prefixspan atau SPMF.
4. Penerapan Algoritma
Terapkan algoritma Sequential Pattern Mining (PrefixSpan atau GSP) pada data sequence yang telah disusun.
Gunakan minimum support 0.01 (relatif terhadap jumlah pelanggan) sebagai titik awal. Jika pola yang dihasilkan terlalu sedikit atau terlalu banyak, sesuaikan nilainya dan jelaskan alasannya.
5. Evaluasi Pola Berurutan
Tampilkan pola berurutan yang ditemukan beserta nilai support dan confidence-nya.
Pilih tiga pola terbaik berdasarkan nilai support tertinggi, lalu interpretasikan artinya dalam konteks bisnis ritel.
6. Penyusunan Laporan
Tulis laporan singkat, dilengkapi dengan tabel/visualisasi, berisi:
Hasil eksplorasi dan pembersihan data.
Pola berurutan yang dihasilkan beserta analisis evaluasinya.
Kesimpulan tentang pola pembelian berurutan yang ditemukan dalam dataset.

Hasil yang Diharapkan
Dataset transaksi yang telah diolah menjadi sequence pembelian per pelanggan.
Daftar pola berurutan yang ditemukan beserta nilai support dan confidence-nya.
Laporan singkat yang mencakup hasil eksplorasi, penerapan algoritma, dan analisis pola berurutan.

Ketentuan Repository GitHub
Gunakan repository GitHub pribadi yang sama (dan tetap public) seperti pada praktikum sebelumnya.
Untuk tugas ini, buat folder bernama tugas-sequential-pattern di dalam repository, berisi file .ipynb dan .pdf sesuai ketentuan penamaan di bawah.
Dataset tidak perlu diunggah ke repository.

Contoh struktur repo
nama-repo/
├── tugas-scrapping-eda/
│   └── ...
├── tugas-praproses-data/
│   └── ...
├── tugas-ensemble/
│   └── ...
├── tugas-association-rule/
│   └── ...
├── tugas-sequential-pattern/
│   ├── NRP_Nama_Tugas_Sequential_Pattern.ipynb
│   └── NRP_Nama_Tugas_Sequential_Pattern.pdf
└── (folder tugas praktikum lain menyusul setiap minggunya)

Format Pengumpulan
File: .ipynb + .pdf
Penamaan file: NRP_Nama_Tugas_Sequential_Pattern
Pengumpulan: kirim link folder tugas-sequential-pattern pada repository GitHub melalui Google Form berikut: https://forms.gle/Z91PQCFDfJR81uZx5
Deadline: Minggu, 9 November 2026, pukul 23:59 WIB

