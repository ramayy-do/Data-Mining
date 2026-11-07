# 🤖 Models

File model `.h5` tidak disimpan di repositori ini karena ukurannya besar.

## Model yang Akan Tersedia (setelah UAS)

| File | Deskripsi | Ukuran |
|---|---|---|
| `baseline_vgg16.h5` | Model baseline VGG-16 tanpa Class Weighting | ~528 MB |
| `baseline_mobilenetv2.h5` | MobileNetV2 tanpa Class Weighting | ~14 MB |
| `dermaspot_model.h5` | **Model final** MobileNetV2 + Class Weighting | ~14 MB |

## Cara Download Model Final
> Link Google Drive akan ditambahkan setelah training selesai.

## Cara Load Model
```python
import tensorflow as tf

model = tf.keras.models.load_model('models/dermaspot_model.h5')
```
