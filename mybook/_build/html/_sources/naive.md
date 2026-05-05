# Tugas Klasifikasi: Naive Bayes

---

## 1. Pendahuluan

Tugas Klasifikasi: Prediksi Kelulusan Mahasiswa Menggunakan Naive Bayes dan Python.

Dokumen ini merupakan versi yang sudah disesuaikan dengan **dataset baru berjumlah 50 data**. Model klasifikasi yang digunakan adalah **Gaussian Naive Bayes** untuk memprediksi apakah mahasiswa **lulus** atau **tidak lulus** berdasarkan beberapa indikator akademik.

Fokus utama tugas ini adalah:

1. Membaca dataset baru berisi 50 data mahasiswa.
2. Melakukan **normalisasi data** menggunakan metode **Min-Max Normalization**.
3. Membagi data menjadi training dan testing set.
4. Melatih model **Gaussian Naive Bayes** menggunakan Python `scikit-learn` pada KNIME.
5. Melakukan prediksi dan evaluasi model.

---

## File Pendukung Tugas

Dataset baru yang digunakan:

- {download}`mahasiswa_lulus (xlsx) <data/mahasiswa_lulus.xlsx>`:  
- {download}`Workflow KNIME Terintegrasi Python (.knwf) <data/klasifikasi data.knwf>`

Dataset terdiri dari **50 baris data mahasiswa** dengan target klasifikasi `Lulus`.

---

## 2. Dataset

Dataset yang digunakan adalah dataset sintetis berisi 50 data mahasiswa. Setiap baris mewakili satu mahasiswa dengan beberapa atribut akademik.

| Nama Kolom | Tipe Data | Deskripsi |
| :--- | :--- | :--- |
| `ID_Mahasiswa` | Kategorikal/ID | Kode unik mahasiswa, tidak digunakan sebagai fitur model |
| `Jam_Belajar` | Numerik | Jumlah jam belajar mahasiswa per minggu |
| `Kehadiran` | Numerik | Persentase kehadiran mahasiswa dalam kelas |
| `Nilai_Tugas` | Numerik | Rata-rata nilai tugas mahasiswa |
| `Nilai_UTS` | Numerik | Nilai Ujian Tengah Semester |
| `Partisipasi_Kelas` | Numerik | Skor keaktifan mahasiswa di kelas, skala 1 sampai 10 |
| `Lulus` | Target | Label target: `1` berarti lulus, `0` berarti tidak lulus |

### 2.1 Fitur dan Target

Fitur yang digunakan untuk membangun model:

- `Jam_Belajar`
- `Kehadiran`
- `Nilai_Tugas`
- `Nilai_UTS`
- `Partisipasi_Kelas`

Kolom target:

- `Lulus`

Kolom yang tidak digunakan sebagai fitur:

- `ID_Mahasiswa`, karena hanya berfungsi sebagai identitas data.

---

## 3. Alur Kerja Workflow KNIME

Workflow KNIME dibuat secara berurutan dari pembacaan dataset sampai evaluasi hasil prediksi.

Urutan workflow:

1. **Excel Reader** atau **CSV Reader**
2. **Normalizer**
3. **Partitioning**
4. **Python Script Learner**
5. **Python Script Predictor**
6. **Scorer**
7. **Confusion Matrix Viewer**

---

## 4. Penjelasan Detail Per Node

### 4.1 Node Excel Reader / CSV Reader

![Tabel](naive/image.png)

**Fungsi:** Membaca dataset baru yang berisi 50 data mahasiswa.

Jika menggunakan file Excel:

- **Node:** Excel Reader
- **File Path:** `dataset_kelulusan_mahasiswa_50.xlsx`
- **Sheet Selection:** pilih sheet `Dataset`
- **Read Area:** Whole sheet

Jika menggunakan file CSV:

- **Node:** CSV Reader
- **File Path:** `dataset_kelulusan_mahasiswa_50.csv`
- **Delimiter:** Comma `,`
- **Header:** baris pertama sebagai nama kolom

**Output:** Tabel dengan 7 kolom:

- `ID_Mahasiswa`
- `Jam_Belajar`
- `Kehadiran`
- `Nilai_Tugas`
- `Nilai_UTS`
- `Partisipasi_Kelas`
- `Lulus`

---

### 4.2 Node Normalizer

![Tabel](naive/normalizer.png)

**Fungsi:** Melakukan normalisasi data menggunakan metode **Min-Max Normalization** agar seluruh fitur numerik berada pada rentang 0 sampai 1.

