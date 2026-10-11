# CNN-Pet-Classification
# Advanced CNNs and Transfer Learning: Oxford-IIIT Pet Classification

 Laporan dan repositori kode untuk tugas eksperimen **Advanced CNNs and Transfer Learning**. Eksperimen ini mengevaluasi berbagai strategi *Transfer Learning* dan arsitektur CNN pada dataset **Oxford-IIIT Pet (10 Kelas)**.

---

## 📌 Ringkasan Eksperimen

Eksperimen dilakukan dengan pembagian dataset 70:15:15 (*Stratified Split*) dan menggunakan `SEED=42` untuk menjamin reproduksibilitas.

| Exp Code | Strategy | Learning Rate | Trainable Params | Converged Epoch | Time (s) | Val Acc | Test Acc | Test Macro F1 |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **B1_Scratch** | Baseline from Scratch | `1e-3` | 11,181,642 | 20 | 120.43 | 0.8291 | 0.7797 | 0.7837 |
| **B2_FeatureExtract** | Feature Extraction | `fc: 1e-3` | 5,130 | 8 | 42.82 | 0.9829 | 0.9068 | 0.9054 |
| **B3_ProgressiveFT** | Progressive Fine-Tuning | `layer4: 1e-4, fc: 1e-3` | 8,398,858 | 5 | 30.92 | 1.0000 | 0.9407 | 0.9419 |
| **B4_NoAug** | Control (No Augmentation) | `fc: 1e-3` | 5,130 | 11 | 46.04 | 1.0000 | 0.9492 | 0.9497 |
| **B5_EfficientNetB0** | Architecture Comparison | `features.7: 1e-4, classifier: 1e-3` | 730,042 | 7 | 38.79 | 0.9829 | 0.9492 | **0.9501** |

---

## 📈 Grafik Komparatif Loss

![Loss Curves](outputs/loss_curves_comparison.png)

* **B1 (Scratch)**: Konvergensi lambat karena melatih seluruh bobot dari awal pada dataset skala kecil.
* **B2 & B3 (Pretrained)**: Konvergensi jauh lebih cepat berkat ektraksi fitur *pretrained* ImageNet.
* **B5 (EfficientNet-B0)**: Mencapai skor **Test Macro F1 tertinggi (0.9501)** dengan jumlah parameter **11.5x lebih hemat** dibanding ResNet-18 B3.

---

## 🔍 Failure Analysis

![Failure Analysis](outputs/failure_analysis.jpg)

Analisis sampel misklasifikasi menunjukkan kesalahan dominan dipicu oleh:
1. **High Inter-class Similarity**: Kemiripan fisik antar-ras (misal: *American Bulldog* vs *Boxer* / *Pit Bull*).
2. **Oklusi & Sudut Ekstrem**: Objek terpotong tiang atau diambil dari sudut *high-angle*.
3. **Pencahayaan Ekstrem**: Perubahan persepsi warna bulu akibat pencahayaan latar belakang.

---

## 🛠️ Cara Menjalankan Kode

1. Clone repositori ini:
   ```bash
   git clone [https://github.com/USERNAME/REPO_NAME.git](https://github.com/USERNAME/REPO_NAME.git)
   cd REPO_NAME
