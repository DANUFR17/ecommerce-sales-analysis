# Analisis Penjualan E-Commerce Olist

Eksplorasi data 100.000+ transaksi e-commerce Brazil (2016–2018)
menggunakan Python dan pandas.

---

## Analisis yang sudah dikerjakan

### 1. EDA penjualan
- Tren jumlah order per bulan
- Order terbanyak di hari kerja (Senin–Rabu)
- Distribusi harga produk — mayoritas di bawah R$150
- Revenue tertinggi di November 2017 (Black Friday)

![Dashboard EDA](output/dashboard.png)

---

### 2. Kepuasan pelanggan & review
- 76% pelanggan memberi rating 4 atau 5 bintang
- Keterlambatan pengiriman adalah faktor terbesar penurunan rating
- Order telat >14 hari → rata-rata rating turun dari 4.26 ke 1.78 (−58%)

![Rating vs Keterlambatan](output/06-rating-vs-delay.png)

---

### 3. Kategori produk
- Top kategori berdasarkan jumlah order: bed & bath, health & beauty
- Kategori terlaku ≠ kategori revenue tertinggi
- Komputer & elektronik: order sedikit tapi revenue besar

![Top Kategori](output/07-top10-kategori-order.png)

---

### 4. Machine Learning — Prediksi kepuasan pelanggan
- Klasifikasi biner: prediksi apakah pelanggan akan memberi rating tinggi (≥4) atau rendah (≤3)
- Feature engineering: delay_days, delivery_days, is_late, total_price, item_count
- Random Forest mencapai **AUC 0.856** dan akurasi **87%** di test set
- `delay_days` dan `is_late` adalah fitur paling dominan — mengkonfirmasi temuan EDA

![Evaluasi Model](output/ml-evaluasi-rating.png)

---

### 5. Machine Learning — Segmentasi pelanggan RFM
- Mengelompokkan 96.000+ pelanggan ke 4 segmen menggunakan K-Means clustering
- Dimensi RFM: Recency (kapan terakhir beli), Frequency (seberapa sering), Monetary (total belanja)
- Jumlah cluster optimal K=4 ditentukan dengan Elbow method dan Silhouette score
- Segmen: **Champions** (12K) · **Loyal** (29K) · **At Risk** (24K) · **Hibernating** (31K)

![Segmentasi RFM](output/12-rfm-segmentasi.png)

---

## Tech stack
- Python 3.x · pandas · matplotlib · seaborn · scikit-learn

## Cara menjalankan
1. Download dataset dari [Kaggle Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
2. Taruh semua file CSV di folder `data/`
3. Jalankan notebook sesuai urutan di folder `notebooks/`

## Struktur folder
```
project-ecommerce/
├── notebooks/
│   ├── 00-ringkasan-olist.ipynb
│   ├── 01-eda-penjualan.ipynb
│   ├── 02-analisis-review.ipynb
│   ├── 03-analisis-produk.ipynb
│   ├── 04-ml-prediksi-rating.ipynb
│   └── 05-rfm-clustering.ipynb
├── output/          # semua grafik hasil analisis
└── README.md
```