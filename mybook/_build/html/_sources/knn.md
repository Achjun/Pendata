# Perhitungan KNN dengan Euclidean Distance (Data 1–9 ke Data 10)

Dataset yang digunakan merupakan data mahasiswa {download}`mahasiswa.csv <data/mahasiswa.csv>`:

Pada contoh ini, **Usia data ke-10 dianggap hilang**, lalu diprediksi menggunakan **K-Nearest Neighbor (KNN)** dengan **Euclidean Distance**.

---

## 1. Data ke-10 (Target)

| Data ke | Usia | Tingkat_Kepuasan | Status_Beasiswa | Program_Studi |
|--------|------|------------------|-----------------|---------------|
| 10 | ? | Sedang | Ya | Manajemen |

Karena atribut pembanding bersifat kategorikal, maka data harus diubah dulu ke bentuk numerik dengan **one-hot encoding**.

---

## 2. One-Hot Encoding

Atribut kategorikal yang dipakai:

- `Tingkat_Kepuasan`
- `Status_Beasiswa`
- `Program_Studi`

Hasil one-hot encoding untuk data ke-10:

| Data | Rendah | Sedang | Tinggi | Tidak | Ya | Akuntansi | Manajemen | Sistem Informasi |
|------|--------|--------|--------|-------|----|------------|------------|------------------|
| 10 | 0 | 1 | 0 | 0 | 1 | 0 | 1 | 0 |

---

## 3. Rumus Euclidean Distance

Rumus Euclidean Distance:

$$
d(x,y) = \sqrt{\sum_{i=1}^{n}(x_i-y_i)^2}
$$

Karena ada 8 kolom hasil one-hot encoding, maka rumusnya menjadi:

$$
d(x,y) = \sqrt{
(x_1-y_1)^2 +
(x_2-y_2)^2 +
(x_3-y_3)^2 +
(x_4-y_4)^2 +
(x_5-y_5)^2 +
(x_6-y_6)^2 +
(x_7-y_7)^2 +
(x_8-y_8)^2
}
$$

Urutan kolom:

1. Rendah  
2. Sedang  
3. Tinggi  
4. Tidak  
5. Ya  
6. Akuntansi  
7. Manajemen  
8. Sistem Informasi  

---

## 4. Data Pembanding 1–9 setelah One-Hot Encoding

| Data | Rendah | Sedang | Tinggi | Tidak | Ya | Akuntansi | Manajemen | Sistem Informasi |
|------|--------|--------|--------|-------|----|------------|------------|------------------|
| 1 | 0 | 1 | 0 | 1 | 0 | 0 | 1 | 0 |
| 2 | 1 | 0 | 0 | 0 | 1 | 0 | 0 | 1 |
| 3 | 0 | 0 | 1 | 1 | 0 | 1 | 0 | 0 |
| 4 | 0 | 1 | 0 | 0 | 1 | 0 | 1 | 0 |
| 5 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 1 |
| 6 | 0 | 0 | 1 | 0 | 1 | 1 | 0 | 0 |
| 7 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 0 |
| 8 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 1 |
| 9 | 1 | 0 | 0 | 1 | 0 | 1 | 0 | 0 |

---

## 5. Perhitungan Jarak Data 1 sampai 9 ke Data 10

### Data 1 ke Data 10

Data 1 = `(0,1,0,1,0,0,1,0)`  
Data 10 = `(0,1,0,0,1,0,1,0)`

$$
d(1,10)=\sqrt{
(0-0)^2 + (1-1)^2 + (0-0)^2 + (1-0)^2 + (0-1)^2 + (0-0)^2 + (1-1)^2 + (0-0)^2
}
$$

$$
d(1,10)=\sqrt{0+0+0+1+1+0+0+0}
$$

$$
d(1,10)=\sqrt{2}=1.414
$$

---

### Data 2 ke Data 10

Data 2 = `(1,0,0,0,1,0,0,1)`  
Data 10 = `(0,1,0,0,1,0,1,0)`

$$
d(2,10)=\sqrt{
(1-0)^2 + (0-1)^2 + (0-0)^2 + (0-0)^2 + (1-1)^2 + (0-0)^2 + (0-1)^2 + (1-0)^2
}
$$

$$
d(2,10)=\sqrt{1+1+0+0+0+0+1+1}
$$

$$
d(2,10)=\sqrt{4}=2.000
$$

---

### Data 3 ke Data 10

Data 3 = `(0,0,1,1,0,1,0,0)`  
Data 10 = `(0,1,0,0,1,0,1,0)`

$$
d(3,10)=\sqrt{
(0-0)^2 + (0-1)^2 + (1-0)^2 + (1-0)^2 + (0-1)^2 + (1-0)^2 + (0-1)^2 + (0-0)^2
}
$$

$$
d(3,10)=\sqrt{0+1+1+1+1+1+1+0}
$$

$$
d(3,10)=\sqrt{6}=2.449
$$

---

### Data 4 ke Data 10

Data 4 = `(0,1,0,0,1,0,1,0)`  
Data 10 = `(0,1,0,0,1,0,1,0)`

