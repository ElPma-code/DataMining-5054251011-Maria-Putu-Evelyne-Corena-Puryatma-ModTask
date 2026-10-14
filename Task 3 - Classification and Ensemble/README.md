Deskripsi Singkat
Pada praktikum ini, mahasiswa membangun model klasifikasi menggunakan ensemble method (Random Forest atau Boosting) pada dataset dengan distribusi kelas tidak seimbang, serta menerapkan teknik penanganan class imbalance seperti oversampling (SMOTE), undersampling, atau cost-sensitive learning.

Tujuan Praktikum
Memahami penerapan ensemble method dalam klasifikasi data.
Mengatasi masalah class imbalance pada dataset.
Mengevaluasi performa model menggunakan metrik yang sesuai seperti precision, recall, F1-score, dan AUC-ROC.

Ketentuan Dataset
Dataset: Credit Card Fraud Detection (Kaggle), berisi data transaksi kartu kredit dengan label Class: 0 = transaksi normal, 1 = transaksi penipuan (fraud).
Link: https://www.kaggle.com/mlg-ulb/creditcardfraud
Gunakan file creditcard.csv (284.807 baris, 31 kolom).

Langkah-Langkah Praktikum

1. Unduh dan Import Dataset
   Unduh creditcard.csv dari link di atas, lalu impor menggunakan pandas.
   Tampilkan .head(), .shape, dan .info() untuk memahami struktur data.
2. Praproses Data
   Identifikasi distribusi kelas pada atribut Class (jumlah dan persentase), lalu visualisasikan.
   Bagi dataset menjadi data latih dan data uji dengan perbandingan 80:20 (gunakan stratify=y).
   Terapkan metode oversampling (seperti SMOTE) atau undersampling untuk menangani class imbalance. Resampling hanya dilakukan pada data latih, data uji tetap menggunakan distribusi asli.
3. Membangun Model Klasifikasi
   Gunakan ensemble method seperti Random Forest atau Gradient Boosting.
   Bandingkan model tanpa dan dengan penanganan class imbalance.
4. Evaluasi Model
   Hitung precision, recall, F1-score, dan AUC-ROC untuk menilai performa model pada kelas minoritas (fraud).
   Gunakan confusion matrix untuk memahami distribusi prediksi.
   Jelaskan mengapa accuracy saja tidak cukup untuk dataset ini.
5. Penyusunan Laporan
   Tulis laporan minimal 2 halaman, dilengkapi dengan visualisasi, berisi:
   Hasil distribusi kelas awal.
   Pendekatan yang digunakan untuk menangani class imbalance.
   Performansi model dengan metrik evaluasi, beserta analisis perbandingannya.
