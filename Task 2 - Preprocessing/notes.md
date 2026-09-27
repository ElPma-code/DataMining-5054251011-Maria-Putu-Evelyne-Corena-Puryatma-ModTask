Tugas Praktikum 2: Praproses Data

Deskripsi Singkat
Pada praktikum ini, mahasiswa melakukan tahapan praproses data agar dataset siap digunakan untuk analisis atau model machine learning: menangani nilai yang hilang, mendeteksi dan menangani outlier, serta melakukan transformasi data (normalisasi dan encoding).

Tujuan Praktikum
Memahami dan menerapkan langkah-langkah praproses data seperti pembersihan, transformasi, dan reduksi data.
Meningkatkan kualitas data melalui penanganan nilai yang hilang dan data yang tidak konsisten.
Menerapkan teknik transformasi data seperti normalisasi dan encoding.

Ketentuan Dataset
Dataset: House Prices - Advanced Regression Techniques (Kaggle), berisi informasi harga rumah beserta atribut seperti ukuran, tahun dibangun, dan kondisi rumah.
Link: https://www.kaggle.com/competitions/house-prices-advanced-regression-techniques/data?select=train.csv
Gunakan file train.csv saja (1460 baris, 81 kolom).

Langkah-Langkah Praktikum

1. Unduh dan Import Dataset
   Unduh train.csv dari link di atas, lalu impor menggunakan pandas.
   Tampilkan .head(), .shape, dan .info() untuk memahami struktur data.
2. Pembersihan Data
   Periksa jumlah nilai yang hilang pada setiap atribut menggunakan pandas.
   Hapus kolom/atribut dengan proporsi nilai hilang lebih dari 50%.
   Tangani nilai hilang

3. Deteksi dan Penanganan Outlier
   Gunakan boxplot untuk mendeteksi outlier pada atribut numerik.
   Tentukan apakah outlier dihapus atau disesuaikan, dan jelaskan alasannya.
4. Transformasi Data
   Lakukan normalisasi/standarisasi atribut.
   Lakukan encoding atribut kategoris menggunakan one-hot encoding.
5. Reduksi Dimensi
   Gunakan analisis korelasi untuk mengidentifikasi atribut yang sangat berkorelasi, lalu buang salah satunya jika perlu.
   Gunakan PCA (Principal Component Analysis) untuk mengurangi dimensi data.
6. Penyusunan Laporan
   Tulis laporan minimal 2 halaman, dilengkapi dengan visualisasi, berisi:
   Langkah-langkah praproses yang dilakukan.
   Hasil dari setiap tahapan praproses.
   Ringkasan dataset akhir setelah praproses.

Hasil yang Diharapkan
Dataset yang bersih dan siap digunakan, dengan nilai hilang dan outlier sudah ditangani.
Transformasi data yang telah dilakukan (normalisasi/standarisasi dan encoding).
Laporan minimal 2 halaman yang mencakup hasil tiap langkah praproses, dilengkapi dengan visualisasi.

# About Data (from Kaggle)

MSSubClass: Identifies the type of dwelling involved in the sale.

        20	1-STORY 1946 & NEWER ALL STYLES
        30	1-STORY 1945 & OLDER
        40	1-STORY W/FINISHED ATTIC ALL AGES
        45	1-1/2 STORY - UNFINISHED ALL AGES
        50	1-1/2 STORY FINISHED ALL AGES
        60	2-STORY 1946 & NEWER
        70	2-STORY 1945 & OLDER
        75	2-1/2 STORY ALL AGES
        80	SPLIT OR MULTI-LEVEL
        85	SPLIT FOYER
        90	DUPLEX - ALL STYLES AND AGES
       120	1-STORY PUD (Planned Unit Development) - 1946 & NEWER
       150	1-1/2 STORY PUD - ALL AGES
       160	2-STORY PUD - 1946 & NEWER
       180	PUD - MULTILEVEL - INCL SPLIT LEV/FOYER
       190	2 FAMILY CONVERSION - ALL STYLES AND AGES

MSZoning: Identifies the general zoning classification of the sale.
A Agriculture
C Commercial
FV Floating Village Residential
I Industrial
RH Residential High Density
RL Residential Low Density
RP Residential Low Density Park
RM Residential Medium Density
LotFrontage: Linear feet of street connected to property

LotArea: Lot size in square feet

Street: Type of road access to property

       Grvl	Gravel
       Pave	Paved

Alley: Type of alley access to property

       Grvl	Gravel
       Pave	Paved
       NA 	No alley access

LotShape: General shape of property

       Reg	Regular
       IR1	Slightly irregular
       IR2	Moderately Irregular
       IR3	Irregular

LandContour: Flatness of the property

       Lvl	Near Flat/Level
       Bnk	Banked - Quick and significant rise from street grade to building
       HLS	Hillside - Significant slope from side to side
       Low	Depression