$$
d(4,10)=\sqrt{
(0-0)^2 + (1-1)^2 + (0-0)^2 + (0-0)^2 + (1-1)^2 + (0-0)^2 + (1-1)^2 + (0-0)^2
}
$$

$$
d(4,10)=\sqrt{0}
$$

$$
d(4,10)=0.000
$$

---

### Data 5 ke Data 10

Data 5 = `(1,0,0,1,0,0,0,1)`  
Data 10 = `(0,1,0,0,1,0,1,0)`

$$
d(5,10)=\sqrt{
(1-0)^2 + (0-1)^2 + (0-0)^2 + (1-0)^2 + (0-1)^2 + (0-0)^2 + (0-1)^2 + (1-0)^2
}
$$

$$
d(5,10)=\sqrt{1+1+0+1+1+0+1+1}
$$

$$
d(5,10)=\sqrt{6}=2.449
$$

---

### Data 6 ke Data 10

Data 6 = `(0,0,1,0,1,1,0,0)`  
Data 10 = `(0,1,0,0,1,0,1,0)`

$$
d(6,10)=\sqrt{
(0-0)^2 + (0-1)^2 + (1-0)^2 + (0-0)^2 + (1-1)^2 + (1-0)^2 + (0-1)^2 + (0-0)^2
}
$$

$$
d(6,10)=\sqrt{0+1+1+0+0+1+1+0}
$$

$$
d(6,10)=\sqrt{4}=2.000
$$

---

### Data 7 ke Data 10

Data 7 = `(0,0,1,1,0,0,1,0)`  
Data 10 = `(0,1,0,0,1,0,1,0)`

$$
d(7,10)=\sqrt{
(0-0)^2 + (0-1)^2 + (1-0)^2 + (1-0)^2 + (0-1)^2 + (0-0)^2 + (1-1)^2 + (0-0)^2
}
$$

$$
d(7,10)=\sqrt{0+1+1+1+1+0+0+0}
$$

$$
d(7,10)=\sqrt{4}=2.000
$$

---

### Data 8 ke Data 10

Data 8 = `(0,1,0,0,1,0,0,1)`  
Data 10 = `(0,1,0,0,1,0,1,0)`

$$
d(8,10)=\sqrt{
(0-0)^2 + (1-1)^2 + (0-0)^2 + (0-0)^2 + (1-1)^2 + (0-0)^2 + (0-1)^2 + (1-0)^2
}
$$

$$
d(8,10)=\sqrt{0+0+0+0+0+0+1+1}
$$

$$
d(8,10)=\sqrt{2}=1.414
$$

---

### Data 9 ke Data 10

Data 9 = `(1,0,0,1,0,1,0,0)`  
Data 10 = `(0,1,0,0,1,0,1,0)`

$$
d(9,10)=\sqrt{
(1-0)^2 + (0-1)^2 + (0-0)^2 + (1-0)^2 + (0-1)^2 + (1-0)^2 + (0-1)^2 + (0-0)^2
}
$$

$$
d(9,10)=\sqrt{1+1+0+1+1+1+1+0}
$$

$$
d(9,10)=\sqrt{6}=2.449
$$

---

## 6. Tabel Hasil Jarak

| Data | Usia | Jarak Euclidean |
|------|------|-----------------|
| 1 | 18 | 1.414 |
| 2 | 25 | 2.000 |
| 3 | 20 | 2.449 |
| 4 | 21 | 0.000 |
| 5 | 19 | 2.449 |
| 6 | 22 | 2.000 |
| 7 | 23 | 2.000 |
| 8 | 24 | 1.414 |
| 9 | 20 | 2.449 |

---

## 7. Urutkan Tetangga Terdekat

| Peringkat | Data | Usia | Jarak |
|-----------|------|------|-------|
| 1 | 4 | 21 | 0.000 |
| 2 | 1 | 18 | 1.414 |
| 3 | 8 | 24 | 1.414 |
| 4 | 2 | 25 | 2.000 |
| 5 | 6 | 22 | 2.000 |
| 6 | 7 | 23 | 2.000 |
| 7 | 3 | 20 | 2.449 |
| 8 | 5 | 19 | 2.449 |
| 9 | 9 | 20 | 2.449 |

---

## 8. Tentukan Nilai K

Misalkan digunakan:

$$
K = 3
$$

Maka 3 tetangga terdekat adalah:

| Data | Usia |
|------|------|
| 4 | 21 |
| 1 | 18 |
| 8 | 24 |

---

## 9. Prediksi Usia

Karena **Usia** adalah atribut numerik, maka digunakan rata-rata:

$$
Usia_{prediksi}=\frac{21+18+24}{3}
$$

$$
Usia_{prediksi}=\frac{63}{3}=21
$$

---

## 10. Kesimpulan

Berdasarkan perhitungan **KNN dengan Euclidean Distance** pada data ke-1 sampai ke-9 terhadap data ke-10, diperoleh 3 tetangga terdekat yaitu **data ke-4, data ke-1, dan data ke-8**. Maka nilai **Usia pada data ke-10 diprediksi sebesar 21 tahun**.

