Tugas Praktikum 6: Clustering (Advance)

Deskripsi Singkat
Pada praktikum ini, mahasiswa menerapkan empat algoritma clustering lanjutan, yaitu Agglomerative Clustering, DBSCAN, Gaussian Mixture Models (GMM), dan Spectral Clustering, pada data pengukuran fisik penguin. Hasil keempat algoritma dibandingkan, dievaluasi dengan Silhouette Score, Rand Index, dan Normalized Mutual Information (NMI), lalu diuji kestabilannya terhadap perubahan kecil pada dataset.

Tujuan Praktikum
Memahami konsep clustering lanjutan: hierarchical, density-based, model-based, dan spectral clustering.
Menerapkan keempat algoritma tersebut pada dataset nyata dan membandingkan hasil pengelompokannya.
Mengevaluasi hasil clustering dengan evaluasi internal (Silhouette Score), evaluasi eksternal (Rand Index dan NMI), serta uji kestabilan.

Ketentuan Dataset
Dataset: Palmer Penguins (Horst, Hill, dan Gorman, 2020), berisi 344 baris hasil pengukuran penguin di Kepulauan Palmer, Antartika, meliputi spesies, pulau, panjang dan kedalaman paruh, panjang sirip, massa tubuh, jenis kelamin, serta tahun pengamatan.
Link: https://raw.githubusercontent.com/allisonhorst/palmerpenguins/main/inst/extdata/penguins.csv
Gunakan empat kolom numerik sebagai fitur clustering: bill_length_mm, bill_depth_mm, flipper_length_mm, dan body_mass_g.
Kolom species (Adelie, Chinstrap, Gentoo) dipakai hanya sebagai label pembanding saat evaluasi eksternal, dan tidak boleh ikut dipakai saat clustering.

Langkah-Langkah Praktikum

1. Unduh dan Import Dataset
   Baca penguins.csv langsung dari link di atas menggunakan pandas (pd.read_csv).
   Tampilkan .head(), .shape, dan .info() untuk memahami struktur dan atribut dataset.
2. Eksplorasi dan Pembersihan Data
   Tampilkan jumlah nilai kosong pada tiap kolom dengan .isna().sum().
   Hapus baris yang nilainya kosong pada salah satu dari empat kolom numerik atau pada kolom species.
   Tampilkan statistik deskriptif dengan .describe(), lalu perhatikan perbedaan skala antar kolom.
   Tampilkan jumlah baris sebelum dan sesudah pembersihan, serta jumlah data per spesies.
   Buat scatter plot awal, misalnya flipper_length_mm terhadap bill_length_mm, untuk melihat sebaran data sebelum clustering.
3. Standardisasi Data
   Pisahkan empat kolom numerik sebagai matriks fitur X, dan kolom species sebagai label pembanding y.
   Standardisasi X dengan z-score (StandardScaler) karena satuan antar kolom berbeda jauh, yaitu milimeter dan gram. Seluruh algoritma dijalankan pada data hasil standardisasi.
4. Penerapan Algoritma
   Terapkan Agglomerative Clustering dengan jumlah kluster 3. Tampilkan dendrogram-nya dan sebutkan jenis linkage yang dipakai.
   Terapkan DBSCAN mulai dari eps 0.5 dan MinPts 5. Coba juga beberapa nilai eps lain, lalu catat jumlah kluster dan jumlah titik noise yang dihasilkan tiap nilai.
   Terapkan Gaussian Mixture Models (GMM) dengan 3 komponen.
   Terapkan Spectral Clustering dengan 3 kluster.
   Buat scatter plot hasil tiap algoritma, satu warna untuk tiap kluster. Khusus DBSCAN, beri warna terpisah untuk titik noise (label -1).
5. Evaluasi Hasil Clustering
   Hitung Silhouette Score untuk tiap algoritma. Untuk DBSCAN, hitung tanpa mengikutsertakan titik noise dan sebutkan berapa titik yang dibuang.
   Hitung Rand Index dan Normalized Mutual Information (NMI) terhadap kolom species.
   Lakukan uji kestabilan: jalankan ulang tiap algoritma pada 90% data yang diambil acak, sebanyak tiga kali, lalu bandingkan hasilnya dengan hasil pada data penuh.
   Rangkum seluruh nilai evaluasi dalam satu tabel perbandingan.
6. Penyusunan Laporan
   Tulis laporan singkat, dilengkapi dengan tabel/visualisasi, berisi:
   Hasil eksplorasi dan pembersihan data.
   Visualisasi dan nilai evaluasi dari keempat algoritma.
   Kesimpulan: algoritma mana yang paling cocok untuk dataset ini beserta alasan pemilihannya.

Hasil yang Diharapkan
Data penguin yang sudah dibersihkan dan distandardisasi.
Scatter plot hasil clustering dari keempat algoritma.
Tabel perbandingan Silhouette Score, Rand Index, NMI, dan hasil uji kestabilan, beserta analisisnya.

Ketentuan Repository GitHub
Gunakan repository GitHub pribadi yang sama (dan tetap public) seperti pada praktikum sebelumnya.
Untuk tugas ini, buat folder bernama tugas-clustering-advance di dalam repository, berisi file .ipynb dan .pdf sesuai ketentuan penamaan di bawah.
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
│ └── ...
├── tugas-sequential-pattern/
│ └── ...
├── tugas-clustering-advance/
│ ├── NRP_Nama_Tugas_Clustering_Advance.ipynb
│ └── NRP_Nama_Tugas_Clustering_Advance.pdf
└── (folder tugas praktikum lain menyusul setiap minggunya)

Format Pengumpulan
File: .ipynb + .pdf
Penamaan file: NRP_Nama_Tugas_Clustering_Advance
Pengumpulan: kirim link folder tugas-clustering-advance pada repository GitHub melalui Google Form berikut: https://forms.gle/Z91PQCFDfJR81uZx5
Deadline: Minggu, 16 November 2026, pukul 23:59 WIB
