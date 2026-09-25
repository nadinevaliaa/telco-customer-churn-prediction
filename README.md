# Telco Customer Churn Prediction
## Gambaran Umum

Project ini mengembangkan model machine learning untuk memprediksi kemungkinan pelanggan berhenti menggunakan layanan berdasarkan informasi demografi, layanan, kontrak, dan akun pelanggan.

Analisis mencakup eksplorasi data, feature engineering, pengembangan model klasifikasi, hyperparameter tuning, evaluasi model, serta segmentasi pelanggan berdasarkan tingkat risiko churn.

## Tujuan

Proyek ini bertujuan untuk:

- Memprediksi kemungkinan pelanggan melakukan churn.
- Membandingkan beberapa model klasifikasi berdasarkan berbagai metrik evaluasi.
- Mengoptimalkan model menggunakan hyperparameter tuning.
- Mengelompokkan pelanggan berdasarkan probabilitas churn.
- Mengidentifikasi karakteristik pelanggan dengan risiko churn yang tinggi.

## Dataset

- **Sumber:** Telco Customer Churn Dataset from IBM Sample Data Sets on Kaggle
- **Jumlah Data:** 7,043 pelanggan
- **Jenis Data:** Data pelanggan layanan telekomunikasi

Dataset berisi informasi mengenai karakteristik pelanggan, layanan yang digunakan, informasi akun, jenis kontrak, serta informasi pembayaran dan tagihan.

## Alur Analisis

```text
Raw Data
   ↓
Data Preparation
   ↓
  EDA
   ↓
Feature Engineering
   ↓
Classification
   ↓
Hyperparameter Tuning
   ↓
Model Evaluation
   ↓
Risk Segmentation
```

## Feature Engineering

Beberapa fitur tambahan dibuat untuk mendukung proses pemodelan:

- `TenureGroup` untuk mengelompokkan pelanggan berdasarkan lama berlangganan.
- `ServiceCount` untuk merepresentasikan jumlah layanan yang digunakan pelanggan.
- `ChargeGroup` untuk mengelompokkan pelanggan berdasarkan biaya bulanan.

Fitur kategorikal kemudian dikonversi menggunakan teknik encoding yang sesuai sebelum digunakan dalam proses pemodelan.

## Pengembangan Model

Tiga algoritma klasifikasi digunakan untuk membandingkan performa model:

- Logistic Regression
- Random Forest
- XGBoost

Data dibagi menjadi data training dan testing dengan proporsi **80:20** menggunakan stratified split.

Evaluasi model dilakukan menggunakan beberapa metrik:

- Accuracy
- Precision
- Recall
- F1 Score
- ROC-AUC

## Perbandingan Model

| Model | Accuracy | Precision | Recall | F1 Score | ROC-AUC |
|---|---:|---:|---:|---:|---:|
| Logistic Regression | 73.88% | 50.52% | 78.34% | 61.43% | 84.18% |
| Random Forest | 78.99% | 63.54% | 48.93% | 55.29% | 82.44% |
| XGBoost | 79.77% | 65.08% | 51.34% | 57.40% | 84.16% |
| **Tuned XGBoost** | **80.20%** | **66.44%** | 51.34% | 57.92% | **84.72%** |

## Hyperparameter Tuning

Model XGBoost kemudian dioptimalkan menggunakan **GridSearchCV** untuk memperoleh konfigurasi hyperparameter yang lebih sesuai.

Model Tuned XGBoost menghasilkan:

- **Accuracy:** 80.20%
- **Precision:** 66.44%
- **Recall:** 51.34%
- **F1 Score:** 57.92%
- **ROC-AUC:** 84.72%

Model Tuned XGBoost kemudian digunakan sebagai model akhir untuk menghasilkan probabilitas churn dan melakukan segmentasi risiko pelanggan.

## Segmentasi Risiko Churn

Pelanggan dikelompokkan berdasarkan probabilitas churn yang dihasilkan oleh model:

| Segmen Risiko | Rentang Probabilitas |
|---|---:|
| Low Risk | < 30% |
| Medium Risk | 30–60% |
| High Risk | ≥ 60% |

### Hasil Segmentasi

| Segmen Risiko | Jumlah Pelanggan | Actual Churn Rate | Rata-rata Probabilitas Churn |
|---|---:|---:|---:|
| Low Risk | 4.325 | 7.39% | 9.81% |
| Medium Risk | 1.797 | 44.52% | 43.76% |
| High Risk | 921 | 75.03% | 72.01% |

Tingkat churn aktual meningkat dari **7.39% pada pelanggan Low Risk menjadi 75.03% pada pelanggan High Risk** menjelaskan adanya hubungan yang jelas antara tingkat risiko yang diprediksi model dengan churn aktual.

## Analisis Pelanggan High Risk

Segmen High Risk terdiri dari **921 pelanggan**, dengan rata-rata probabilitas churn sebesar **72.01%**.

Sebanyak **920 dari 921 pelanggan High Risk** memiliki kontrak **Month-to-Month**, dengan actual churn rate sebesar **75.0%**.

pelanggan dengan kontrak Month-to-Month merupakan kelompok yang sangat dominan dalam segmen High Risk dan dapat menjadi perhatian dalam analisis customer churn.

## Business Insights

Beberapa insight yang diperoleh dari analisis:

1. Pelanggan dalam segmen High Risk memiliki tingkat churn aktual yang jauh lebih tinggi dibandingkan pelanggan Low Risk dan Medium Risk.
2. Pelanggan dengan kontrak Month-to-Month mendominasi segmen High Risk.
3. Segmentasi risiko menunjukkan hubungan yang jelas antara probabilitas churn yang diprediksi dengan churn aktual pelanggan.

Insight dapat digunakan sebagai dasar untuk analisis lebih lanjut terkait churn dan identifikasi pelanggan yang membutuhkan perhatian lebih. 

## Tech Stack

- Python
- Pandas
- NumPy
- Scikit-learn
- XGBoost
- Matplotlib
- Seaborn
- Jupyter Notebook
