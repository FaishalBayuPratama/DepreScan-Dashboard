# 🧠 DepreScan — Sistem Deteksi Risiko Depresi Berdasarkan Gaya Hidup

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)

**Coding Camp 2026 powered by DBS Foundation**
`CC26-PSU066` · Tema: Healthy Lives & Well-being

[🌐 Live App](#) · [📊 Dashboard Analisis](#) · [📄 Dokumentasi](#)

</div>

---

## 📖 Tentang Proyek

**DepreScan** adalah platform web interaktif untuk deteksi dini risiko depresi secara mandiri menggunakan standar klinis **Patient Health Questionnaire (PHQ-9)**. Sistem ini hadir sebagai solusi atas tiga hambatan utama akses kesehatan mental di Indonesia: stigma sosial, biaya konsultasi yang tinggi, dan keterbatasan tenaga profesional.

Dengan mengintegrasikan kuesioner PHQ-9 dan data gaya hidup ke dalam model **Deep Learning** yang dilatih menggunakan data survei **NHANES 2017-2018**, DepreScan mampu memberikan interpretasi skor depresi (0–27) beserta klasifikasi tingkat keparahannya secara cepat, privat, dan objektif.

> ⚠️ **Disclaimer:** Hasil DepreScan adalah indikasi awal, **bukan diagnosis klinis**. Selalu konsultasikan kondisi Anda kepada tenaga profesional kesehatan mental. Jika kamu membutuhkan bantuan segera, hubungi **119 ext. 8** (Kemenkes RI) atau **Into The Light Indonesia: 021-7884-5555**.

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

## ✨ Fitur Utama

- 📋 **Kuesioner PHQ-9 Interaktif** — Form skrining mandiri dengan validasi input dan skip-logic
- 🤖 **Prediksi Deep Learning** — Model TensorFlow dengan akurasi ≥ 85% dan MAE ≤ 0.02
- 📊 **Dashboard Analisis Data** — Eksplorasi pola kesehatan mental dari dataset NHANES secara visual dan interaktif
- 🔒 **Privasi Terjaga** — Tidak memerlukan registrasi, nama bersifat opsional, data tidak disimpan permanen
- 📱 **Responsive Web** — Antarmuka React.js yang dapat diakses dari perangkat apapun
- 💡 **Insight Otomatis** — Setiap visualisasi dilengkapi interpretasi kontekstual

---

## 🏗️ Arsitektur Sistem

```
┌─────────────────────────────────────────────────────────────┐
│                        Pengguna                             │
└─────────────────────┬───────────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────────┐
│              Frontend (React.js + Vite)                      │
│          Form PHQ-9 · Hasil Prediksi · Visualisasi          │
│                   Deploy: Netlify                            │
└─────────────────────┬───────────────────────────────────────┘
                      │ Axios HTTP Request
┌─────────────────────▼───────────────────────────────────────┐
│              Backend API (Node.js + Express)                 │
│            RESTful API · Data Routing · Auth                 │
│                    Deploy: Render                            │
└─────────────────────┬───────────────────────────────────────┘
                      │ Internal API Call
┌─────────────────────▼───────────────────────────────────────┐
│             Model Server (FastAPI + TensorFlow)              │
│          Inference · Preprocessing · Klasifikasi            │
│               Deploy: Hugging Face Spaces                    │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│           Dashboard Analisis (Streamlit)                     │
│     EDA · Demografi · Gaya Hidup · Korelasi Fitur           │
│              Deploy: Streamlit Community Cloud               │
└─────────────────────────────────────────────────────────────┘
```

---

## 📊 Dashboard Analisis Data (MindScope)

Dashboard interaktif berbasis **Streamlit** untuk mengeksplorasi pola kesehatan mental dari dataset NHANES. Dibangun oleh tim Data Scientist sebagai media visualisasi hasil analisis.

### Halaman Dashboard

**📋 Ringkasan Utama**
- Metrik kunci: total responden, rata-rata usia, rata-rata skor PHQ-9, proporsi depresi
- Distribusi tingkat depresi dan perbandingan gender
- Heatmap Top 10 fitur paling berpengaruh terhadap PHQ-9

**👥 Analisis Demografi**
- Pola depresi berdasarkan jenis kelamin, pendidikan, kelompok usia
- Analisis ras/etnis, status pernikahan, dan dampak tinggal sendirian

**🧠 Analisis Depresi**
- Distribusi skor PHQ-9 dan piramida kategori depresi
- Analisis item parah (N_SEVERE_ITEMS) dan DPQ100
- Korelasi berbagai faktor gaya hidup dengan skor depresi

**🏃 Gaya Hidup & Risiko**
- Hubungan alkohol, aktivitas fisik, dan kualitas tidur dengan depresi
- Analisis skor risiko komposit (TOTAL_RISK_COMPOSITE)
- Gangguan tidur dan sleep apnea per tingkat depresi

### Menjalankan Dashboard

```bash
# Install dependencies
pip install streamlit plotly pandas numpy

# Jalankan dashboard
streamlit run dashboard_nhanes_Final.py
```

> Pastikan `Final_Data.csv` berada di direktori yang sama.

---

## 🤖 Model Deep Learning

Model dibangun menggunakan **TensorFlow Functional API** dengan karakteristik:

- **Input:** Fitur gaya hidup, tidur, aktivitas fisik, dan variabel demografis dari NHANES
- **Target:** Skor PHQ-9 (0–27) dan klasifikasi tingkat depresi (5 kelas)
- **Threshold Performa:** Akurasi ≥ 85%, MAE ≤ 0.02
- **Format Export:** `.keras` / `SavedModel` (siap produksi)
- **Monitoring:** TensorBoard (loss, accuracy, MAE per epoch)

### Komponen Kustom yang Diimplementasikan
- Custom Layer / Custom Loss Function (mempertimbangkan class imbalance PHQ-9)
- Custom Callback untuk monitoring real-time
- SMOTE & class_weight untuk menangani distribusi kelas yang tidak seimbang (74.4% Minimal, 0.8% Severe)

---

## 📁 Struktur Repositori

```
📦 deprescan/
├── 📂 frontend/                  # React.js + Vite
│   ├── src/
│   │   ├── components/           # Komponen reusable
│   │   ├── pages/                # Halaman kuesioner & hasil
│   │   └── services/             # Axios API calls
│   └── package.json
│
├── 📂 backend/                   # Node.js + Express
│   ├── routes/                   # Endpoint API
│   ├── controllers/
│   └── server.js
│
├── 📂 ai-model/                  # FastAPI + TensorFlow
│   ├── app.py                    # FastAPI server
│   ├── model/                    # File model .keras / SavedModel
│   ├── preprocessing.py          # Pipeline preprocessing inference
│   └── testdata.py               # Validasi fitur
│
├── 📂 data-science/              # Analisis & Dashboard
│   ├── dashboard_nhanes_Final.py # Dashboard Streamlit
│   ├── Final_Data.csv            # Dataset hasil preprocessing
│   ├── notebooks/                # Notebook EDA & modeling
│   └── tensorboard_logs/         # Log pelatihan model
│
└── README.md
```

---

## 🚀 Cara Menjalankan (Lokal)

### Prasyarat
- Node.js ≥ 18
- Python ≥ 3.10
- pip / conda

### 1. Clone Repository
```bash
git clone https://github.com/username/deprescan.git
cd deprescan
```

### 2. Jalankan Model Server (FastAPI)
```bash
cd ai-model
pip install -r requirements.txt
uvicorn app:app --reload --port 8000
```

### 3. Jalankan Backend (Node.js)
```bash
cd backend
npm install
npm run dev
```

### 4. Jalankan Frontend (React)
```bash
cd frontend
npm install
npm run dev
```

### 5. Jalankan Dashboard (Streamlit)
```bash
cd data-science
pip install streamlit plotly pandas numpy
streamlit run dashboard_nhanes_Final.py
```

---

## 🌐 Deployment

| Komponen | Platform | Status |
|----------|----------|--------|
| Frontend (React) | Netlify | ✅ Live |
| Backend (Node.js) | Render | ✅ Live |
| Model Server (FastAPI) | Hugging Face Spaces | ✅ Live |
| Dashboard (Streamlit) | Streamlit Community Cloud | ✅ Live |

> **Catatan:** Render free tier sleep otomatis setelah 15 menit tidak ada request. Cold start pertama sekitar 30–50 detik.

---

## 📦 Tech Stack

| Layer | Teknologi |
|-------|-----------|
| Frontend | React.js, Vite, Tailwind CSS, Axios |
| Backend | Node.js, Express.js |
| AI / Model | TensorFlow, FastAPI, Python |
| Data & Dashboard | Streamlit, Plotly, Pandas, NumPy |
| Desain | Figma |
| Version Control | GitHub |

---

## 📂 Dataset

Dataset yang digunakan adalah **NHANES 2017–2018** — siklus terakhir dengan format PHQ-9 lengkap (DPQ010–DPQ090) sebelum perubahan metodologi survei berikutnya.

| Siklus | PHQ-9 Lengkap | N Sampel | Catatan |
|--------|---------------|----------|---------|
| 2013–2014 | ✅ Ya | 10.175 | Tersedia |
| 2015–2016 | ✅ Ya | 9.971 | Tersedia |
| **2017–2018** | ✅ **Ya** | **9.254** | **Terpilih, Pre-COVID** |
| 2019–2020 | ⚠️ Terbatas | ~4.000 | Terdisrupsi COVID |
| 2021–2023 | ❌ Berbeda | N/A | Metodologi Berubah |

### Modul Dataset yang Digunakan
- `DEMO_J.xpt` — Data demografis (usia, jenis kelamin, ras, pendidikan)
- `DPQ_J.xpt` — Depression Screener (PHQ-9, DPQ010–DPQ090)
- `ALQ_J.xpt` — Alcohol Use Questionnaire
- `PAQ_J.xpt` — Physical Activity Questionnaire
- `SLQ_J.xpt` — Sleep Disorders Questionnaire

### Variabel Utama `Final_Data.csv` (5.088 responden, 78 variabel)

| Kategori | Kolom Utama |
|----------|-------------|
| Target | `PHQ9_SCORE`, `PHQ9_SEVERITY`, `PHQ9_BINARY` |
| Demografi | `AGE`, `GENDER`, `RACE`, `EDUCATION`, `MARITAL` |
| Aktivitas Fisik | `PA_CATEGORY`, `VIG_MIN_WEEK`, `TOTAL_MET_MIN` |
| Tidur | `AVG_SLEEP_HOURS`, `SLEEP_RISK_SCORE`, `SLEEP_DISORDERED` |
| Alkohol | `ALCOHOL_RISK_SCORE`, `BINGE_DRINKER`, `HEAVY_DRINKER` |
| Risiko | `TOTAL_RISK_COMPOSITE`, `N_SEVERE_ITEMS` |

---

## 📅 Jadwal Pengerjaan

| Minggu | Aktivitas | Divisi |
|--------|-----------|--------|
| 1–2 | Preprocessing & EDA dataset NHANES | Data Scientist |
| 2–3 | Pengembangan & pelatihan model Deep Learning | AI Engineer |
| 3–4 | Pengembangan backend API & frontend web | Fullstack Web Dev |
| 4–5 | Pengujian, feedback, finalisasi & dokumentasi | Semua |

---

## ⚠️ Keterbatasan & Disclaimer

- Dataset berbasis populasi **Amerika Serikat (2017–2018)**, belum divalidasi untuk populasi Indonesia
- Hasil prediksi adalah **indikasi awal**, bukan pengganti diagnosis klinis profesional
- Model berpotensi mengalami bias terhadap kelas mayoritas (Minimal 74.4%) — kasus berat perlu diinterpretasikan dengan hati-hati
- Seluruh input berbasis **self-report** yang rentan terhadap response bias

---

## 🆘 Bantuan Kesehatan Mental

Jika kamu atau orang di sekitarmu membutuhkan bantuan segera:

- 📞 **Hotline Kemenkes RI:** 119 ext. 8
- 📞 **Into The Light Indonesia:** 021-7884-5555
- 🌐 **Yayasan Pulih:** www.yayasanpulih.org

---

## 📄 Referensi

- Kroenke, K., et al. *The PHQ-9: Validity of a Brief Depression Severity Measure.* Journal of General Internal Medicine, 2001.
- CDC NHANES. *2017–2018 National Health and Nutrition Examination Survey.* cdc.gov/nchs/nhanes
- Manea, L., et al. *The validity and reliability of the PHQ-9 on screening of depression in neurology: a cross sectional study.*

---

## 📄 Lisensi

Distributed under the MIT License. See `LICENSE` for more information.

---

<div align="center">

Dibuat dengan ❤️ oleh Tim CC26-PSU066
**Coding Camp 2026 powered by DBS Foundation**

*DepreScan bukan pengganti diagnosis klinis. Jika kamu membutuhkan bantuan, jangan ragu untuk menghubungi profesional.*

</div>
