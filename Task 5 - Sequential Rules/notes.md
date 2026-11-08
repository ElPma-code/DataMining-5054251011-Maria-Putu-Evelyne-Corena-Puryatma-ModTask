### Notes

# Notebook

## Data & pembersihan

1. awal 541.909 baris, 25.900 invoice, 4.372 pelanggan. yang kepake: CustomerID (siapa), InvoiceDate (kapan), InvoiceNo (1 invoice = 1 itemset), Description (produk)
2. description kosong 1.454 baris, semuanya juga no CustomerID, jumlah pelanggan ga berubah (tetep 4.372)
3. after buang yg batal (C) pelanggan turun 4.372 -> 4.339, berarti ada 33 pelanggan yg isinya cuma transaksi batal
4. CustomerID kosong 135.080 baris (24,9%), wajib dibuang krn sequence disusun per pelanggan. ini yg paling banyak ngurangin baris (530.693 -> 397.924)
5. description di-strip + spasi ganda dirapihin, contoh "LUNCH BAG SUKI DESIGN" sama "LUNCH BAG SUKI DESIGN" tadinya kebaca 2 produk beda. produk unik 3.877 -> 3.858
6. POSTAGE, DOTCOM POSTAGE, Manual, CARRIAGE dibuang sama kayak tugas 4 (ongkir/input manual, bukan produk) untuk report. 3 pelanggan ilang krn isinya cuma ongkir (4.339 -> 4.336)
7. akhirnya 396.386 baris, 18.416 invoice, 4.336 pelanggan, 3.854 produk
8. invoice per pelanggan: median 2, rata2 4,2, max 206. 1.506 pelanggan (34,7%) cuma belanja sekali -> ga punya urutan, tapi tetep dihitung di penyebut support (tugas bilang relatif thd jumlah pelanggan)

## Persiapan sequence

9. data diurutin CustomerID + InvoiceDate dulu, baru digroup per invoice. 1 itemset = produk unik di 1 invoice (pake set, quantity ga dipake)
10. ada 30 invoice yg tanggalnya lebih dari 1 (beda menit), dipake yg paling awal ('first' setelah diurutin)
11. 1 pelanggan = 1 sequence = list itemset urut waktu. semua disimpen jadi `sequences` (list of list) sesuai tugas
12. contoh di notebook pelanggan 12347, 7 invoice, cuma ditampilin 3 produk pertama per invoice biar ga kepanjangan

## PrefixSpan

13. library `prefixspan` (pip) cuma bisa sequence isi item tunggal, ga bisa itemset (beberapa produk per invoice). SPMF butuh java jadi PrefixSpan ditulis sendiri ±25 baris
14. mlxtend ga punya `sequential_rules`, import itu dihapus
15. pola yg dicari A -> B -> C, tiap langkah 1 produk di invoice yg lebih belakang. produk dalam 1 invoice yg sama ga dianggap urutan (itu udah association rule tugas 4), jadi ga ada pola kayak {A, B} -> C
16. cara kerja: hitung pelanggan per produk -> yg lolos min_support jadi prefix -> potong sequence tiap pelanggan setelah invoice tempat prefix pertama kali ketemu (projected database) -> hitung lagi produk di sisa -> sambung ke prefix -> ulang sampe ga ada yg lolos
17. dipake kemunculan pertama prefix (paling awal) biar sisa sequence paling panjang, jadi ga ada pola yg kelewat
18. support = pelanggan yg punya pola / 4.336. 1 pelanggan dihitung sekali walau polanya kejadian berkali2
19. confidence A -> B = support(A -> B) / support(A) = dari yg pernah beli A, berapa persen yg abis itu beli B. pola 3 langkah: support(A -> B -> C) / support(A -> B). pola 1 langkah ga ada confidence-nya, jadi ga ditampilin (isinya cuma produk laris)

## Pilih min_support

20. 0.01 (min 44 pelanggan) -> 45.303 pola, sampe 7 langkah, 85% support < 0.015 (pas2an). kebanyakan
21. penyebab meledak: pelanggan grosir belanja puluhan-ratusan kali (max 206 invoice), hampir semua kombinasi urutan produk kejadian di mereka
22. tabel perbandingan cukup disaring dari hasil 0.01, ga perlu run ulang (pola yg lolos support gede pasti lolos 0.01)
23. 0.015 -> 6.675, 0.02 -> 1.973, masih ribuan. 0.04 -> 59, 0.05 -> 10 dan semuanya beli ulang produk yg sama (ga ada pola produk beda)
24. jadi pake 0.03 (min 131 pelanggan) -> 294 pola: 283 dua langkah, 10 tiga langkah, 1 empat langkah, 228 ada produk bedanya

## Hasil

25. top 3 support semuanya beli ulang produk yg sama:
    - WHITE HANGING HEART T-LIGHT HOLDER -> sama: 405 pelanggan (9,3%), conf 0,473 (dari 856 pembeli)
    - REGENCY CAKESTAND 3 TIER -> sama: 330 pelanggan (7,6%), conf 0,375 (dari 881 pembeli)
    - JUMBO BAG RED RETROSPOT -> sama: 312 pelanggan (7,2%), conf 0,491 (dari 635 pembeli)
26. bisnis: produk andalan yg dibeli berulang -> jaga stok, kirim pengingat "beli lagi", harga grosir / diskon pembelian ulang. regency conf paling kecil kemungkinan krn lebih mahal & awet, tapi pembeli ulangnya tetep banyak (kemungkinan toko/reseller)
27. tugas cuma minta top 3 berdasar support, jadi pola produk beda ditaruh sbg pelengkap. paling tinggi LUNCH BAG RED RETROSPOT -> LUNCH BAG BLACK SKULL. (212 pelanggan, 4,9%, conf 0,398). isinya didominasi seri LUNCH BAG & JUMBO BAG -> abis beli 1 motif, rekomendasi motif lain dari seri yg sama
28. conf paling tinggi: JUMBO BAG RED RETROSPOT -> LUNCH BAG RED RETROSPOT -> JUMBO BAG RED RETROSPOT (0,670), white hanging heart 4x berturut2 (0,631). makin sering pelanggan beli ulang, makin besar peluang beli lagi
29. support semua pola kecil (3-9%) krn sepertiga pelanggan cuma belanja sekali
