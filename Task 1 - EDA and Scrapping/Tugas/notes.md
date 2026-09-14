## Konfigurasi dan pengambilan HTML

Hanya menerima HTTPS dan host yang terdaftar, memeriksa `robots.txt`, membatasi waktu tunggu serta ukuran respons, dan menolak respons non-HTML.

Dua penyesuaian:

1. `ALLOWED_LIVE_HOSTS` diarahkan ke `en.wikipedia.org`;
2. `MAX_RESPONSE_BYTES` dinaikkan menjadi 5 MB karena halaman daftar eksoplanet berukuran sekitar 1,6-2,3 MB, jauh di atas batas 1 MB pada contoh sebelumnya.

---

# Catatan EDA

## Ruang lingkup

Notebook **hanya EDA**: masalah diidentifikasi dan dicatat, penanganannya untuk tahap preprocessing.

1. Tidak ada kolom yang di-drop, tidak ada kolom yang di-rename, tidak ada baris yang dihapus;
2. `df` tidak pernah diubah; hasil perhitungan tambahan disimpan di variabel terpisah (`kelompok_metode`, `cek_kepler`, `awalan_katalog`, `ringkasan_outlier`);
3. sel lama yang error (`pd.read_csv"eksoplanet.csv"`) diganti seluruhnya.

## Struktur dan penyesuaian terhadap notebook referensi

Urutan bagian 1-9 mengikuti `intro-to-exploratory-data-analysis-eda-in-python.ipynb`. Beberapa langkah disesuaikan agar tetap EDA:

1. **Import library**: sama, ditambah pengaturan palet dan gaya grafik;
2. **Memuat data**: `head()` dan `tail()`;
3. **Tipe data**: `dtypes`, ditambah `nunique()` untuk melihat kolom yang sebenarnya kategori;
4. **Kolom kurang relevan**: referensi melakukan drop; di sini hanya **ditandai** lewat tabel ringkasan (tipe, nilai unik, terisi, % kosong);
5. **Nama kolom**: referensi melakukan rename; di sini hanya **dicek**, karena nama sudah `snake_case` dan memuat satuan;
6. **Duplikat**: referensi menghapus duplikat; di sini hanya dihitung (hasilnya 0);
7. **Missing values**: referensi melakukan `dropna()`; di sini diganti dengan analisis pola kosong (per kolom, per metode, per tahun, per baris);
8. **Outlier**: referensi menghapus outlier IQR; di sini hanya dideteksi (boxplot, tabel IQR, baris ekstrem);
9. **Plot**: histogram, heatmap, scatterplot seperti referensi, diperluas menjadi grafik untuk setiap fitur.

Bagian tambahan di akhir: **Ringkasan masalah untuk tahap preprocessing**.

## Keputusan visualisasi

1. **Skala log** dipakai untuk `massa_mj`, `radius_rj`, `periode_hari`, `sumbu_semimayor_au`, dan `jarak_tahun_cahaya` karena nilainya menyebar di beberapa orde besaran; skala asli tetap ditampilkan pada boxplot pertama sebagai pembanding;
2. `suhu_planet_k`, `massa_bintang_msun`, dan `suhu_bintang_k` memakai skala linear karena rentangnya sempit;
3. pada scatterplot, **microlensing, timing, dan imaging digabung menjadi "lainnya"** karena jumlahnya kecil (27 planet) dan agar cukup 3 warna yang tetap bisa dibedakan penderita buta warna;
4. palet: biru `#2a78d6` (satu seri / transit), oranye `#eb6834` (radial vel.), aqua `#1baf7a` (lainnya);
5. heatmap korelasi memakai skala **diverging biru-merah** dengan titik tengah abu-abu; heatmap nilai kosong dan jumlah pasangan memakai skala **sekuensial biru**;
6. heatmap korelasi hanya menampilkan segitiga bawah agar nilai tidak berulang.

## Fungsi bantu di notebook

1. `plot_distribusi(kolom, skala_log, bins)`: histogram satu fitur dengan garis median, judul berisi `n` dan jumlah kosong, lalu mengembalikan tabel `describe()` + `skewness`;
2. `plot_sebar(x, y, log_x, log_y)`: scatterplot dua fitur, hanya memakai baris yang keduanya terisi, diwarnai per kelompok metode.

## Catatan metode analisis

1. **Awalan katalog**: diambil dari `nama` dengan regex (Kepler, K2, WASP, HAT-P, HATS, KELT, OGLE, HD, HIP, Gliese, 2MASS, COROT, Qatar, XO, EPIC, TRAPPIST, KOI); sisanya masuk "Lainnya";
2. **IQR** dihitung dua kali: skala asli dan skala log (`log10`), untuk membedakan outlier sebenarnya dari efek distribusi yang miring;
3. `batas_bawah` IQR negatif pada kolom yang pasti positif, jadi hanya outlier atas yang bermakna di kolom tersebut;
4. **Pearson dan Spearman** dibandingkan: selisih besar menandakan hubungan tidak linear atau terdistorsi outlier;
5. setiap korelasi dihitung dari **pasangan baris yang berbeda** (pairwise), sehingga jumlah pasangan ditampilkan dalam heatmap terpisah;
6. **cek hukum Kepler III**: `rasio = a³ / (P² × M)` dengan `a` dalam AU, `P` dalam tahun (`periode_hari / 365,25`), `M` dalam massa Matahari; nilai ideal ≈ 1, rasio di luar 0,5-2 dianggap tidak konsisten;
7. batas **13 MJ** dipakai sebagai batas umum planet vs katai coklat (batas pembakaran deuterium);
8. konversi kasar radius: 1 RJ ≈ 11,2 radius Bumi, sehingga 0,09-0,36 RJ ≈ 1-4 radius Bumi.

