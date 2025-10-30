# 🌀 CCAV (Chaotic Chisa-chan Abstract Vision)

> Clean Chaotic Abstract Vision — custom method buat akselerasi training CNN dengan inspirasi Dropout, Early Stopping, dan traversal ala DFS.
> Cocok buat eksperimen di hardware terbatas (contoh: laptop iGPU).

---

## 📖 Deskripsi
CCAV adalah varian sederhana dari CNN yang pakai metode **chaotic node traversal**.
Alih-alih semua node layer dilalui, hanya **30–70% subset node** yang diaktifkan secara semi-random.
Tujuannya:
- 🔹 Ngehemat resource training
- 🔹 Latency lebih kecil
- 🔹 Tetep bisa jaga akurasi di level acceptable

---

## ⚙️ Fitur Utama
- Chaos Layer (semi-random node activation)
- Early Stopping bawaan
- Support PyTorch + Torch-DirectML (buat laptop kentang)
- Metrics lengkap: Accuracy, F1-Score, Recall, Latency

---

## 🏗️ Arsitektur
1. **Pre-processing**: Resize, normalize, augmentasi dataset
2. **CNN Backbone**: Conv → Pool → FC
3. **Chaos Layer**: DFS-inspired node skipping
4. **Stop Condition**: Training berhenti saat akurasi stagnan

---

## 📊 Perbandingan (Contoh Dummy)
| Model            | Akurasi | F1 | Latency | Notes |
|------------------|---------|----|---------|-------|
| CNN Standar      | 85%     | 0.82 | 120ms | baseline |
| CNN + Dropout    | 84%     | 0.83 | 115ms | lebih stabil |
| CNN + EarlyStop  | 83%     | 0.81 | 100ms | cepat convergence |
| **CCAVNet**      | 82%     | 0.80 | 70ms  | trade-off speed |

---

## 🚀 Instalasi
```bash
git clone https://github.com/im-bara/CCAVNet.git
cd CCAVNet
pip install -r requirements.txt
```

## Install Coy (Wajib Hukumnya, haram kalo gak di Install gk bisa Training nanti)
```requirements.txt
torch
torchvision
numpy
scikit-learn
pillow
torch-directml   # optional buat Windows + iGPU
torchvision-directml   # optional buat Windows + iGPU
```
## Cara Vakai (Godvlan Mode)
```bash
python train.py --dataset ./data --ephocs 50 --chaos 0.5
```
### Options :
- `--dataset`: Path to dataset directory.
- `--epochs`: Number of training epochs.
- `--chaos`: Probability of node skipping in Chaos Layer. (Rekomendasi: 0.3-0.7) lebih dari itu Mending Lu pake Dropout atau lainnya
- `--directml`: Use DirectML backend for GPU acceleration.

## 📌 Note ya Cuy
- Data Set Kecil 150 kurang lebih sih.
- Training bisa dilakukan dengan GPU atau CPU.
- Jangan Lupa Tune Hyperparameter.
- Perluas Dataset dengan lebih banyak gambar.
- Jangan Lupa Save Model setelah Training.

## 🪄 Roadmap
- Uji di dataset yang lebih besar (Seperti CIFAR-10, ImageNet subnet)
- Implementasi pada aplikasi real-time
- Bandingin sama MobileNet/ResNet

## 📜 Reference
- [Paper](https://www.nature.com/articles/nature14539)
- [Paper](https://arxiv.org/pdf/1512.03385)
- [Paper](https://jmlr.org/papers/volume15/srivastava14a/srivastava14a.pdf)
- Depth-First Search Graph Theory
- [Code](https://github.com/im-bara/CCAVNet)
