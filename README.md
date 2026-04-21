# 🧠 DepreScan — Sistem Deteksi Risiko Depresi Berdasarkan Gaya Hidup

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

## 📁 Struktur Repositori

```
📦 deprescan/
│
├── 📂 src/                         # Pipeline data science (Data Scientist)
│   ├── config/
│   │   └── settings.py             # Konfigurasi path, kolom, dan parameter global
│   ├── preproc/
│   │   ├── gather.py               # Unduh & load file NHANES (.xpt)
│   │   ├── merge.py                # Gabungkan modul DEMO, DPQ, ALQ, PAQ, SLQ
│   │   ├── assess.py               # Audit missing value & distribusi awal
│   │   └── clean.py                # Imputasi, filter outlier, encoding
│   ├── features/
│   │   ├── demographics.py         # Fitur usia, gender, ras, pendidikan, marital
│   │   ├── activity.py             # Kategori aktivitas fisik & MET menit
│   │   ├── alcohol.py              # Skor risiko alkohol, binge/heavy drinker
│   │   ├── sleep.py                # Jam tidur, gangguan tidur, sleep apnea risk
│   │   ├── target.py               # Kalkulasi PHQ9_SCORE, severity, binary label
│   │   ├── feature_engineering.py  # Fitur turunan & skor komposit (TOTAL_RISK_COMPOSITE)
│   │   └── eda.py                  # Fungsi-fungsi analisis eksploratif
│   ├── experiments/
│   │   └── ab_testing.py           # Pengujian eksperimen & perbandingan fitur
│   ├── pipeline/
│   │   └── run.py                  # Entry point pipeline end-to-end
│   └── utils/
│       ├── io.py                   # Helper baca/tulis file
│       └── sentinel.py             # Penanganan nilai sentinel NHANES
│
├── 📂 data-science/                # Analisis & Dashboard (Data Scientist)
│   ├── dashboard_nhanes_Final.py   # Dashboard Streamlit (DepreScan)
│   ├── Final_Data.csv              # Dataset hasil pipeline (5.088 baris, 78 kolom)
│   └── notebooks/                  # Notebook EDA & pelatihan model
│
└── README.md
```

---

## 🚀 Cara Menjalankan (Lokal)

**Prasyarat:** Node.js ≥ 18 · Python ≥ 3.10

### 1. Pipeline Data Science
```bash
# Jalankan pipeline preprocessing & feature engineering
cd src
pip install -r requirements.txt
python pipeline/run.py
# Output: data-science/Final_Data.csv
```

### 2. Dashboard Analisis (Streamlit)
```bash
cd data-science
pip install streamlit plotly pandas numpy
streamlit run dashboard_nhanes_Final.py
# Pastikan Final_Data.csv ada di direktori yang sama
```

### 3. Model Server (FastAPI)
```bash
cd ai-model
pip install -r requirements.txt
uvicorn app:app --reload --port 8000
```

### 4. Backend (Node.js)
```bash
cd backend && npm install && npm run dev
```

### 5. Frontend (React)
```bash
cd frontend && npm install && npm run dev
```

---

## 🌐 Deployment

| Komponen | Platform | Status |
|----------|----------|--------|
| Frontend (React) | Netlify | ✅ Live |
| Backend (Node.js) | Render | ✅ Live |
| Model Server (FastAPI) | Hugging Face Spaces | ✅ Live |
| Dashboard (Streamlit) | Streamlit Community Cloud | ✅ Live |

> Render free tier sleep otomatis setelah 15 menit idle. Cold start pertama sekitar 30–50 detik.

---

## 📦 Tech Stack

| Layer | Teknologi |
|-------|-----------|
| Frontend | React.js, Vite, Tailwind CSS, Axios |
| Backend | Node.js, Express.js |
| AI / Model | TensorFlow, FastAPI, Python |
| Data & Dashboard | Streamlit, Plotly, Pandas, NumPy |
| Version Control | GitHub |

---

## 📂 Dataset

**NHANES 2017–2018** — dipilih sebagai siklus terakhir dengan format PHQ-9 lengkap sebelum perubahan metodologi survei. Modul yang digunakan: `DEMO_J.xpt`, `DPQ_J.xpt`, `ALQ_J.xpt`, `PAQ_J.xpt`, `SLQ_J.xpt`.

Hasil preprocessing menghasilkan `Final_Data.csv` dengan **5.088 responden** dan **78 variabel**.

---

## ⚠️ Keterbatasan

- Dataset berbasis populasi **Amerika Serikat (2017–2018)**, belum divalidasi untuk populasi Indonesia
- Model berpotensi bias terhadap kelas mayoritas (Minimal 74.4%)
- Seluruh input berbasis **self-report** yang rentan response bias

---

## 🆘 Bantuan Kesehatan Mental

- 📞 **Hotline Kemenkes RI:** 119 ext. 8
- 📞 **Into The Light Indonesia:** 021-7884-5555
- 🌐 **Yayasan Pulih:** www.yayasanpulih.org

---

<div align="center">

Dibuat dengan ❤️ oleh Tim CC26-PSU066 · **Coding Camp 2026 powered by DBS Foundation**

</div>