**Kolom yang dinormalisasi:**

- `Jam_Belajar`
- `Kehadiran`
- `Nilai_Tugas`
- `Nilai_UTS`
- `Partisipasi_Kelas`

**Kolom yang tidak dinormalisasi:**

- `ID_Mahasiswa`, karena hanya identitas.
- `Lulus`, karena merupakan target/label.

**Konfigurasi:**

- **Normalization Method:** Min-Max Normalization
- **New Minimum:** `0.0`
- **New Maximum:** `1.0`

**Rumus Min-Max:**

$$
X_{normalized} = \frac{X - X_{min}}{X_{max} - X_{min}}
$$

**Output:** Tabel dengan fitur numerik yang sudah berada pada rentang nilai `[0, 1]`.

---

### 4.3 Node Partitioning

![Tabel](naive/partisi.png)

**Fungsi:** Membagi dataset menjadi data training dan testing.

**Konfigurasi:**

- **Partitioning Mode:** Relative [%]
- **Training Set:** 80%
- **Testing Set:** 20%
- **Sampling Strategy:** Random
- **Random Seed:** `42` atau seed default KNIME

**Output:**

- **Port 0:** Data training sebanyak 80% dari dataset
- **Port 1:** Data testing sebanyak 20% dari dataset

Karena jumlah data adalah 50, maka pembagian 80:20 menghasilkan:

- 40 data training
- 10 data testing

---

### 4.4 Node Python Script Learner

![Tabel](naive/piton.png)

**Fungsi:** Melatih model **Gaussian Naive Bayes** menggunakan data training.

**Konfigurasi Port:**

- **Input Port 0 (Table):** data training dari node Partitioning
- **Output Port 0 (Object):** model Naive Bayes yang sudah dilatih

**Kode Python:**

```python
import knime.scripting.io as knio
from sklearn.naive_bayes import GaussianNB

# 1. Ambil data training dari input table KNIME
df = knio.input_tables[0].to_pandas()

# 2. Tentukan fitur dan target
fitur = ['Jam_Belajar', 'Kehadiran', 'Nilai_Tugas', 'Nilai_UTS', 'Partisipasi_Kelas']
X = df[fitur]
y = df['Lulus']

# 3. Buat dan latih model Gaussian Naive Bayes
model = GaussianNB()
model.fit(X, y)

# 4. Kirim model ke output object port
knio.output_objects[0] = model
```

**Penjelasan Kode:**

1. `knime.scripting.io` digunakan untuk komunikasi antara KNIME dan Python.
2. `GaussianNB` digunakan karena semua fitur yang dipakai adalah numerik.
3. Kolom `ID_Mahasiswa` tidak dimasukkan ke fitur karena bukan variabel prediktif.
4. Kolom `Lulus` digunakan sebagai target klasifikasi.
5. Model dikirim ke output port dalam bentuk Python Object.

**Output:** Model Gaussian Naive Bayes yang sudah dilatih.

---

### 4.5 Node Python Script Predictor

![Tabel](naive/predik.png)

**Fungsi:** Menggunakan model yang sudah dilatih untuk memprediksi data testing.

**Konfigurasi Port:**

- **Input Port 0 (Object):** model dari node Python Script Learner
- **Input Port 1 (Table):** data testing dari node Partitioning
- **Output Port 0 (Table):** tabel testing dengan kolom prediksi tambahan

**Kode Python:**

```python
import knime.scripting.io as knio

# 1. Ambil model dari input object
model = knio.input_objects[0]

# 2. Ambil data testing dari input table
test_df = knio.input_tables[0].to_pandas()

# 3. Tentukan kolom fitur yang sama dengan saat training
fitur = ['Jam_Belajar', 'Kehadiran', 'Nilai_Tugas', 'Nilai_UTS', 'Partisipasi_Kelas']
X_test = test_df[fitur]

# 4. Prediksi kelas kelulusan
predictions = model.predict(X_test)

# 5. Tambahkan hasil prediksi ke dataframe
test_df['Prediksi_Lulus'] = predictions

# 6. Kirim kembali ke KNIME sebagai tabel
knio.output_tables[0] = knio.Table.from_pandas(test_df)
```

**Output:** Tabel testing dengan kolom tambahan `Prediksi_Lulus`.

---

### 4.6 Node Scorer

![Tabel](naive/scorer.png)

**Fungsi:** Mengevaluasi performa model dengan membandingkan label asli dengan hasil prediksi.

