# Analisis dan Penjelasan Workflow Orange Data Mining (uas.ows)

Dokumen ini berisi penjelasan lengkap langkah demi langkah mengenai alur kerja (*workflow*) yang terdapat dalam file `uas.ows`. Workflow ini dirancang untuk melakukan analisis data, pra-pemrosesan, pemodelan menggunakan metode **Decision Tree**, serta evaluasi performa model terhadap dataset **Higher Education Students Performance Evaluation**.

---

## 1. Daftar dan Penjelasan Setiap Widget (Nodes)

Di dalam file skema Anda, terdapat 10 widget yang masing-masing memiliki peran spesifik:

### A. Widget 0: File
* **Nama Widget:** `File`
* **Fungsi:** Menjadi gerbang awal untuk memuat dataset luar ke dalam Orange. Berdasarkan riwayat file Anda, widget ini membaca file lokal bernama `DATA (1).csv` yang diunduh dari UCI Machine Learning Repository.

### B. Widget 1: Data Table
* **Nama Widget:** `Data Table`
* **Fungsi:** Menampilkan data mentah dari widget `File` dalam bentuk baris dan kolom seperti spreadsheet. Ini mempermudah Anda untuk melihat nilai instans data secara langsung sebelum diproses lebih lanjut.

### C. Widget 7: Data Info
* **Nama Widget:** `Data Info`
* **Fungsi:** Memberikan ringkasan metadata dari dataset yang dimuat. Widget ini menampilkan informasi dasar seperti jumlah baris (145 instans), jumlah fitur (31 fitur), ada tidaknya data kosong (*missing values*), serta tipe variabelnya.

### D. Widget 8: Preprocess
* **Nama Widget:** `Preprocess`
* **Fungsi:** Melakukan transformasi atau pembersihan data. Berdasarkan berkas konfigurasi dan konfirmasi visual Anda, widget ini menerapkan metode **Normalize features** dengan pilihan **"Normalize to interval [0, 1]"** atau biasa disebut **Min-Max Scaling**. Metode ini mengubah seluruh nilai fitur menjadi skala desimal antara 0 hingga 1.

### E. Widget 9: Data Table (1)
* **Nama Widget:** `Data Table (1)`
* **Fungsi:** Menampilkan hasil data yang telah melalui proses transformasi pada widget `Preprocess`. Di sini Anda bisa melihat perbedaan nilai angka bulat asli yang kini telah berubah menjadi pecahan desimal antara 0 dan 1.

### F. Widget 4: Select Columns
* **Nama Widget:** `Select Columns`
* **Fungsi:** Mengatur peran (*role*) dari masing-masing kolom data. Di sinilah Anda memisahkan data menjadi:
  * **Features (X):** 31 kolom perilaku, demografi, dan latar belakang mahasiswa.
  * **Target (y):** Kolom `OUTPUT Grade` yang bertindak sebagai label kelas yang ingin diprediksi.

### G. Widget 2: Rank
* **Nama Widget:** `Rank`
* **Fungsi:** Melakukan seleksi fitur (*Feature Selection*) dengan mengukur tingkat kepentingan setiap variabel prediktor terhadap variabel target menggunakan metode statistik seperti *Information Gain*, *Gain Ratio*, atau *Gini Impurity*. Fitur yang memiliki skor tertinggi berarti paling berpengaruh terhadap nilai akhir mahasiswa.

### H. Widget 3: Tree (Decision Tree Learner)
* **Nama Widget:** `Tree`
* **Fungsi:** Algoritma *Machine Learning* yang bertindak sebagai model pembelajaran. Menggunakan metode **Decision Tree** (Pohon Keputusan), ia menyusun aturan logika berbentuk pohon bercabang untuk mengklasifikasikan kelas `OUTPUT Grade` mahasiswa berdasarkan fitur-fitur yang tersedia.

### I. Widget 5: Test and Score
* **Nama Widget:** `Test and Score`
* **Fungsi:** Melakukan pengujian dan evaluasi performa model. Diatur menggunakan metode **Cross-Validation** (Validasi Silang, 10-fold), widget ini membagi data menjadi beberapa bagian untuk dilatih dan diuji secara bergantian guna mendapatkan metrik performa yang objektif seperti *Classification Accuracy (CA)*, *F1-Score*, *Precision*, dan *Recall*.

### J. Widget 6: Confusion Matrix
* **Nama Widget:** `Confusion Matrix`
* **Fungsi:** Menampilkan tabel visual yang membandingkan hasil prediksi model *Decision Tree* dengan kelas aktual/sebenarnya dari data mahasiswa. Anda bisa melihat dengan jelas kelas mana yang berhasil diprediksi dengan tepat dan di kelas mana model sering melakukan kesalahan klasifikasi.

---

## 2. Penjelasan Alur Hubungan Antar Widget (Links)

Hubungan antarkoneksi garis dalam skema Orange Anda mengalir melalui beberapa jalur utama:

1. **Jalur Eksplorasi Data Awal:**
   * `File` -> `Data Table`: Mengirimkan seluruh data mentah agar bisa diinspeksi secara visual.
   * `File` -> `Data Info`: Mengirimkan data untuk memunculkan ringkasan jumlah baris dan kolom.
   * `Data Table` -> `Select Columns`: Meneruskan data yang dipilih dari tabel menuju tahap penentuan target pemodelan.

2. **Jalur Normalisasi Data (Eksperimen Terpisah):**
   * `File` -> `Preprocess` -> `Data Table (1)`: Mengambil data mentah asli -> Mengubah skalanya menjadi interval [0, 1] -> Menampilkan hasilnya pada tabel data baru untuk dicek perubahannya.

3. **Jalur Pemodelan dan Evaluasi (Inti Klasifikasi):**
   * `Select Columns` -> `Rank`: Membantu Anda menganalisis variabel mana saja yang paling relevan secara statistik sebelum pohon keputusan dibangun.
   * `Select Columns` -> `Tree`: Mengirimkan data terstruktur (Fitur & Target) ke algoritma pembelajar Pohon Keputusan untuk membentuk model penentu keputusan.
   * `Select Columns` -> `Test and Score`: Mengirimkan data mentah terstruktur untuk digunakan sebagai bahan pengujian validasi silang (*Cross-Validation*).
   * `Tree` -> `Test and Score`: Mengirimkan algoritma/struktur model *Decision Tree* agar diuji kinerjanya di dalam mesin evaluasi.
   * `Test and Score` -> `Confusion Matrix`: Meneruskan hasil skor prediksi akhir ke dalam bentuk matriks visual untuk dianalisis lebih lanjut tingkat kesalahannya.

---

## 3. Kesimpulan Analisis Workflow

Struktur alur kerja dalam file `uas.ows` Anda sudah dirancang dengan **sangat komprehensif**. Anda memisahkan alur dengan baik antara:
1. Tahap pemahaman data awal (`Data Info` & `Data Table`).
2. Uji coba transformasi data (`Preprocess`).
3. Evaluasi analitis fitur (`Rank`).
4. Proses pemodelan klasifikasi yang valid secara ilmiah (`Select Columns` -> `Tree` -> `Test and Score` -> `Confusion Matrix`). 

Workflow ini sangat ideal untuk pengerjaan tugas akademik maupun proyek data sains terstruktur karena menjamin transparansi data di setiap tahapannya.
