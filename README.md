# 🇮🇩 GA-RF Rupiah Forecasting

**Hybrid Genetic Algorithm + Random Forest untuk Prediksi Nilai Tukar USD/IDR**

Proyek ini merupakan implementasi pendekatan hybrid antara **Algoritma Genetika (GA)** dan **Random Forest (RF)** untuk memprediksi pergerakan nilai tukar Rupiah terhadap USD. GA digunakan sebagai mekanisme optimasi otomatis terhadap hyperparameter model Random Forest, menggantikan proses pencarian manual yang tidak efisien.

> Final Project — Mata Kuliah Algoritma Evolusi 2026
> Tema: *"Evolusi Cerdas untuk Ketahanan Ekonomi"*

---

## 📌 Deskripsi Program

Program membaca 8 variabel makroekonomi sebagai fitur input, kemudian menjalankan pipeline berikut:

1. Generate / load data makroekonomi (inflasi, suku bunga BI, Fed Rate, harga minyak, cadangan devisa, neraca perdagangan, IHSG, harga emas)
2. Melatih **baseline Random Forest** dengan hyperparameter default sebagai pembanding
3. Menjalankan **Algoritma Genetika** (50 generasi, populasi 30) untuk mencari kombinasi hyperparameter RF yang optimal
4. Meretrain model RF dengan hyperparameter terbaik hasil GA
5. Membandingkan performa baseline vs GA-optimal menggunakan metrik RMSE dan MAPE
6. Menghasilkan visualisasi konvergensi fitness dan hasil prediksi

---

## 📦 Library & Framework

| Library | Versi Minimum | Fungsi |
|---------|--------------|--------|
| `pygad` | ≥ 3.0.0 | Implementasi Algoritma Genetika |
| `scikit-learn` | ≥ 1.3.0 | Model Random Forest, cross-validation, metrik evaluasi |
| `numpy` | ≥ 1.24.0 | Operasi array dan komputasi numerik |
| `pandas` | ≥ 2.0.0 | Manipulasi dan preprocessing data |
| `matplotlib` | ≥ 3.7.0 | Visualisasi konvergensi dan hasil prediksi |

---

## ⚙️ Instalasi

**1. Clone repository**
```bash
git clone https://github.com/[username]/ga-rf-rupiah-forecasting.git
cd ga-rf-rupiah-forecasting
```

**2. (Opsional) Buat virtual environment**
```bash
python -m venv venv
source venv/bin/activate        # Linux/Mac
venv\Scripts\activate           # Windows
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

---

## ▶️ Cara Menjalankan

**Mode full (untuk eksperimen & laporan — 50 generasi):**
```bash
python ga_rf_rupiah_final.py
```

**Mode fast (untuk testing cepat — 10 generasi):**
```bash
python ga_rf_rupiah_final.py --fast
```

---

## 📥 Input & 📤 Output

### Input
Program saat ini menggunakan **data simulasi** yang di-generate otomatis di dalam script (`generate_macro_data()`), merepresentasikan 8 variabel makroekonomi bulanan:

| Fitur | Satuan | Sumber Data Riil |
|-------|--------|-----------------|
| Inflasi Indonesia | % YoY | BPS / FRED |
| Suku Bunga BI | % | Bank Indonesia |
| Fed Funds Rate | % | FRED |
| Harga Minyak Dunia | USD/barel | Yahoo Finance (`BZ=F`) |
| Cadangan Devisa | Miliar USD | Bank Indonesia |
| Neraca Perdagangan | Miliar USD | BPS / World Bank |
| IHSG | Ribuan poin | Yahoo Finance (`^JKSE`) |
| Harga Emas | USD/troy oz | Yahoo Finance (`GC=F`) |

**Target variabel:** Kurs USD/IDR (di sekitar Rp17.600)

### Output

| Output | Deskripsi |
|--------|-----------|
| Console log | Fitness & hyperparameter terbaik per generasi |
| Tabel perbandingan | RMSE & MAPE baseline vs GA-optimal |
| `results/ga_rf_results.png` | 4-panel visualisasi: konvergensi fitness, prediksi vs aktual, residual plot, feature importance |

### Contoh Output Console
```
[Gen 048] Fitness=0.002531 | CV-RMSE≈394.1 | n_est=105, depth=25, feat=0.723
[Gen 049] Fitness=0.002531 | CV-RMSE≈394.1 | n_est=105, depth=25, feat=0.723
[Gen 050] Fitness=0.002531 | CV-RMSE≈394.1 | n_est=105, depth=25, feat=0.723

=================================================================
  Metrik              Baseline   GA-Optimal         Δ%
  ---------------------------------------------------
  RMSE (IDR)            373.84       351.11      6.08%
  MAPE (%)              1.7712       1.6262      8.19%
=================================================================

[PLOT] Disimpan ke: results/ga_rf_results.png
```



