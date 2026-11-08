# 📦 Dataset — HAM10000

Dataset **tidak disimpan di repositori ini** karena ukurannya ~2.6 GB.

## Cara Download

### Opsi 1: Kaggle (Recommended)
1. Buat akun di [kaggle.com](https://kaggle.com) (gratis)
2. Download Kaggle API key: Account → API → Create New Token → `kaggle.json`
3. Letakkan `kaggle.json` di `~/.kaggle/`
4. Jalankan:
```bash
kaggle datasets download -d kmader/skin-lesion-analysis-toward-melanoma-detection
unzip skin-lesion-analysis-toward-melanoma-detection.zip -d ./raw/
```

### Opsi 2: Harvard Dataverse
- Link: https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/DBW86T

## Struktur Folder Setelah Download
```
data/
├── raw/
│   ├── HAM10000_images_part_1/   ← ~5.000 gambar JPEG
│   ├── HAM10000_images_part_2/   ← ~5.000 gambar JPEG
│   └── HAM10000_metadata.csv     ← Label & metadata
└── processed/                    ← Diisi otomatis setelah preprocessing
```

## Lisensi
CC BY-NC-SA 4.0 — bebas untuk penelitian akademik non-komersial.

**Referensi:** Tschandl, P., Rosendahl, C., & Kittler, H. (2018). The HAM10000 dataset, a large collection of multi-source dermatoscopic images of common pigmented skin lesions. *Scientific Data*, 5, 180161.
