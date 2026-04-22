# uts

## 1. Gambaran Umum
Workflow ini dibuat menggunakan **Orange Data Mining** untuk melakukan:
- Preprocessing data
- Eksplorasi data (visualisasi)
- Pemodelan machine learning (kNN)
- Evaluasi model

Dataset yang digunakan:
- Dataset kesuburan tanah (terdapat missing value)

---

## 2. Alur Kerja (Workflow)

### 🔹 1. Input Data
**Widget:** `CSV File Import`  
- Mengimpor dataset dari file CSV  
- Data awal kemungkinan masih memiliki missing value  

**Output:** Data mentah  

---

### 🔹 2. Menampilkan Data Awal
**Widget:** `Data Table`  
- Menampilkan isi dataset untuk inspeksi awal  

**Tujuan:**
- Melihat struktur data  
- Mengetahui missing value  

---

### 🔹 3. Seleksi Fitur
**Widget:** `Select Columns`  
- Memilih atribut yang digunakan sebagai:
  - Feature (input)
  - Target (label)

**Output:** Data terpilih  

---

### 🔹 4. Eksplorasi Data (EDA)

#### a. Distribusi Data
**Widget:** `Distributions`  
- Melihat distribusi tiap fitur  

#### b. Box Plot
**Widget:** `Box Plot`  
- Melihat outlier  

**Tujuan:**
- Memahami karakteristik data  
- Deteksi anomali  

---

### 🔹 5. Menangani Missing Value
**Widget:** `Impute`  
- Mengisi nilai yang hilang (missing value)  
- Metode umum: mean, median, dll  

**Output:** Data bersih dari missing value  

---

### 🔹 6. Transformasi Data
**Widget:** `Continuize`  
- Mengubah data kategorikal menjadi numerik  

**Penting untuk:**
- Algoritma kNN (butuh numerik)  

---

### 🔹 7. Preprocessing Lanjutan
**Widget:** `Preprocess`  

Biasanya meliputi:
- Normalisasi / standardisasi  
- Scaling data  

**Output:** Data siap untuk modeling  

---

### 🔹 8. Modeling (Machine Learning)
**Widget:** `kNN (k-Nearest Neighbor)`  
- Menggunakan algoritma kNN untuk klasifikasi  

**Input:**
- Data hasil preprocessing  

**Output:**
- Model kNN  

---

### 🔹 9. Evaluasi Model
**Widget:** `Test and Score`  
- Menguji performa model  
- Biasanya menggunakan:
  - Cross-validation  

**Output:**
- Akurasi  
- Precision  
- Recall  
- F1-score  

---

### 🔹 10. Confusion Matrix
**Widget:** `Confusion Matrix`  
- Menampilkan hasil prediksi vs aktual  

**Berguna untuk:**
- Melihat kesalahan klasifikasi  

---

### 🔹 11. Reduksi Dimensi (Opsional)
**Widget:** `PCA`  
- Mengurangi dimensi data  

**Tujuan:**
- Visualisasi lebih mudah  
- Mengurangi kompleksitas  

---

### 🔹 12. Visualisasi
**Widget:** `Scatter Plot`  
- Menampilkan data dalam bentuk 2D  

**Input:**
- Data dari PCA  

---

## 3. Ringkasan Alur