Utilities: Type of utilities available
AllPub All public Utilities (E,G,W,& S)
NoSewr Electricity, Gas, and Water (Septic Tank)
NoSeWa Electricity and Gas Only
ELO Electricity only
LotConfig: Lot configuration

       Inside	Inside lot
       Corner	Corner lot
       CulDSac	Cul-de-sac
       FR2	Frontage on 2 sides of property
       FR3	Frontage on 3 sides of property

LandSlope: Slope of property
Gtl Gentle slope
Mod Moderate Slope
Sev Severe Slope
Neighborhood: Physical locations within Ames city limits

       Blmngtn	Bloomington Heights
       Blueste	Bluestem
       BrDale	Briardale
       BrkSide	Brookside
       ClearCr	Clear Creek
       CollgCr	College Creek
       Crawfor	Crawford
       Edwards	Edwards
       Gilbert	Gilbert
       IDOTRR	Iowa DOT and Rail Road
       MeadowV	Meadow Village
       Mitchel	Mitchell
       Names	North Ames
       NoRidge	Northridge
       NPkVill	Northpark Villa
       NridgHt	Northridge Heights
       NWAmes	Northwest Ames
       OldTown	Old Town
       SWISU	South & West of Iowa State University
       Sawyer	Sawyer
       SawyerW	Sawyer West
       Somerst	Somerset
       StoneBr	Stone Brook
       Timber	Timberland
       Veenker	Veenker

Condition1: Proximity to various conditions
Artery Adjacent to arterial street
Feedr Adjacent to feeder street
Norm Normal
RRNn Within 200' of North-South Railroad
RRAn Adjacent to North-South Railroad
PosN Near positive off-site feature--park, greenbelt, etc.
PosA Adjacent to postive off-site feature
RRNe Within 200' of East-West Railroad
RRAe Adjacent to East-West Railroad
Condition2: Proximity to various conditions (if more than one is present)
Artery Adjacent to arterial street
Feedr Adjacent to feeder street
Norm Normal
RRNn Within 200' of North-South Railroad
RRAn Adjacent to North-South Railroad
PosN Near positive off-site feature--park, greenbelt, etc.
PosA Adjacent to postive off-site feature
RRNe Within 200' of East-West Railroad
RRAe Adjacent to East-West Railroad
BldgType: Type of dwelling
1Fam Single-family Detached
2FmCon Two-family Conversion; originally built as one-family dwelling
Duplx Duplex
TwnhsE Townhouse End Unit
TwnhsI Townhouse Inside Unit
HouseStyle: Style of dwelling
1Story One story
1.5Fin One and one-half story: 2nd level finished
1.5Unf One and one-half story: 2nd level unfinished
2Story Two story
2.5Fin Two and one-half story: 2nd level finished
2.5Unf Two and one-half story: 2nd level unfinished
SFoyer Split Foyer
SLvl Split Level
OverallQual: Rates the overall material and finish of the house

       10	Very Excellent
       9	Excellent
       8	Very Good
       7	Good
       6	Above Average
       5	Average
       4	Below Average
       3	Fair
       2	Poor
       1	Very Poor

OverallCond: Rates the overall condition of the house

       10	Very Excellent
       9	Excellent
       8	Very Good
       7	Good
       6	Above Average
       5	Average
       4	Below Average
       3	Fair
       2	Poor
       1	Very Poor

YearBuilt: Original construction date

YearRemodAdd: Remodel date (same as construction date if no remodeling or additions)

RoofStyle: Type of roof

       Flat	Flat
       Gable	Gable
       Gambrel	Gabrel (Barn)
       Hip	Hip
       Mansard	Mansard
       Shed	Shed

RoofMatl: Roof material

       ClyTile	Clay or Tile
       CompShg	Standard (Composite) Shingle
       Membran	Membrane
       Metal	Metal
       Roll	Roll
       Tar&Grv	Gravel & Tar
       WdShake	Wood Shakes
       WdShngl	Wood Shingles

Exterior1st: Exterior covering on house

       AsbShng	Asbestos Shingles
       AsphShn	Asphalt Shingles
       BrkComm	Brick Common
       BrkFace	Brick Face
       CBlock	Cinder Block
       CemntBd	Cement Board
       HdBoard	Hard Board
       ImStucc	Imitation Stucco
       MetalSd	Metal Siding
       Other	Other
       Plywood	Plywood
       PreCast	PreCast
       Stone	Stone
       Stucco	Stucco
       VinylSd	Vinyl Siding
       Wd Sdng	Wood Siding
       WdShing	Wood Shingles

Exterior2nd: Exterior covering on house (if more than one material)

       AsbShng	Asbestos Shingles
       AsphShn	Asphalt Shingles
       BrkComm	Brick Common
       BrkFace	Brick Face
       CBlock	Cinder Block
       CemntBd	Cement Board
       HdBoard	Hard Board
       ImStucc	Imitation Stucco
       MetalSd	Metal Siding
       Other	Other
       Plywood	Plywood
       PreCast	PreCast
       Stone	Stone
       Stucco	Stucco
       VinylSd	Vinyl Siding
       Wd Sdng	Wood Siding
       WdShing	Wood Shingles

