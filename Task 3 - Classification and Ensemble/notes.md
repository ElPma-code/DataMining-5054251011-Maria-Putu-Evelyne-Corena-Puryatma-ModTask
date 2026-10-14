## Dataset

- `creditcard.csv`: 284.807 baris, 31 kolom
- Missing value: 0
- Baris duplikat: 1.081 (dicek, tidak dihapus)
- Kelas 0 (normal): 284.315
- Kelas 1 (fraud): 492 = 0,173%

## Split dan resampling

- Split 80:20 dengan `stratify=y`, `random_state=42`
- Data latih: 227.845 baris (227.451 normal, 394 fraud)
- Data uji: 56.962 baris (56.864 normal, 98 fraud)
- Undersampling hanya di data latih: 394 normal + 394 fraud = 788 baris
- Data uji tidak diubah, tetap distribusi asli
- Undersampling membuang 227.057 baris normal (99,8% dari data normal)
- SMOTE hanya di data latih: 227.451 normal + 227.451 fraud = 454.902 baris
- SMOTE menambah 227.057 fraud sintetis, data normal tidak ada yang dibuang

## Model

- XGBoost (`XGBClassifier`), termasuk gradient boosting
- `GridSearchCV`, 5-fold stratified, scoring F1
- Grid: `n_estimators` [100, 200], `learning_rate` [0.05, 0.1], `max_depth` [3, 5]
- Parameter terbaik: `learning_rate=0.05`, `max_depth=5`, `n_estimators=200`
- Skor cross validation: 0,950
- Model tanpa resampling dan model SMOTE parameternya sama

## Hasil di data uji

| Model            | Accuracy | Precision | Recall | F1    | ROC AUC |
| ---------------- | -------- | --------- | ------ | ----- | ------- |
| Tanpa resampling | 1,000    | 0,929     | 0,806  | 0,863 | 0,976   |
| Undersampling    | 0,955    | 0,034     | 0,918  | 0,066 | 0,975   |
| SMOTE            | 0,997    | 0,381     | 0,898  | 0,535 | 0,978   |

| Model            | TN     | FP (salah tuduh) | FN (fraud lolos) | TP (fraud tertangkap) |
| ---------------- | ------ | ---------------- | ---------------- | --------------------- |
| Tanpa resampling | 56.858 | 6                | 19               | 79                    |
| Undersampling    | 54.333 | 2.531            | 8                | 90                    |
| SMOTE            | 56.721 | 143              | 10               | 88                    |

## Insight: accuracy menyesatkan

- Model yang selalu menebak "normal" sudah dapat accuracy 0,998 tanpa menangkap satu fraud pun
- Di balik 1,000 itu masih ada 19 dari 98 fraud yang lolos
- Selisih accuracy model tak berguna vs model bagus hanya sekitar 0,001
- Yang dipakai untuk menilai: precision, recall, F1, AUC-ROC pada kelas fraud

## Insight: resampling = trade-off, bukan otomatis lebih baik

- Tujuan resampling: menaikkan recall, bukan accuracy
- Recall naik 0,806 -> 0,918 (fraud lolos turun 19 -> 8)
- Precision jatuh 0,929 -> 0,034 (salah tuduh naik 6 -> 2.531)
- +11 fraud tertangkap dibayar +2.525 salah tuduh, sekitar 230 salah tuduh per 1 fraud tambahan
- F1 memilih model tanpa resampling (0,863 vs 0,066)
- Undersampling layak hanya kalau 1 fraud lolos jauh lebih mahal daripada memeriksa ~230 transaksi normal
- Kesimpulan --> resampling tidak selalu menang sah,

## Insight: AUC hampir sama, bedanya di threshold

- AUC 0,976 vs 0,975: kemampuan memisahkan fraud dan normal setara
- Bedanya di prediksi akhir pada threshold 0,5
- Model undersampling dilatih seolah fraud 50%, padahal aslinya 0,17%, jadi terlalu mudah menandai fraud
- Skor CV 0,950 dihitung di data seimbang, jadi tidak mencerminkan F1 di data uji (0,066)

## Insight: SMOTE ada di tengah (tanpa vs under vs over)

- Recall SMOTE 0,898, hampir setara undersampling 0,918 (fraud lolos 10 vs 8)
- Salah tuduh SMOTE 143, jauh di bawah undersampling (2.531), masih di atas tanpa resampling (6)
- SMOTE vs tanpa resampling: +9 fraud tertangkap dibayar +137 salah tuduh, sekitar 15 salah tuduh per 1 fraud tambahan
- SMOTE vs undersampling: hanya 2 fraud lebih sedikit, tapi 2.388 salah tuduh lebih sedikit
- Urutan F1: tanpa resampling 0,863 > SMOTE 0,535 > undersampling 0,066
- Urutan recall: undersampling 0,918 > SMOTE 0,898 > tanpa resampling 0,806
- AUC ketiganya hampir sama (0,976 / 0,975 / 0,978)
- SMOTE tidak membuang data normal, jadi precision-nya jauh di atas undersampling
- Prioritas precision / F1 -> tanpa resampling
- Prioritas recall dengan salah tuduh masih wajar -> SMOTE
- Undersampling 1:1 kalah dari SMOTE hampir di semua metrik, recall-nya cuma unggul 0,02
- Dicoba juga SMOTE + `StandardScaler`: tidak lebih baik (precision 0,238, recall 0,878, F1 0,374), jadi dipakai SMOTE tanpa scaling

## Catatan kecil

- Teks merah `ResourceTracker ... ChildProcessError` = noise dari `n_jobs=-1` di Python 3.13, tidak memengaruhi hasil
- `StandardScaler` di-import tapi tidak dipakai, model berbasis tree tidak butuh scaling
- Variabel masih bernama `gb`, `grid_gb`, `gb_tanpa` walau modelnya sekarang XGBoost
- Sebelum dikumpulkan: Restart & Run All (seluruh notebook jalan sekitar 10 detik)
- kalau prioritasnya precision atau F1, pakai tanpa resampling; kalau prioritasnya menangkap fraud sebanyak mungkin, SMOTE better than undersampling.

## Laporan Guide

- Laporan minimal 2 halaman dengan visualisasi (langkah 5 README)
- Isi laporan: distribusi kelas awal, pendekatan penanganan imbalance, metrik + analisis perbandingan
