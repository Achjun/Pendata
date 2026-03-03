# Mengukur Jarak

## Mengapa Mengukur Jarak Penting dalam Penambangan Data?

Dalam penambangan data (*data mining*), **mengukur jarak (distance measurement)** sangat penting karena banyak algoritma bekerja berdasarkan konsep **kemiripan (similarity)** atau **ketidaksamaan (dissimilarity)** antar data.  

Jarak adalah cara kuantitatif untuk menentukan seberapa mirip atau berbeda dua data.  


## 1. Dasar untuk Clustering (Pengelompokan)

Algoritma seperti:

- K-Means  
- Hierarchical Clustering  
- DBSCAN  

mengelompokkan data berdasarkan **jarak antar titik data**.

Contoh:  
Jika dua pelanggan memiliki usia, pendapatan, dan pola belanja yang mirip (jaraknya kecil), maka mereka kemungkinan masuk ke cluster yang sama.

Tanpa pengukuran jarak → sistem tidak tahu mana data yang “dekat” atau “jauh”.  

## 2. Digunakan dalam K-Nearest Neighbors (KNN)

Pada algoritma **KNN**, prediksi dilakukan berdasarkan prinsip:

- Data baru akan mengikuti kelas dari tetangga terdekatnya.

Di sini, jarak menentukan:
- Siapa tetangga terdekat
- Seberapa dekat mereka

Jika pengukuran jarak salah → hasil klasifikasi bisa salah.

## 3. Mengukur Kemiripan Data

Dalam banyak kasus kita ingin mengetahui:

- Dokumen mana yang paling mirip?
- Produk mana yang serupa?
- Pasien mana yang memiliki kondisi hampir sama?

Contoh metrik jarak:
- **Euclidean Distance** → untuk data numerik
- **Manhattan Distance** → untuk data multidimensi
- **Cosine Similarity** → untuk data teks
- **Hamming Distance** → untuk data biner

## 4. Deteksi Outlier (Anomali)

Data yang memiliki jarak sangat jauh dari kelompok lain dapat dianggap sebagai **anomali**.

Contoh:  
Dalam sistem deteksi fraud, transaksi yang “jauh” dari pola normal bisa dianggap mencurigakan.

## 5. Berpengaruh terhadap Akurasi Model

Pemilihan jenis jarak sangat krusial.

- Euclidean cocok untuk data numerik dengan skala yang sama
- Cosine cocok untuk teks
- Hamming cocok untuk data biner

Jika salah memilih metrik jarak:
- Cluster bisa tidak masuk akal
- Prediksi bisa bias
- Model bisa gagal

## 6. Fondasi Representasi Data dalam Ruang Dimensi

Dalam data mining, data direpresentasikan sebagai titik dalam ruang multidimensi.

Jarak membantu menjawab:
- Seberapa dekat dua titik dalam ruang tersebut?
- Bagaimana struktur data secara keseluruhan?

## Kesimpulan

Mengukur jarak penting karena hampir semua teknik data mining berbasis pada konsep **kedekatan atau kemiripan antar data**.

Tanpa pengukuran jarak:
- Tidak ada clustering yang efektif
- Tidak ada KNN
- Tidak ada deteksi anomali berbasis jarak
- Tidak ada pengukuran kemiripan yang objektif