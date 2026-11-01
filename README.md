# Regresi Linear Biaya Asuransi Kesehatan

Tugas Pengantar Sains Data, Universitas Matana (Tema: Data Kesehatan).

**Dosen:** Amanatullah Pandu Zenklinov, S.Stat., M.Stat.

**Kelompok:** Satria Ramadhani, Immanuel Machello Sutanto, Joe Alexander

## Ringkasan
Membandingkan regresi linear sederhana (SLR) dan regresi linear berganda (MLR) untuk memprediksi biaya asuransi tahunan (`charges`) pada 1338 pelanggan.

| Model (data test, 268 baris) | MAE (USD) | RMSE (USD) | R² |
|---|---|---|---|
| SLR: `age` | 9.173,26 | 11.661,22 | 0,1241 |
| MLR: 6 prediktor | 4.181,19 | 5.796,28 | 0,7836 |

Temuan utama: usia saja lemah menjelaskan biaya, sedangkan status merokok (`smoker_yes`) memiliki koefisien terbesar (sekitar +23.651 USD dengan prediktor lain tetap). Koefisien menunjukkan asosiasi, bukan sebab-akibat.

## Struktur Repo
```
.
├── README.md
├── requirements.txt
├── data/
│   └── insurance.csv
├── notebook/
│   └── Tugas_Regresi_Linear_Asuransi.ipynb
└── presentation/
    └── Regresi_Linear_Biaya_Asuransi_Kesehatan.pptx
```

## Dataset
- **Nama:** Medical Cost Personal Datasets
- **Sumber:** Kaggle, https://www.kaggle.com/datasets/mirichoi0218/insurance (berasal dari buku *Machine Learning with R* karya Brett Lantz)
- **Ukuran:** 1338 baris, 7 kolom, tanpa missing values

| Kolom | Tipe | Keterangan |
|---|---|---|
| `age` | Numerik | Usia (tahun) |
| `sex` | Kategori | male / female |
| `bmi` | Numerik | Body Mass Index (kg/m²) |
| `children` | Numerik | Jumlah tanggungan anak |
| `smoker` | Kategori | yes / no |
| `region` | Kategori | northeast, northwest, southeast, southwest |
| `charges` | Numerik | Biaya asuransi tahunan (USD), target Y |

## Metode
- Split 80:20, `random_state=42` (1070 train, 268 test), sama untuk SLR dan MLR.
- SLR: `charges ~ age` dengan `LinearRegression`.
- MLR: enam prediktor, `OneHotEncoder(drop="first")` dalam `Pipeline`. Kategori referensi: `smoker=no`, `sex=female`, `region=northeast`.
- Evaluasi: MAE, RMSE, R², plot residual, Q-Q plot, dan pemeriksaan outlier.

## Cara Menjalankan
1. Buka `notebook/Tugas_Regresi_Linear_Asuransi.ipynb` di Google Colab (File > Upload notebook).
2. Pilih Runtime > Run all.
3. Lokal: `pip install -r requirements.txt`, lalu jalankan notebook dengan Jupyter.

Notebook memuat data lewat `kagglehub`. Salinan data tersedia di `data/insurance.csv`.
