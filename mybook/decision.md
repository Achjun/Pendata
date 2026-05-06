#  Decision Tree

## 📌 Pendahuluan
Workflow ini dibuat menggunakan **KNIME Analytics Platform** dan bertujuan untuk melakukan proses *data mining* menggunakan algoritma **Decision Tree**.

Decision Tree adalah metode klasifikasi yang digunakan untuk memprediksi suatu kelas berdasarkan aturan berbentuk pohon keputusan (tree), yang terdiri dari node, cabang, dan daun (leaf).

---

## 🎯 Tujuan Workflow
Tujuan dari workflow ini adalah:
- Melatih model klasifikasi menggunakan algoritma Decision Tree  
- Menguji performa model terhadap data uji  
- Menampilkan hasil evaluasi model  
- Memvisualisasikan struktur pohon keputusan  

---

## 🔄 Alur Proses Workflow

```mermaid
graph LR
A[Excel Reader] --> B[Partitioning]
B --> C[Decision Tree Learner]
C --> D[Decision Tree Predictor]
D --> E[Scorer]
C --> F[Decision Tree View]
```
---

## 🧩 Penjelasan Detail Setiap Node

### 1. Excel Reader

![Tabel](decison/1.png)

Node Excel Reader digunakan untuk membaca data dari file Excel (.xlsx atau .xls).

Konfigurasi utama:

- Memilih file Excel sebagai input
- Menentukan sheet yang digunakan
- Menentukan apakah baris pertama sebagai header

Output:

Data tabel (dataset) yang siap diproses



---
### 2. Partitioning

![Tabel](decison/2.png)

Node Partitioning digunakan untuk membagi dataset menjadi dua bagian, yaitu data latih dan data uji.

Konfigurasi utama:

Rasio pembagian data (misalnya 70% training, 30% testing)
Metode sampling (random atau stratified)

Output:

Port 1: Training data
Port 2: Testing data


---
### 3. Decision Tree Learner

![Tabel](decison/3.png)

Node Decision Tree Learner digunakan untuk membangun model klasifikasi berbasis pohon keputusan.

Konfigurasi utama:

- Menentukan atribut target (label/kelas)
- Menentukan kriteria pemisahan (misalnya Gini Index atau Information Gain)
- Mengatur kedalaman maksimum pohon (max depth)

Output:

Model Decision Tree


---
### 4. Decision Tree Predictor

![Tabel](decison/4.png)

Node Decision Tree Predictor digunakan untuk menerapkan model yang telah dibuat ke data testing.

Konfigurasi utama:

- Menghubungkan model dari Learner
- Menggunakan dataset testing sebagai input

Output:

Data testing yang sudah ditambahkan kolom hasil prediksi

---
### 5. Scorer

![Tabel](decison/5.png)

Node Scorer digunakan untuk mengevaluasi performa model klasifikasi.

Konfigurasi utama:

Menentukan kolom actual (label asli)
Menentukan kolom predicted (hasil prediksi)

Output:

- Confusion Matrix
- Accuracy
- Precision
- -Recall

---
### 6. Decision Tree View

![Tabel](decison/6.png)

Node Decision Tree View digunakan untuk menampilkan visualisasi dari model Decision Tree.

Fitur utama:

- Menampilkan struktur pohon
- Menampilkan aturan keputusan (rule)
- Menunjukkan atribut yang digunakan pada setiap percabangan

Output:

Visualisasi pohon keputusan

---
### Kesimpulan

Workflow ini menunjukkan proses lengkap dalam pembuatan model machine learning menggunakan algoritma Decision Tree, mulai dari input data hingga evaluasi model.

Langkah-langkah utama:

- Membaca data
- Membagi data
- Melatih model
- Melakukan prediksi
- Mengevaluasi hasil
- Visualisasi model


---