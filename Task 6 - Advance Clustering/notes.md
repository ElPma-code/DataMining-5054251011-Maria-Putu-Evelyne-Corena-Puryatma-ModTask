### Notes

# Notebook

## Data & pembersihan

1. dataset dibaca langsung dari link (pd.read_csv(url)) sesuai tugas, isinya sama persis sama penguins.csv di folder. 344 baris, 8 kolom
2. yg kepake cuma 4 fitur numerik: bill_length_mm, bill_depth_mm, flipper_length_mm, body_mass_g. species cuma buat evaluasi (RI, NMI), ga ikut clustering. island, sex, year ga dipake
3. nilai kosong: 4 fitur masing2 2 baris, dan itu 2 baris yg sama (1 adelie, 1 gentoo, semua ukurannya kosong). sex kosong 11, species ga ada yg kosong
4. dropna cuma di 4 fitur + species -> 344 jadi 342 baris. sex kosong dibiarin krn sex ga dipake, kalo ikut di-drop malah buang 9 baris lagi yg ukurannya lengkap
5. per spesies: Adelie 151, Gentoo 123, Chinstrap 68 -> ga seimbang, chinstrap paling sedikit
6. describe: body_mass_g rata2 4.201 gram (std 802), kolom lain cuma puluhan-ratusan mm (bill_depth std cuma 1,97). kalo ga distandardisasi, jarak antar titik hampir cuma ditentuin body_mass
7. scatter flipper vs bill_length: gentoo misah jelas (flipper panjang, rata2 217 mm, badan paling berat). adelie & chinstrap flipper-nya mirip (190 vs 196 mm), bedanya di paruh (chinstrap 48,8 mm vs adelie 38,8 mm), dan ada bagian yg tumpang tindih

## Standardisasi

8. X = 4 fitur, y = species. StandardScaler (z-score) -> tiap kolom mean 0, std 1. semua algoritma jalan di X_scaled
9. scatter hasil clustering tetep pake satuan asli (mm) biar gampang dibaca, clustering-nya tetep di data standardisasi
10. warna di scatter hasil = nomor kluster, bukan spesies. jadi kluster 0 di GMM ga harus sama sama kluster 0 di agglomerative

## Agglomerative

11. linkage ward (default sklearn): tiap langkah gabungin 2 kluster yg nambahin variasi dalam kluster paling kecil. cenderung bikin kluster yg bulat & ukurannya mirip
12. dendrogram cuma nampilin 30 gabungan terakhir (truncate_mode='lastp'), kalo full 342 daun ga kebaca. angka dalam kurung = jumlah titik di cabang itu
13. 3 gabungan terakhir jaraknya 12,4 -> 18,6 -> 40,1. garis potong ditaruh di tengah 12,4 & 18,6 -> kepotong jadi 3 kluster. lompatan jaraknya gede jadi 3 kluster emang masuk akal
14. hasil 162 / 123 / 57. gentoo 123 pas semua, 11 chinstrap masuk ke kluster adelie

## DBSCAN

15. parameter: eps = radius tetangga, MinPts (min_samples) = minimal tetangga biar jadi titik inti. titik yg ga masuk kluster mana2 = noise (label -1)
16. eps 0.5 / MinPts 5 -> 4 kluster, 69 noise (20% data). chinstrap kepecah jadi 2 kluster (15 & 27) dan 23 chinstrap jadi noise
17. coba eps lain: 0.3 -> 317 noise (hampir semua noise), 0.4 -> 10 kluster kecil2, 0.5 -> 4 kluster, 0.6 sampe 1.0 -> stabil 2 kluster, noise turun 33 -> 1
18. dipake eps 0.8: noise tinggal 5 (1,5%), jumlah kluster udah ga berubah dari 0.6. 0.9 & 1.0 hasilnya hampir sama
19. eps 0.5 RI-nya lebih tinggi (0,853 vs 0,821) tapi NMI lebih rendah (0,663 vs 0,730) dan 69 titik kebuang jadi noise -> tetep pilih 0.8
20. DBSCAN ga bisa misahin adelie & chinstrap krn kepadatan mereka nyambung (ga ada celah kosong di antaranya). gentoo kepisah sendiri krn ada celah jelas. kelemahan DBSCAN: jumlah kluster ga bisa diatur, cuma ngikutin kepadatan
21. di RI & NMI, noise dihitung sbg 1 kelompok sendiri (5 titik), ga dibuang. yg dibuang cuma di silhouette