**Konfigurasi:**

- **First Column / Actual:** `Lulus`
- **Second Column / Predicted:** `Prediksi_Lulus`

**Metrik Evaluasi:**

- **Accuracy:** persentase seluruh prediksi yang benar.
- **Precision:** ketepatan model saat memprediksi kelas lulus.
- **Recall:** kemampuan model menemukan seluruh mahasiswa yang benar-benar lulus.
- **F1-Score:** rata-rata harmonis antara precision dan recall.
- **Confusion Matrix:** tabel distribusi prediksi benar dan salah.

---

### 4.7 Confusion Matrix Viewer

**Fungsi:** Menampilkan confusion matrix agar kesalahan prediksi lebih mudah dianalisis.

Struktur confusion matrix:

```text
                Predicted: 0    Predicted: 1
Actual: 0       TN              FP
Actual: 1       FN              TP
```

Keterangan:

- **TN (True Negative):** mahasiswa diprediksi tidak lulus dan memang tidak lulus.
- **FP (False Positive):** mahasiswa diprediksi lulus, tetapi sebenarnya tidak lulus.
- **FN (False Negative):** mahasiswa diprediksi tidak lulus, tetapi sebenarnya lulus.
- **TP (True Positive):** mahasiswa diprediksi lulus dan memang lulus.

---

## 5. Hasil dan Analisis

### 5.1 Komposisi Dataset

Dataset baru terdiri dari 50 data dengan komposisi target:

| Kelas | Jumlah Data | Keterangan |
| :--- | ---: | :--- |
| `1` | 19 | Lulus |
| `0` | 31 | Tidak lulus |

### 5.2 Hasil Evaluasi Model

Dengan pembagian data 80% training dan 20% testing, jumlah data testing adalah 10 data.

Contoh hasil evaluasi menggunakan Gaussian Naive Bayes pada dataset ini:

| Metrik | Hasil | Interpretasi |
| :--- | ---: | :--- |
| Accuracy | 1.000 | Semua data testing diprediksi dengan benar |
| Precision | 1.000 | Semua prediksi lulus benar-benar lulus |
| Recall | 1.000 | Semua mahasiswa yang lulus berhasil dikenali |
| F1-Score | 1.000 | Keseimbangan precision dan recall sangat baik |

Confusion matrix contoh:

| Actual / Predicted | Predicted 0 | Predicted 1 |
| :--- | ---: | ---: |
| Actual 0 | 6 | 0 |
| Actual 1 | 0 | 4 |

### 5.3 Analisis Hasil

Model mampu memprediksi data testing dengan sangat baik karena pola pada dataset cukup jelas. Mahasiswa dengan kombinasi nilai akademik tinggi, kehadiran baik, jam belajar cukup, dan partisipasi kelas baik cenderung masuk kelas `1` atau lulus.

Namun, hasil sempurna pada dataset berjumlah 50 data tetap perlu dianalisis secara hati-hati. Beberapa kemungkinan penyebab akurasi tinggi adalah:

1. Dataset sintetis memiliki pola yang lebih teratur dibanding dataset nyata.
2. Jumlah data masih relatif kecil.
3. Data testing hanya 20% dari 50 data, yaitu 10 data.
4. Perlu pengujian lanjutan menggunakan data mahasiswa nyata atau data tambahan.

---

## 6. Kesimpulan

Tugas klasifikasi ini berhasil disesuaikan dengan dataset baru berjumlah 50 data mahasiswa. Dataset baru menggunakan lima fitur numerik, yaitu `Jam_Belajar`, `Kehadiran`, `Nilai_Tugas`, `Nilai_UTS`, dan `Partisipasi_Kelas`, dengan target `Lulus`.

Poin-poin penting:

1. **Dataset baru** berisi 50 data mahasiswa.
2. **Target klasifikasi** adalah `Lulus`, dengan nilai `1` untuk lulus dan `0` untuk tidak lulus.
3. **Normalisasi Min-Max** diterapkan pada semua fitur numerik.
4. **Gaussian Naive Bayes** cocok digunakan karena fitur yang dipakai berbentuk numerik.
5. **Workflow KNIME** tetap modular, mulai dari pembacaan dataset, normalisasi, partitioning, training, prediksi, hingga evaluasi.
6. Model menghasilkan performa sangat baik pada data testing, tetapi tetap perlu diuji menggunakan dataset yang lebih besar dan lebih realistis.

