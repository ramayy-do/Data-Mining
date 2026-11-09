<div align="center">

# 🔬 DermaSpot
### AI-Powered Early Detection System for Skin Cancer Melanoma

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-1.x-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![Status](https://img.shields.io/badge/Status-In%20Development-yellow?style=for-the-badge)

> **Deteksi dini kanker kulit melanoma berbasis Transfer Learning MobileNetV2 dengan optimasi Class Weighting — dapat diakses siapa saja hanya lewat browser.**

</div>

---

## 📌 Tentang Proyek

**DermaSpot** adalah aplikasi website berbasis AI yang memungkinkan pengguna melakukan **skrining awal (self-screening)** terhadap lesi kulit yang mencurigakan. Pengguna cukup mengunggah foto area kulit melalui browser, dan sistem akan memberikan hasil deteksi risiko secara instan beserta rekomendasi tindak lanjut.

Proyek ini dikembangkan sebagai **Tugas Akhir (UAS)** mata kuliah **Data Mining** di Universitas Dian Nuswantoro (UDINUS) Semarang.

---

## 👤 Identitas

| | |
|---|---|
| **Nama** | Rama Adhi Saputra |
| **NIM** | A11.2024.15847 |
| **Kelas** | A11.4507 |
| **Dosen Pengampu** | Abu Salam, M.Kom |
| **Mata Kuliah** | Data Mining |
| **Universitas** | Universitas Dian Nuswantoro (UDINUS) |

---

## 🎯 Latar Belakang & Urgensi

Kanker kulit melanoma adalah salah satu kanker paling berbahaya, namun tingkat kesembuhan sangat tinggi jika terdeteksi sejak dini. Masalahnya:

- 🏥 Rasio dermatolog terhadap penduduk Indonesia masih sangat rendah
- 💸 Biaya konsultasi spesialis tidak terjangkau semua kalangan
- ❌ Banyak kasus stadium lanjut terjadi karena keterlambatan deteksi
- 📱 Mayoritas masyarakat memiliki smartphone dengan kamera yang memadai

**DermaSpot hadir sebagai solusi**: sistem skrining awal berbasis AI yang gratis, cepat, dan dapat diakses siapa saja.

---

## 🧠 Pendekatan Teknis

### Masalah Inti: Imbalanced Data
Dataset HAM10000 sangat tidak seimbang — kasus Melanoma (ganas) hanya **~11%** dari total data. Model AI yang dilatih tanpa penanganan khusus akan cenderung selalu memprediksi "jinak" karena itu adalah jawaban yang paling sering benar secara statistik.

```
Dataset HAM10000:
├── Jinak (Benign)    : ~8.900 gambar  (89%)
└── Ganas (Malignant) : ~1.100 gambar  (11%)  ← sangat sedikit!
```

### Solusi yang Diusulkan

| Komponen | Fungsi |
|---|---|
| **MobileNetV2** | Arsitektur Transfer Learning ringan (~14 MB) — cocok untuk web deployment |
| **Class Weighting** | Penalti ~8× lebih besar saat salah prediksi kelas ganas — mendorong model lebih sensitif |
| **Recall sebagai metrik utama** | Meminimalisir False Negative (orang sakit tidak terdeteksi) — target ≥ 85% |

### Rumusan Masalah
> *"Bagaimana pengaruh penerapan teknik Class Weighting pada arsitektur Transfer Learning MobileNetV2 terhadap peningkatan nilai Recall dalam klasifikasi kanker kulit melanoma pada dataset HAM10000 yang tidak seimbang?"*

---

## 🗂️ Struktur Repositori

```
dermaspot/
│
├── 📄 README.md                          ← Kamu sedang membaca ini
├── 📄 requirements.txt                   ← Semua library yang dibutuhkan
│
├── 📁 docs/
│   ├── template_ide_ml.pdf               ← Jawaban UTS Machine Learning (7 poin)
│   ├── proposal_penambangan_data.pdf     ← Jawaban UTS Penambangan Data (6 soal)
│   └── laporan_akhir.pdf                 ← [UAS] Laporan akhir proyek
│
├── 📁 data/
│   └── README.md                         ← Panduan download HAM10000
│                                            (dataset ~2.6 GB, tidak di-upload ke repo)
│
├── 📁 notebooks/
│   ├── 01_EDA.ipynb                      ← Exploratory Data Analysis
│   ├── 02_preprocessing.ipynb            ← Preprocessing & augmentasi
│   ├── 03_baseline_vgg16.ipynb           ← Training model baseline VGG-16
│   └── 04_mobilenetv2_classweight.ipynb  ← Training model usulan (MobileNetV2 + CW)
│
├── 📁 src/
│   ├── preprocessing.py                  ← Fungsi resize, normalisasi, augmentasi
│   ├── model.py                          ← Arsitektur MobileNetV2 + classifier head
│   ├── train.py                          ← Script training dengan Class Weighting
│   └── evaluate.py                       ← Script evaluasi & komparasi metrik
│
├── 📁 models/
│   └── README.md                         ← Panduan download model .h5
│                                            (file terlalu besar untuk GitHub)
│
└── 📁 app/
    ├── app.py                            ← [UAS] Main Streamlit application
    ├── utils.py                          ← Helper: preprocessing & inference
    └── assets/
        └── logo.png                      ← Logo DermaSpot
```

---

## 📊 Dataset

**HAM10000** *(Human Against Machine with 10000 training images)*

| Info | Detail |
|---|---|
| **Sumber** | [Kaggle](https://www.kaggle.com/datasets/kmader/skin-lesion-analysis-toward-melanoma-detection) / [Harvard Dataverse](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/DBW86T) |
| **Jumlah Gambar** | 10.015 foto lesi kulit berlabel |
| **Format** | JPEG |
| **Lisensi** | CC BY-NC-SA 4.0 (bebas untuk penelitian) |
| **Referensi** | Tschandl et al. (2018), *Scientific Data* |

### Label Binary (Penyederhanaan untuk DermaSpot)
```
Ganas (1): mel, akiec, bcc
Jinak (0): nv, bkl, df, vasc
```

### Split Dataset
```
Train      : 80%  (8.012 gambar) ← augmentasi diterapkan di sini
Validasi   : 10%  (1.001 gambar)
Test       : 10%  (1.002 gambar) ← tidak disentuh selama training
```

---

## ⚗️ Rancangan Eksperimen

| Metrik | Eks.1: VGG-16 | Eks.2: MobileNetV2 | Eks.3: MobileNetV2 + CW *(Usulan)* |
|---|---|---|---|
| Recall | ~65% | ~72% | **≥ 85%** 🎯 |
| Precision | ~78% | ~75% | ≥ 70% |
| F1-Score | ~71% | ~73% | ≥ 77% |
| AUC-ROC | ~0.79 | ~0.83 | ≥ 0.87 |
| Inference Time | ~2.1s | ~0.8s | ≤ 0.8s |
| Model Size | ~528 MB | ~14 MB | ~14 MB |

> *Angka Eks.1 dan Eks.2 adalah proyeksi berdasarkan literatur. Eks.3 adalah target yang akan divalidasi saat UAS.*

---

## 🗓️ Timeline Pengerjaan

```
Minggu 1-2  │ ████████░░░░░░░░  Setup, download HAM10000, preprocessing, EDA
Minggu 3-4  │ ░░░░░░░░████████  Training baseline & model usulan
Minggu 5-6  │ ░░░░░░░░░░░░████  Evaluasi, komparasi metrik, dokumentasi
Minggu 7-8  │ ░░░░░░░░░░░░░░██  Development Streamlit + deployment (UAS)
```

---

## 🚀 Cara Menjalankan (Coming Soon — UAS)

```bash
# 1. Clone repositori
git clone https://github.com/[username]/dermaspot.git
cd dermaspot

# 2. Install dependencies
pip install -r requirements.txt

# 3. Download model (lihat models/README.md)

# 4. Jalankan aplikasi
streamlit run app/app.py
```

---

## 📈 Target Luaran

- [x] Template Ide Produk ML (7 poin) — selesai
- [ ] Proposal Penelitian Penambangan Data (6 soal)
- [ ] Notebook EDA & Preprocessing
- [ ] Training & evaluasi model baseline
- [ ] Training & evaluasi model usulan (MobileNetV2 + Class Weighting)
- [ ] Website DermaSpot (Streamlit)
- [ ] Deployment ke Streamlit Cloud
- [ ] Laporan akhir

---

## 📚 Referensi

1. Esteva, A., et al. (2017). Dermatologist-level classification of skin cancer with deep neural networks. *Nature*, 542, 115–118.
2. Goyal, M., et al. (2020). Artificial intelligence-based image classification methods for diagnosis of skin cancer. *Computers in Biology and Medicine*, 127.
3. Chaturvedi, S. S., et al. (2022). A multi-class skin cancer classification using deep convolutional neural networks. *Multimedia Tools and Applications*, 79.
4. Kassem, M. A., et al. (2020). Machine learning and deep learning methods for skin lesion classification. *Diagnostics*, 11(8).
5. Tschandl, P., et al. (2018). The HAM10000 dataset. *Scientific Data*, 5, 180161.

---

## ⚠️ Disclaimer

> DermaSpot adalah alat bantu skrining awal berbasis AI untuk tujuan edukasi dan penelitian. **Bukan pengganti diagnosis medis profesional.** Selalu konsultasikan kondisi kulit Anda ke dokter spesialis kulit (dermatolog) untuk diagnosis yang akurat.

---

<div align="center">

**Create by Rama Adhi Saputra**
*Dian Nuswantoro University — 2026*

</div>