MasVnrType: Masonry veneer type

       BrkCmn	Brick Common
       BrkFace	Brick Face
       CBlock	Cinder Block
       None	None
       Stone	Stone

MasVnrArea: Masonry veneer area in square feet

ExterQual: Evaluates the quality of the material on the exterior
Ex Excellent
Gd Good
TA Average/Typical
Fa Fair
Po Poor
ExterCond: Evaluates the present condition of the material on the exterior
Ex Excellent
Gd Good
TA Average/Typical
Fa Fair
Po Poor
Foundation: Type of foundation
BrkTil Brick & Tile
CBlock Cinder Block
PConc Poured Contrete
Slab Slab
Stone Stone
Wood Wood
BsmtQual: Evaluates the height of the basement

       Ex	Excellent (100+ inches)
       Gd	Good (90-99 inches)
       TA	Typical (80-89 inches)
       Fa	Fair (70-79 inches)
       Po	Poor (<70 inches
       NA	No Basement

BsmtCond: Evaluates the general condition of the basement

       Ex	Excellent
       Gd	Good
       TA	Typical - slight dampness allowed
       Fa	Fair - dampness or some cracking or settling
       Po	Poor - Severe cracking, settling, or wetness
       NA	No Basement

BsmtExposure: Refers to walkout or garden level walls

       Gd	Good Exposure
       Av	Average Exposure (split levels or foyers typically score average or above)
       Mn	Mimimum Exposure
       No	No Exposure
       NA	No Basement

BsmtFinType1: Rating of basement finished area

       GLQ	Good Living Quarters
       ALQ	Average Living Quarters
       BLQ	Below Average Living Quarters
       Rec	Average Rec Room
       LwQ	Low Quality
       Unf	Unfinshed
       NA	No Basement

BsmtFinSF1: Type 1 finished square feet

BsmtFinType2: Rating of basement finished area (if multiple types)

       GLQ	Good Living Quarters
       ALQ	Average Living Quarters
       BLQ	Below Average Living Quarters
       Rec	Average Rec Room
       LwQ	Low Quality
       Unf	Unfinshed
       NA	No Basement

BsmtFinSF2: Type 2 finished square feet

BsmtUnfSF: Unfinished square feet of basement area

TotalBsmtSF: Total square feet of basement area

Heating: Type of heating
Floor Floor Furnace
GasA Gas forced warm air furnace
GasW Gas hot water or steam heat
Grav Gravity furnace
OthW Hot water or steam heat other than gas
Wall Wall furnace
HeatingQC: Heating quality and condition

       Ex	Excellent
       Gd	Good
       TA	Average/Typical
       Fa	Fair
       Po	Poor

CentralAir: Central air conditioning

       N	No
       Y	Yes

Electrical: Electrical system

       SBrkr	Standard Circuit Breakers & Romex
       FuseA	Fuse Box over 60 AMP and all Romex wiring (Average)
       FuseF	60 AMP Fuse Box and mostly Romex wiring (Fair)
       FuseP	60 AMP Fuse Box and mostly knob & tube wiring (poor)
       Mix	Mixed

1stFlrSF: First Floor square feet

2ndFlrSF: Second floor square feet

LowQualFinSF: Low quality finished square feet (all floors)

GrLivArea: Above grade (ground) living area square feet

BsmtFullBath: Basement full bathrooms

BsmtHalfBath: Basement half bathrooms

FullBath: Full bathrooms above grade

HalfBath: Half baths above grade

Bedroom: Bedrooms above grade (does NOT include basement bedrooms)

Kitchen: Kitchens above grade

KitchenQual: Kitchen quality

       Ex	Excellent
       Gd	Good
       TA	Typical/Average
       Fa	Fair
       Po	Poor

TotRmsAbvGrd: Total rooms above grade (does not include bathrooms)

Functional: Home functionality (Assume typical unless deductions are warranted)

       Typ	Typical Functionality
       Min1	Minor Deductions 1
       Min2	Minor Deductions 2
       Mod	Moderate Deductions
       Maj1	Major Deductions 1
       Maj2	Major Deductions 2
       Sev	Severely Damaged
       Sal	Salvage only

Fireplaces: Number of fireplaces

FireplaceQu: Fireplace quality

       Ex	Excellent - Exceptional Masonry Fireplace
       Gd	Good - Masonry Fireplace in main level
       TA	Average - Prefabricated Fireplace in main living area or Masonry Fireplace in basement
       Fa	Fair - Prefabricated Fireplace in basement
       Po	Poor - Ben Franklin Stove
       NA	No Fireplace

GarageType: Garage location
2Types More than one type of garage
Attchd Attached to home
Basment Basement Garage
BuiltIn Built-In (Garage part of house - typically has room above garage)
CarPort Car Port
Detchd Detached from home
NA No Garage
GarageYrBlt: Year garage was built
GarageFinish: Interior finish of the garage

       Fin	Finished
       RFn	Rough Finished
       Unf	Unfinished
       NA	No Garage

GarageCars: Size of garage in car capacity

GarageArea: Size of garage in square feet

GarageQual: Garage quality

       Ex	Excellent
       Gd	Good
       TA	Typical/Average
       Fa	Fair
       Po	Poor
       NA	No Garage

GarageCond: Garage condition

       Ex	Excellent
       Gd	Good
       TA	Typical/Average
       Fa	Fair
       Po	Poor
       NA	No Garage

PavedDrive: Paved driveway

       Y	Paved
       P	Partial Pavement
       N	Dirt/Gravel

WoodDeckSF: Wood deck area in square feet

OpenPorchSF: Open porch area in square feet

EnclosedPorch: Enclosed porch area in square feet

3SsnPorch: Three season porch area in square feet

ScreenPorch: Screen porch area in square feet

PoolArea: Pool area in square feet

PoolQC: Pool quality
Ex Excellent
Gd Good
TA Average/Typical
Fa Fair
NA No Pool
Fence: Fence quality
GdPrv Good Privacy
MnPrv Minimum Privacy
GdWo Good Wood
MnWw Minimum Wood/Wire
NA No Fence
MiscFeature: Miscellaneous feature not covered in other categories
Elev Elevator
Gar2 2nd Garage (if not described in garage section)
Othr Other
Shed Shed (over 100 SF)
TenC Tennis Court
NA None
MiscVal: $Value of miscellaneous feature

MoSold: Month Sold (MM)

YrSold: Year Sold (YYYY)

SaleType: Type of sale
WD Warranty Deed - Conventional
CWD Warranty Deed - Cash
VWD Warranty Deed - VA Loan
New Home just constructed and sold
COD Court Officer Deed/Estate
Con Contract 15% Down payment regular terms
ConLw Contract Low Down payment and low interest
ConLI Contract Low Interest
ConLD Contract Low Down
Oth Other
SaleCondition: Condition of sale

       Normal	Normal Sale
       Abnorml	Abnormal Sale -  trade, foreclosure, short sale
       AdjLand	Adjoining Land Purchase
       Alloca	Allocation - two linked properties with separate deeds, typically condo with a garage unit
       Family	Sale between family members
       Partial	Home was not completed when last assessed (associated with New Homes)

## Notes

1. IQR (aturan Tukey): nilai di bawah Q1 - 1.5 x IQR atau di atas Q3 + 1.5 x IQR dianggap outlier.
2. Skewness: ukuran kemiringan sebaran. 0 berarti simetris, di atas 1 berarti ekor kanan panjang (banyak nilai kecil, sedikit nilai sangat besar).
3. Pearson (r) mengukur hubungan linear. Spearman (rho) mengukur hubungan berdasarkan urutan (ranking) dan lebih tahan terhadap outlier. Kalau rho jauh lebih besar dari r, hubungannya ada tetapi tidak linear atau terganggu nilai ekstrem.
4. eta (rasio korelasi): kekuatan hubungan fitur kategorik dengan fitur angka, dari 0 sampai 1. Dipakai karena Pearson tidak cocok untuk kategori.
5. NA struktural: NA yang artinya "fasilitasnya tidak ada" (misalnya tidak punya garasi), bukan data yang lupa diisi.
6. log1p: log(1 + x). Dipakai supaya nilai 0 tetap bisa di-log.
7. PCA: merangkum banyak fitur menjadi sedikit komponen baru yang tetap menyimpan sebagian besar variasi data.

## 1. Data before

### Struktur dan tipe data

1. 81 kolom: 43 object, 35 int64, 3 float64. Tidak ada baris duplikat dan `Id` unik.
2. Kalau dilihat dari maknanya (bukan hanya dtype), di luar `Id` dan `SalePrice` ada 33 fitur numerik (19 kontinu, 9 diskrit/hitungan, 5 waktu) dan 46 fitur kategorik (15 ordinal teks, 28 nominal teks, 3 yang disimpan sebagai angka).
3. Jebakan tipe data:
   - `MSSubClass` berupa angka (20, 60, 120, ...) tetapi sebenarnya kode tipe bangunan, jadi harus diperlakukan sebagai kategori nominal;
   - `OverallQual` dan `OverallCond` adalah skala 1-10 yang berurutan (ordinal);
   - `LotFrontage`, `MasVnrArea`, `GarageYrBlt` bertipe float hanya karena ada NaN, padahal semua nilainya bulat.

### Target: SalePrice

1. Mean 180921 lebih besar dari median 163000, skew 1.88, rentang 34900 - 755000. Sebarannya miring ke kanan.
2. 61 rumah berada di atas batas atas IQR (340038). 58 di antaranya berkualitas 8-10, jadi ini rumah mahal yang sah, bukan salah input.
3. Setelah log1p skew-nya turun menjadi 0.12 (hampir normal). Karena itu target dipakai dalam bentuk log.

### Sebaran fitur

1. Banyak fitur hampir selalu bernilai 0: `PoolArea` 99.5%, `3SsnPorch` 98.4%, `LowQualFinSF` 98.2%, `MiscVal` 96.4%, `ScreenPorch` 92.1%, `BsmtFinSF2` 88.6%, `EnclosedPorch` 85.8%. Fitur seperti ini lebih mirip penanda ada/tidak ada fasilitas.
2. `LotArea` paling miring (skew 12.2): maksimum 215245 sqft, sekitar 23 kali mediannya (9478).
3. Fitur kategorik yang hampir konstan: `Utilities` (hanya 1 rumah yang berbeda), `Street` 99.6%, `Condition2` 99.0%, `RoofMatl` 98.2%, `Heating` 97.8%.
4. Fitur ordinal kualitas didominasi TA (rata-rata), misalnya `GarageQual` dan `GarageCond` sekitar 95% dari baris yang terisi.

### Yang berhubungan dengan harga

1. Fitur numerik terkuat (Pearson): `OverallQual` 0.79, `GrLivArea` 0.71, `GarageCars` 0.64, `GarageArea` 0.62, `TotalBsmtSF` 0.61, `1stFlrSF` 0.61.
2. Fitur kategorik terkuat (eta): `OverallQual` 0.83, `Neighborhood` 0.74, `ExterQual` 0.69, `BsmtQual` 0.68, `KitchenQual` 0.68.
3. Lokasi berpengaruh besar: median harga termurah di MeadowV (88000), termahal di NridgHt (315000).
4. Pada fitur kualitas (Fa < TA < Gd < Ex) median harga naik berurutan. Ini dasar saya memakai encoding ordinal untuk fitur-fitur tersebut.
5. Kategori "tidak ada" (tanpa garasi, basement, atau perapian) selalu masuk kelompok termurah. Jadi "tidak ada" itu informasi, bukan data yang boleh dibuang.
6. `YearBuilt`: Spearman 0.65 lebih besar dari Pearson 0.52. Hubungannya tidak linear; harga melonjak untuk rumah yang dibangun setelah sekitar 1990.
7. Temuan yang awalnya aneh: rumah mahal justru menumpuk di `OverallCond` = 5 (rata-rata). Ternyata rumah dengan kondisi 5 umumnya rumah baru (median dibangun 1998), sedangkan kondisi 6-8 kebanyakan rumah tua.
8. Hampir tidak berpengaruh ke harga: `MoSold`, `YrSold`, dan fitur yang hampir selalu 0.

### Pasangan fitur yang mengukur hal yang sama

`GarageArea` - `GarageCars` (0.88), `GarageYrBlt` - `YearBuilt` (0.83), `TotRmsAbvGrd` - `GrLivArea` (0.83), `1stFlrSF` - `TotalBsmtSF` (0.82). Pasangan ini jadi kandidat untuk dibuang salah satunya di tahap reduksi.

## 2. Pembersihan data

### Nilai kosong: temuan terpenting

1. Ada 19 kolom dengan total 7829 sel kosong, tetapi 7551 sel (96.4%) bersifat struktural: menurut dokumentasi dataset, NA berarti fasilitasnya tidak ada.
2. Mencocokkan ke kolom pasangannya:
   - `PoolQC` kosong tepat di 1453 rumah dengan `PoolArea` = 0;
   - `FireplaceQu` kosong tepat di 690 rumah dengan `Fireplaces` = 0;
   - lima kolom garasi kosong di 81 rumah yang sama, semuanya dengan `GarageArea` = 0;
   - lima kolom basement kosong di 37 rumah dengan `TotalBsmtSF` = 0.
3. Yang benar-benar hilang hanya 278 sel: `LotFrontage` 259, `MasVnrArea` 8, `MasVnrType` 8, `BsmtExposure` 1 (Id 949), `BsmtFinType2` 1 (Id 333), `Electrical` 1 (Id 1380).
4. Jebakan pandas: teks "None" di `MasVnrType` otomatis dibaca sebagai NaN. Kolom ini tercatat 59.7% kosong, padahal 864 dari 872 sel adalah kategori "tanpa pelapis batu" dan hanya 8 yang benar-benar kosong.
5. `LotFrontage` kosong tidak acak: 52% pada kavling CulDSac vs 13% pada kavling Inside, dan di lingkungan ClearCr sampai 54%. Jadi mengisi dengan median global kurang tepat.

### Penanganan nilai kosong

1. Buang 5 kolom yang kosong lebih dari 50% (sesuai instruksi): `PoolQC`, `MiscFeature`, `Alley`, `Fence`, `MasVnrType`.
   - Informasinya tidak banyak hilang karena ada kolom pengganti yang tetap disimpan: `PoolArea`, `MiscVal`, `MasVnrArea`.
   - `Alley` dan `Fence` tidak punya pengganti, tetapi hubungannya dengan harga memang lemah (eta 0.14 dan 0.19).
   - Catatan jujur: `MasVnrType` sebenarnya hanya 0.5% kosong dan cukup berhubungan dengan harga (eta 0.43). Tetap saya buang supaya mengikuti aturan tugas; informasinya sebagian besar sudah terwakili `MasVnrArea`.
2. NA struktural diisi "Tidak Ada": `FireplaceQu`, 4 kolom kategorik garasi, dan 5 kolom basement. `GarageYrBlt` untuk rumah tanpa garasi diisi `YearBuilt`, supaya tidak muncul tahun 0 yang menjadi outlier buatan.
3. `LotFrontage` diisi dengan KNN (k=5) berdasarkan log `LotArea` dan luas bangunan. Metode ini dipilih setelah diuji: 20% nilai asli saya sembunyikan, diisi dengan tiap metode, lalu dibandingkan dengan nilai sebenarnya, diulang 20 kali. Rata-rata galat (MAE):
   - KNN (LotArea + luas bangunan): 11.28 ft (dipilih);
   - KNN (LotArea saja): 12.04 ft;
   - median per Neighborhood: 12.78 ft;
   - median global: 16.42 ft.
4. Sisanya diisi dengan logika dari data:
   - `MasVnrArea` (8 baris) diisi 0, karena tipe pelapisnya juga kosong dan 0 adalah nilai tersering;
   - `Electrical` (Id 1380, dibangun 2006) diisi SBrkr, karena semua rumah yang dibangun sejak 2000 memakai SBrkr;
   - `BsmtExposure` (Id 949) diisi No, modus rumah yang punya basement;
   - `BsmtFinType2` (Id 333) diisi Rec, bukan modus umum Unf, karena rumah ini punya area basement jadi seluas 479 sqft.
5. Jumlah sel kosong: 7829 -> 1550 (setelah buang kolom) -> 270 (setelah NA struktural) -> 0.
6. Efek samping yang perlu diingat: hasil imputasi KNN lebih mengumpul di tengah (80% berada di 49-94 ft) karena KNN merata-ratakan tetangga.

### Data tidak konsisten

1. Label salah tulis di `Exterior2nd`: "Brk Cmn", "CmentBd", "Wd Shng" diseragamkan menjadi "BrkComm", "CemntBd", "WdShing" seperti di `Exterior1st` (105 baris). Tanpa perbaikan ini, one-hot akan membuat dua kolom untuk material yang sama.
2. `MasVnrArea` bernilai 1 sqft padahal tipenya "None" (Id 774 dan 1231), jadi diubah menjadi 0.
3. Id 524 tercatat direnovasi 2008 padahal terjual 2007. Ternyata rumah ini salah satu anomali harga dan dibuang di tahap outlier.
4. `GarageYrBlt` lebih kecil dari `YearBuilt` di 9 rumah (selisih 1-10 tahun). Saya biarkan karena masih masuk akal, misalnya garasi lama dipertahankan saat rumah dibangun ulang.
5. Pengecekan penjumlahan luas lolos di semua baris: `TotalBsmtSF` = `BsmtFinSF1` + `BsmtFinSF2` + `BsmtUnfSF`, dan `GrLivArea` = `1stFlrSF` + `2ndFlrSF` + `LowQualFinSF`.

## 3. Outlier

### Membaca hasil boxplot

Jumlah outlier IQR tidak bisa langsung dipercaya. Saya memilahnya menjadi tiga jenis:

1. Artefak IQR = 0 pada 9 fitur yang hampir selalu 0 (misalnya `EnclosedPorch` dengan 208 "outlier"). Karena Q1 = Q3, semua nilai selain 0 otomatis dianggap outlier. Ini bukan masalah data.
2. Nilai langka pada fitur diskrit atau kode (`OverallCond`, `MSSubClass`, `BedroomAbvGr`): hanya kategori yang jarang muncul, bukan nilai ekstrem.
3. Nilai ekstrem kontinu yang memang perlu diperiksa: `MasVnrArea`, `LotFrontage`, `LotArea`, `TotalBsmtSF`, `GrLivArea`, `SalePrice`.

Ada 387 baris yang punya minimal satu outlier kontinu, terlalu banyak untuk dibuang begitu saja.

### Keputusan

1. Dihapus: 2 baris, Id 524 dan 1299.
   - Keduanya rumah sangat besar (4676 dan 5642 sqft) dengan kualitas tertinggi (10), tetapi harganya hanya 184750 dan 160000.
   - Harga per sqft 40 dan 28 USD, sementara median rumah berkualitas 10 adalah 174 USD.
   - Harganya 5.4 dan 6.6 simpangan baku di bawah perkiraan dari luas dan kualitas.
   - Keduanya dijual Partial (rumah belum selesai dibangun), jadi bukan penjualan normal.
   - Efeknya: korelasi `GrLivArea` dengan harga naik dari 0.709 ke 0.735.
   - Tidak semua rumah murah dibuang. Id 31 dan 496 juga murah, tetapi kualitasnya 4, jadi harganya wajar. Rumah besar lain (Id 692 dan 1183) dipertahankan karena harganya sepadan (755000 dan 745000).
2. Disesuaikan (capping di persentil 99): hanya `LotArea`.
   - 15 kavling dipotong ke 35403 sqft. Skew turun dari 12.57 ke 2.20, dan korelasi dengan harga naik dari 0.268 ke 0.401.
   - Kavling raksasa itu nyata (daerah pinggiran seperti Timber dan ClearCr), tetapi harganya tidak naik sebanding luasnya. Karena itu nilainya disesuaikan, barisnya tidak dibuang.
   - Cara memilih: untuk setiap fitur kontinu saya coba capping dan melihat apakah korelasinya dengan harga membaik. Hanya `LotArea` yang jelas membaik; `GrLivArea` malah turun (-0.016), artinya nilai ekstremnya justru informatif. `LotFrontage` nyaris lolos (+0.0099).
3. Dibiarkan: rumah mahal di `SalePrice`, fitur yang hampir selalu 0, dan nilai langka pada fitur diskrit. Semuanya informasi nyata.

### Hasil pembersihan (train_clean.csv)

1. Ukuran 1458 x 76, tanpa sel kosong.
2. 25 dari 37 fitur numerik hampir tidak berubah (mean dan std bergeser kurang dari 0.5%).
3. Yang berubah hanya yang memang ditangani:
   - `LotArea` std turun 51% karena capping;
   - `PoolArea` mean turun 11.8% karena Id 1299 punya kolam (1 dari 7 kolam di data);
   - `GarageYrBlt` std naik 6.5% karena rumah tanpa garasi rata-rata dibangun tahun 1942.
4. Kesimpulan: pembersihan menghapus masalah tanpa mengubah karakter data.

## 4. Transformasi

1. Target dipisah: y = log1p(`SalePrice`). `Id` dibuang dari fitur karena hanya nomor urut.
2. Encoding:
   - 14 fitur ordinal diubah menjadi angka berurutan (Tidak Ada = 0, Po = 1, Fa = 2, TA = 3, Gd = 4, Ex = 5; `BsmtFinType`, `GarageFinish`, `BsmtExposure`, `Functional` memakai urutannya sendiri). Alasannya, urutan kualitas berhubungan dengan harga, sedangkan one-hot akan membuang urutan itu;
   - 25 fitur nominal (termasuk `MSSubClass`) di-one-hot menjadi 183 kolom, sehingga total X menjadi 232 kolom. Kalau semua kategorik di-one-hot, hasilnya 294 kolom.
3. log1p untuk 16 fitur kontinu yang miring, tetapi hanya kalau skew-nya benar-benar turun. `BsmtUnfSF` tidak di-log karena log justru membuat skew-nya dari 0.92 menjadi -2.18. Fitur yang hampir selalu 0 tetap miring walaupun sudah di-log, karena masalahnya adalah banyaknya nilai 0, bukan ekor yang panjang.
4. Standarisasi: StandardScaler untuk 49 kolom numerik (hasilnya mean 0, std 1). Kolom dummy dibiarkan 0/1.
   - Kenapa bukan Min-Max: bentuk sebarannya sama saja, tetapi Min-Max ditentukan oleh satu nilai terkecil dan terbesar. PCA butuh varians yang setara, jadi dipilih Standard.
   - Kenapa dummy tidak distandarisasi: dummy untuk kategori yang hanya dimiliki 1% rumah akan bernilai sekitar 10 dan mendominasi PCA.

## 5. Reduksi dimensi

1. Buang fitur hampir konstan (satu nilai mencakup lebih dari 99% baris): 69 kolom, yaitu `Street`, `Utilities`, `PoolArea`, dan dummy kategori langka (paling banyak 14 rumah). Kolom: 232 -> 163.
2. Buang fitur yang saling berkorelasi tinggi (|r| > 0.8): ada 29 pasangan dan 28 kolom dibuang. Dari setiap pasangan saya pertahankan fitur yang korelasinya ke log harga lebih kuat. Kolom: 163 -> 135. Jenis redundansinya:
   - kolom kembar hasil one-hot: `CentralAir_Y` / `CentralAir_N` (r = -1), `SaleType_New` / `SaleCondition_Partial` (0.99, rumah baru yang dijual sebelum selesai), dan material yang sama di `Exterior1st` / `Exterior2nd`;
   - kode yang tumpang tindih: `MSSubClass_90` sama persis dengan `BldgType_Duplex` (r = 1.00);
   - ukuran fisik yang sama: `GarageArea` / `GarageCars`, `GarageQual` / `GarageCond`, `GarageYrBlt` / `YearBuilt`, `TotRmsAbvGrd` / `GrLivArea`.
3. PCA: 80% varians butuh 24 komponen, 90% butuh 37, dan 95% butuh 51. Saya pakai 95%, jadi 135 fitur menjadi 51 komponen (berkurang 62%).
4. PC1 (19.4% varians) adalah sumbu "kualitas dan ukuran rumah": `OverallQual`, `ExterQual`, `YearBuilt`, `BsmtQual`, `KitchenQual`, `GarageCars`. Korelasinya dengan log harga 0.906, padahal PCA sama sekali tidak melihat harga.
5. PC2 (7.0%) membedakan rumah bertingkat (lantai 2, kamar tidur, half bath) dari rumah satu lantai dengan basement jadi.
6. 86.4% varians total berasal dari kolom numerik dan hanya 13.6% dari dummy, jadi komponen utama terutama dibentuk oleh fitur numerik.

## Ringkasan dataset akhir

| Tahap                               | Baris x kolom | Sel kosong |
| ----------------------------------- | ------------- | ---------- |
| Data mentah                         | 1460 x 81     | 7829       |
| Buang kolom kosong > 50%            | 1460 x 76     | 1550       |
| Isi NA struktural                   | 1460 x 76     | 270        |
| Imputasi nilai hilang               | 1460 x 76     | 0          |
| Hapus 2 anomali                     | 1458 x 76     | 0          |
| Capping LotArea (= train_clean.csv) | 1458 x 76     | 0          |
| Pisah Id dan target                 | 1458 x 74     | 0          |
| Encoding                            | 1458 x 232    | 0          |
| Buang fitur hampir konstan          | 1458 x 163    | 0          |
| Buang fitur berkorelasi tinggi      | 1458 x 135    | 0          |
| PCA 95% varians                     | 1458 x 51     | 0          |

Data siap model: 1458 x 135 (41 kolom numerik terstandarisasi dan 94 dummy 0/1) dengan target y = log1p(`SalePrice`). Kalau memakai PCA: 1458 x 51.

## Poin utama kesimpulam

1. NA di dataset ini sebagian besar berarti "tidak ada fasilitas". Hanya 278 dari 7829 sel kosong yang benar-benar hilang.
2. Outlier harus dipilah dulu sifatnya. Yang dibuang hanya 2 transaksi yang tidak wajar, `LotArea` disesuaikan, dan sisanya dipertahankan karena merupakan informasi nyata.
3. Keputusan imputasi dan capping diuji dengan angka (galat imputasi, perubahan korelasi), bukan sekadar tebakan.
4. Skala kualitas di-encode secara ordinal dan fitur nominal di-one-hot.
5. Redundansi paling banyak berasal dari one-hot dan kode yang tumpang tindih. PCA memperlihatkan satu sumbu utama (kualitas dan ukuran rumah) yang sangat terkait dengan harga.

## Visual

1. Jumlah fitur per jenis (numerik vs kategorik): bagian 3.
2. Distribusi `SalePrice` sebelum dan sesudah log, beserta Q-Q plot: bagian 4.
3. Nilai kosong struktural vs hilang sebenarnya, dan pola kosong per baris: bagian 9.
4. Box plot semua fitur dan jumlah outlier per jenis: bagian 10.
5. Validasi metode imputasi `LotFrontage`: langkah 2.4.
6. Anomali `GrLivArea` vs `SalePrice` dan harga per sqft per `OverallQual`: langkah 3.1.
7. Efek capping `LotArea`: langkah 3.2.
8. Perbandingan data mentah vs bersih (line chart dan densitas): setelah ekspor CSV.
9. Skewness sebelum dan sesudah log, serta Min-Max vs Standard: langkah 4.3 dan 4.4.
10. Pasangan berkorelasi tinggi, scree plot PCA, dan loading PC1 / PC2: langkah 5.2 dan 5.3.
11. Ukuran data di setiap tahap: ringkasan akhir.

## Keterbatasan dan hal yang bisa dikembangkan

1. `MasVnrType` dibuang karena aturan 50%, padahal kosong sebenarnya hanya 0.5% dan informasinya cukup kuat.
2. Keputusan capping `LotArea` hanya berdasarkan satu kriteria (perubahan korelasi Pearson dengan harga).
3. Membuang dummy langka sama saja dengan menggabungkan kategori langka ke kelompok dasar.
4. Imputasi KNN membuat sebaran `LotFrontage` sedikit lebih sempit dari aslinya.
5. Belum ada pemodelan, jadi pengaruh praproses ini terhadap akurasi model belum diuji.