## Temuan utama

### Kualitas data

1. Tidak ada baris duplikat dan tidak ada nama planet ganda;
2. semua kolom numerik sudah bertipe `float64`;
3. `tahun_penemuan` hanya berisi 2014 dan 2016, lebih tepat dianggap kategori.

### Missing values

1. Kosong per kolom: `suhu_planet_k` 95,6%, `massa_mj` 87,4%, `sumbu_semimayor_au` 57,0%, `massa_bintang_msun` 11,2%, `radius_rj` 5,4%, `jarak_tahun_cahaya` 3,2%, `suhu_bintang_k` 1,1%, `periode_hari` 0,8%;
2. pola kosong **struktural** mengikuti metode: transit tanpa massa (92%), radial velocity tanpa radius (99%), microlensing tanpa periode/radius/suhu bintang, imaging tanpa periode (100%);
3. pola kosong juga mengikuti **tabel sumber per tahun**: `sumbu_semimayor_au` 7% (2014) vs 86% (2016), `massa_bintang_msun` 29% (2014) vs 1% (2016), `jarak_tahun_cahaya` hanya kosong di 2016 (5%);
4. hanya **78 baris (3,3%)** lengkap; 1.620 baris kosong di 3 kolom.

### Distribusi

1. `metode_deteksi`: transit 2.235 (94,4%), radial vel. 105 (4,4%), microlensing 13, timing 9, imaging 5;
2. `tahun_penemuan`: 2014 = 869, 2016 = 1.498; kenaikan hampir seluruhnya dari transit (801 → 1.434);
3. awalan nama: Kepler 2.066 (87%), K2 94, HD 54, WASP 43;
4. `massa_mj`: median 0,73 MJ, rentang 0,0002-30, **dua kelompok** (~0,01-0,05 MJ dan ~1 MJ), 6 objek > 13 MJ;
5. `radius_rj`: median 0,189 RJ, 82% berukuran 1-4 radius Bumi, puncak kedua kecil di ~1 RJ (138 planet > 0,8 RJ);
6. `periode_hari`: median 11 hari, 47% < 10 hari, skewness 13,96;
7. `sumbu_semimayor_au`: median 0,098 AU, skewness 28,9 (tertinggi) karena nilai 6.900 AU;
8. `suhu_planet_k`: hanya 104 data, median 1.292 K, tersebar merata;
9. `jarak_tahun_cahaya`: median 2.320 tahun cahaya, maksimum 27.000 (microlensing);
10. `massa_bintang_msun`: median 0,95 Msun, 72% bermassa 0,8-1,2 Msun;
11. `suhu_bintang_k`: median 5.636 K, 60% bersuhu 5.000-6.000 K, miring ke kiri.

### Outlier

1. **626 baris** punya minimal satu outlier IQR (skala asli);
2. outlier turun drastis pada skala log (`periode_hari` 289 → 67, `massa_mj` 38 → 2);
3. nilai paling ekstrem valid secara fisik dan berasal dari metode minoritas: `2MASS J2126-8140` (6.900 AU), `OGLE-2015-BLG-0051Lb` (27.000 tahun cahaya), `HR 2562 b` (30 MJ), `HD 100546 b` (3,4 RJ, bintang 10.500 K), `HD 30177 c` (11.613 hari).

### Hubungan antar fitur

1. `periode_hari` - `sumbu_semimayor_au`: 0,95 (Pearson), 0,99 (Spearman), sesuai hukum Kepler;
2. `massa_bintang_msun` - `suhu_bintang_k`: 0,78 / 0,86;
3. `radius_rj` - `suhu_planet_k`: 0,80 / 0,87, tetapi hanya dari ~97 pasangan;
4. `massa_mj` - `radius_rj`: 0,23 / 0,72; radius mendatar di ~1 RJ untuk massa > ~0,3 MJ;
5. `periode_hari` - `suhu_planet_k`: -0,32 / -0,74;
6. cek Kepler: 745 planet, median rasio 1,006; tidak konsisten hanya `Kepler-186c` (0,43) dan `XO-6b` (3,47);
7. bintang radial velocity bermassa > 1,3 Msun keluar dari tren massa-suhu (suhu 4.000-5.600 K, kemungkinan bintang raksasa);
8. jarak median per metode: imaging 160, radial vel. 208, timing 1.790, transit 2.390, microlensing 13.000 tahun cahaya.

## Daftar masalah untuk preprocessing

1. Missing values berat dan struktural (bergantung metode dan tahun);
2. distribusi sangat miring pada fitur planet dan jarak;
3. outlier valid secara fisik dari populasi berbeda; 6 objek > 13 MJ kemungkinan bukan planet;
4. kelas tidak seimbang (transit 94,4%, Kepler 87%);
5. fitur redundan (`periode_hari` dan `sumbu_semimayor_au`);
6. dua baris tidak konsisten dengan hukum Kepler III (`Kepler-186c`, `XO-6b`);
7. `nama` hanya identitas; `tahun_penemuan` hanya 2 nilai;
8. satuan massa berbeda antara planet (MJ) dan bintang (Msun).
