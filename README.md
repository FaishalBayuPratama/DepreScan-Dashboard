# 🧠 DepreScan - Dashboard Analisis Kesehatan Mental NHANES

**Coding Camp 2026 powered by DBS Foundation** · `CC26-PSU066` · Tema: Healthy Lives & Well-being

> ⚠️ **Disclaimer:** Hasil DepreScan adalah indikasi awal, **bukan diagnosis klinis**. Jika kamu membutuhkan bantuan segera, hubungi **119 ext. 8** (Kemenkes RI) atau **Into The Light Indonesia: 021-7884-5555**.

---

## 👥 Tim Pengembang

| ID | Nama | Peran |
|----|------|-------|
| CFCC284D6Y0191 | M. Syafi'ul Masruri | Fullstack Web Developer |
| CFCC284D6X0778 | Nani Fitria Ramadhani | Fullstack Web Developer |
| CDCC284D6Y1269 | Bagus Febriansyah Pratama | Data Scientist |
| CDCC284D6Y1932 | Faishal Bayu Pratama | Data Scientist |
| CACC284D6X1992 | Hannia Hary Putri | AI Engineer |
| CACC284D6Y2611 | Muhammad Wildan Arif Maulana | AI Engineer |

---

## 📁 Struktur Proyek

```
📦 deprescan-data-science/
│
├── 📂 src/                              # Pipeline preprocessing & feature engineering
│   ├── config/
│   │   └── settings.py                  # Path, nama kolom, dan parameter global
│   │
│   ├── preproc/                         # Tahap 1 - Persiapan data mentah NHANES
│   │   ├── gather.py                    # Load file .xpt dari CDC NHANES
│   │   ├── merge.py                     # Gabungkan modul DEMO, DPQ, ALQ, PAQ, SLQ
│   │   ├── assess.py                    # Audit missing value & distribusi awal
│   │   └── clean.py                     # Imputasi, filter outlier, encoding
│   │
│   ├── features/                        # Tahap 2 - Feature engineering
│   │   ├── demographics.py              # Usia, gender, ras, pendidikan, status menikah
│   │   ├── activity.py                  # Kategori aktivitas fisik & total MET menit
│   │   ├── alcohol.py                   # Skor risiko alkohol, binge/heavy drinker
│   │   ├── sleep.py                     # Jam tidur, gangguan tidur, sleep apnea risk
│   │   ├── target.py                    # PHQ9_SCORE, PHQ9_SEVERITY, PHQ9_BINARY
│   │   ├── feature_engineering.py       # Fitur turunan & TOTAL_RISK_COMPOSITE
│   │   └── eda.py                       # Fungsi analisis eksploratif (korelasi, distribusi)
│   │
│   ├── experiments/
│   │   └── ab_testing.py                # Pengujian & perbandingan konfigurasi fitur
│   │
│   ├── pipeline/
│   │   └── run.py                       # Entry point - jalankan pipeline end-to-end
│   │
│   └── utils/
│       ├── io.py                        # Helper baca/tulis file CSV & XPT
│       └── sentinel.py                  # Penanganan nilai sentinel khas NHANES
│
├── dashboard_nhanes_Final.py            # Dashboard Streamlit (DepreScan)
├── Final_Data.csv                       # Output pipeline: 5.088 baris, 78 kolom
└── README.md
```

---

## ⚙️ Cara Menjalankan

**Prasyarat:** Python ≥ 3.10

### 1. Install dependensi

```bash
pip install streamlit plotly pandas numpy
```

### 2. Jalankan pipeline (opsional - jika ingin generate ulang `Final_Data.csv`)

```bash
python src/pipeline/run.py
```

### 3. Jalankan dashboard

```bash
streamlit run dashboard_nhanes_Final.py
```

> Pastikan `Final_Data.csv` berada di direktori yang sama dengan `dashboard_nhanes_Final.py`.

---

## 📂 Dataset

**NHANES 2017–2018** dipilih sebagai siklus terakhir dengan format PHQ-9 lengkap sebelum perubahan metodologi survei CDC.

| Modul | File | Isi |
|-------|------|-----|
| Demografi | `DEMO_J.xpt` | Usia, gender, ras, pendidikan, status menikah |
| Depresi | `DPQ_J.xpt` | Kuesioner PHQ-9 (DPQ010–DPQ090) |
| Alkohol | `ALQ_J.xpt` | Frekuensi & jumlah konsumsi alkohol |
| Aktivitas Fisik | `PAQ_J.xpt` | Jenis, durasi, dan intensitas aktivitas |
| Tidur | `SLQ_J.xpt` | Durasi tidur, gangguan tidur, sleep apnea |

Hasil preprocessing: **5.088 responden · 78 variabel** tersimpan di `Final_Data.csv`.

---

## 📊 Dashboard - DepreScan

Dashboard interaktif berbasis Streamlit untuk mengeksplorasi pola kesehatan mental dari dataset NHANES. Terdiri dari 5 halaman:

| Halaman | Isi |
|---------|-----|
| 📊 Ringkasan Utama | Metrik kunci, distribusi depresi, heatmap top-10 fitur |
| 👥 Demografi | Pola depresi per gender, usia, pendidikan, ras, status menikah |
| 🧠 Analisis Depresi | Distribusi PHQ-9, item parah, korelasi fitur |
| 🏃 Gaya Hidup & Risiko | Alkohol, aktivitas fisik, tidur, indeks risiko komposit |
| 💼 Pertanyaan Bisnis | Jawaban 4 pertanyaan bisnis berbasis visualisasi data |

---

## ⚠️ Keterbatasan

- Dataset berbasis populasi **Amerika Serikat (2017–2018)**, belum divalidasi untuk populasi Indonesia
- Distribusi kelas tidak seimbang: Minimal 74.4%, Severe hanya 0.8%
- Seluruh data bersifat **self-report** - rentan terhadap response bias

---

<div align="center">

Dibuat dengan ❤️ oleh Tim CC26-PSU066 · **Coding Camp 2026 powered by DBS Foundation**

</div>
