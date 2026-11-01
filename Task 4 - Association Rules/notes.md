### Notes

# Manual

1. yang 17920 missing perbatasan 17920 and 12838, which id is that...

# Notebook

1. awal 541.909 baris, 25.900 invoice. yang kepake cuma InvoiceNo + Description, CustomerID kosong biarin aja ga dipake
2. description kosong 1.454 baris, ternyata tiap baris itu invoice sendiri jadi invoice langsung turun 1.454 juga
3. abis buang yg batal (C) sisa qty <= 0 tinggal 474 baris
4. description di-strip, banyak yg ada spasi di belakang, produk unik 4.077 -> 4.065
5. POSTAGE, DOTCOM POSTAGE, Manual, CARRIAGE dibuang, itu ongkir/input manual bukan produk. kalo ga dibuang ada 62 aturan isinya ongkir. ini ga diminta tugas jadi jelasin di laporan
6. akhirnya 528.390 baris, 19.973 invoice, basket 19.973 x 4.061, rata2 26,5 produk per invoice
7. 0.01 / 0.5 -> 816 aturan, kebanyakan. 78% support-nya < 0,015 (pas2an), top lift isinya HERB MARKER semua
8. jadi pake 0.015 / 0.6 -> 97 aturan. 0.02 udah buang pasangan yg jelas nyambung (tea plate, playhouse), 0.03 cuma 3-11 aturan
9. top 3 lift: tea plate green -> roses (37,6), playhouse bedroom -> kitchen (33,9), red spotty cups -> plates (31,0). semua satu seri produk -> bundling / taruh sebelahan / rekomendasi
10. A -> B sama B -> A lift-nya sama, jadi top 3 diambil satu arah aja biar ga dobel
11. lift tinggi tapi support kecil (1,6 - 1,8%), kuat buat rekomendasi tapi bukan pola kebanyakan pembeli
12. tugas minta pd.read_excel, aku pake csv (isinya sama 541.909 baris)
13. df.describe -> df.describe() (tadinya cuma keluar method)
14. run all sekitar 45 detik, paling lama apriori 0.01
15. dataset belum masuk .gitignore, tugas bilang ga usah diupload
16. kumpul: folder tugas-association-rule, NRP_Nama_Tugas_Association_Rule .ipynb + .pdf, deadline 1 nov 23:59