## GMM

22. GMM nganggep data = campuran 3 distribusi normal (gaussian), tiap komponen punya mean & kovarians sendiri -> kluster boleh lonjong/miring & ukurannya beda2. tiap titik dapet peluang masuk tiap komponen, label = peluang paling besar
23. n_init=10 = dicoba 10 titik awal, diambil yg terbaik. sempet nyoba default (n_init=1): di uji kestabilan 1 dari 3 percobaan RI-nya cuma 0,76 krn kejebak titik awal yg jelek. pake n_init=10 jadi stabil terus
24. hasil 123 / 152 / 67. gentoo pas semua, cuma 5 yg salah (2 adelie, 3 chinstrap)

## Spectral

25. spectral: bikin graf kemiripan antar titik (affinity rbf, default), terus dipotong jadi 3 kelompok yg sambungan antar kelompoknya paling lemah. bisa nangkep kluster bentuk aneh (ga harus bulat)
26. hasil 176 / 123 / 43, 25 chinstrap masuk kluster adelie -> paling banyak salah di antara algoritma yg k=3
27. sempet nyoba affinity='nearest_neighbors' -> hasilnya sama persis kayak agglomerative (RI 0,961) tapi muncul warning "graph is not fully connected" (gentoo kepisah total). jadi pake default aja
28. GMM & spectral munculin RuntimeWarning matmul (divide by zero / overflow) -> itu bug numpy di Mac, hasilnya tetep bener (keliatan dari tabel silang). di-ignore di cell import

## Evaluasi

29. silhouette (internal, ga pake species): seberapa deket titik ke klusternya sendiri dibanding ke kluster lain, -1 sampe 1. 5 noise DBSCAN dibuang dulu sebelum dihitung
30. silhouette semua mirip: agglomerative 0,454, GMM 0,455, spectral 0,462. DBSCAN paling tinggi 0,536 krn cuma 2 kluster yg jaraknya jauh, bukan berarti lebih bagus
31. rand index (eksternal): persentase pasangan titik yg perlakuannya sama di kluster & species (sama2 satu kelompok atau sama2 beda kelompok). NMI: seberapa banyak info species yg ketangkep kluster, 0-1. dua2nya ga peduli nomor kluster (kluster 0 ga harus = adelie)
32. RI / NMI: GMM 0,982 / 0,935 > agglomerative 0,961 / 0,901 > spectral 0,917 / 0,831 > DBSCAN 0,821 / 0,730
33. tabel silang: gentoo selalu bener di semua algoritma. yg ketuker selalu adelie <-> chinstrap
34. uji kestabilan: ambil 90% data acak (307 titik) 3x (rng seed 42), jalanin ulang tiap algoritma, terus label-nya dibandingin sama label data penuh di titik yg sama pake rand index (1 = sama persis). nomor kluster boleh beda, RI ga peduli
35. hasil stabilitas rata2: spectral 1,000, GMM 0,999, DBSCAN 0,997, agglomerative 0,970. agglomerative paling goyang, kemungkinan krn hilang beberapa titik bisa ngubah urutan gabungan di ward
36. semua ≥ 0,97 -> perubahan kecil di data ga ngubah hasil banyak

## Kesimpulan

37. GMM paling cocok: RI & NMI paling tinggi, cuma 5 dari 342 yg salah, stabil 0,999
38. alasannya: ukuran badan penguin saling berkorelasi (flipper vs body_mass 0,87), jadi sebaran tiap spesies lonjong/miring, dan jumlahnya beda2 (chinstrap 68 vs adelie 151). GMM bisa nangkep itu krn tiap kluster punya kovarians sendiri. ward lebih suka kluster bulat & seimbang
39. silhouette GMM bukan yg paling tinggi, tapi silhouette cuma ngukur seberapa misah klusternya, bukan seberapa sesuai sama spesies. adelie & chinstrap emang nempel, jadi silhouette semua algoritma k=3 cuma sedang (~0,45)
40. DBSCAN paling ga cocok buat dataset ini: kepadatan adelie & chinstrap nyambung, jadi cuma ketemu 2 kluster
