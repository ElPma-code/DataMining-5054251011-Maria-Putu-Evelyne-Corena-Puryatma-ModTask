Tugas Praktikum 4: Association Rule

Deskripsi Singkat
Pada praktikum ini, mahasiswa menemukan pola atau hubungan antar item dalam dataset transaksi menggunakan Association Rule. Aturan asosiasi diekstraksi dengan algoritma Apriori atau FP-Growth, lalu dievaluasi berdasarkan metrik support, confidence, dan lift.

Tujuan Praktikum
Memahami konsep dan aplikasi Association Rule dalam analisis data.
Menggunakan algoritma Apriori atau FP-Growth untuk mengekstraksi aturan asosiasi.
Mengevaluasi aturan asosiasi dengan metrik support, confidence, dan lift.

Ketentuan Dataset
Dataset: Online Retail (UCI Machine Learning Repository), berisi transaksi ritel online sebuah toko di Inggris periode Desember 2010 sampai Desember 2011, meliputi nomor invoice, kode dan deskripsi produk, jumlah, harga, ID pelanggan, serta negara.
Link: https://archive.ics.uci.edu/dataset/352/online+retail
Gunakan file Online Retail.xlsx (541.909 baris, 8 kolom).

Langkah-Langkah Praktikum

1. Unduh dan Import Dataset
   Unduh Online Retail.xlsx dari link di atas, lalu impor menggunakan pandas (pd.read_excel).
   Tampilkan .head(), .shape, dan .info() untuk memahami struktur dan atribut dataset.
2. Eksplorasi dan Pembersihan Data
   Identifikasi kolom yang relevan untuk analisis Association Rule (misalnya InvoiceNo dan Description).
   Hapus baris dengan Description kosong dan transaksi yang dibatalkan (InvoiceNo diawali huruf "C").
   Hapus baris dengan Quantity bernilai negatif atau nol.
   Tampilkan jumlah baris dan jumlah invoice sebelum dan sesudah pembersihan.
3. Persiapan Data untuk Association Rule
   Format data menjadi transaksi berbasis invoice, di mana setiap transaksi berisi daftar produk yang dibeli.
   Ubah data transaksi ke bentuk one-hot (basket) agar dapat diproses menggunakan pustaka mlxtend atau apyori.
4. Penerapan Algoritma
   Terapkan algoritma Apriori atau FP-Growth untuk menemukan frequent itemset dan aturan asosiasi.
   Gunakan minimum support 0.01 dan minimum confidence 0.5 sebagai titik awal. Jika aturan yang dihasilkan terlalu sedikit atau terlalu banyak, sesuaikan nilainya dan jelaskan alasannya.
5. Evaluasi Aturan Asosiasi
   Tampilkan aturan yang dihasilkan beserta nilai support, confidence, dan lift.
   Pilih tiga aturan terbaik berdasarkan nilai lift, lalu interpretasikan artinya dalam konteks bisnis ritel.
6. Penyusunan Laporan
   Tulis laporan singkat, dilengkapi dengan tabel/visualisasi, berisi:
   Hasil eksplorasi dan pembersihan data.
   Aturan asosiasi yang dihasilkan beserta analisis evaluasinya.
   Kesimpulan tentang pola yang ditemukan dalam dataset.

Hasil yang Diharapkan
Dataset transaksi yang telah diolah dan diformat untuk analisis Association Rule.
Daftar aturan asosiasi yang dihasilkan dengan nilai support, confidence, dan lift.
Laporan singkat yang mencakup hasil eksplorasi, penerapan algoritma, dan analisis aturan asosiasi.

Ketentuan Repository GitHub
Gunakan repository GitHub pribadi yang sama (dan tetap public) seperti pada praktikum sebelumnya.
Untuk tugas ini, buat folder bernama tugas-association-rule di dalam repository, berisi file .ipynb dan .pdf sesuai ketentuan penamaan di bawah.
Dataset tidak perlu diunggah ke repository.

Contoh struktur repo
nama-repo/
├── tugas-scrapping-eda/
│ └── ...
├── tugas-praproses-data/
│ └── ...
├── tugas-ensemble/
│ └── ...
├── tugas-association-rule/
│ ├── NRP_Nama_Tugas_Association_Rule.ipynb
│ └── NRP_Nama_Tugas_Association_Rule.pdf
└── (folder tugas praktikum lain menyusul setiap minggunya)

Format Pengumpulan
File: .ipynb + .pdf
Penamaan file: NRP_Nama_Tugas_Association_Rule
Pengumpulan: kirim link folder tugas-association-rule pada repository GitHub melalui Google Form berikut: https://forms.gle/Z91PQCFDfJR81uZx5
Deadline: Minggu, 1 November 2026, pukul 23:59 WIB
