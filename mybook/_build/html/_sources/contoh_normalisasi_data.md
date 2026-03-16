# Contoh Normalisasi Data pada Dataset Mahasiswa

Dataset yang digunakan merupakan data mahasiswa {download}`mahasiswa.csv <data/mahasiswa.csv>`:

Dataset memiliki atribut **Usia** dengan statistik:

- Xmin = 18  
- Xmax = 25  
- Mean = 21.5  
- Standar deviasi ≈ 2.156  
- j = 2 (jumlah digit nilai maksimum untuk decimal scaling)

---

# 1. Min-Max Normalization

### Rumus

$$
X' = \frac{X - X_{min}}{X_{max} - X_{min}}
$$

### Contoh Perhitungan

Jika X = 20

$$
X' = \frac{20 - 18}{25 - 18}
$$

$$
X' = \frac{2}{7} = 0.286
$$

---

# 2. Z-Score Normalization

### Rumus

$$
X' = \frac{X - \mu}{\sigma}
$$

### Contoh Perhitungan

Jika X = 20

$$
X' = \frac{20 - 21.5}{2.156}
$$

$$
X' ≈ -0.696
$$

---

# 3. Decimal Scaling Normalization

### Rumus

$$
X' = \frac{X}{10^j}
$$

Karena nilai maksimum memiliki **2 digit**, maka:

$$
j = 2
$$

### Contoh

Jika X = 20

$$
X' = \frac{20}{100} = 0.2
$$

---

# 4. Mean Normalization

### Rumus

$$
X' = \frac{X - mean}{X_{max} - X_{min}}
$$

### Contoh

Jika X = 20

$$
X' = \frac{20 - 21.5}{25 - 18}
$$

$$
X' = \frac{-1.5}{7} ≈ -0.214
$$

---

# Tabel Hasil Normalisasi Dataset

| ID | Usia | Min-Max | Z-Score | Decimal Scaling | Mean Normalization |
|----|------|--------|--------|----------------|-------------------|
| 1 | 18 | 0.000 | -1.623 | 0.18 | -0.500 |
| 2 | 25 | 1.000 | 1.623 | 0.25 | 0.500 |
| 3 | 20 | 0.286 | -0.696 | 0.20 | -0.214 |
| 4 | 21 | 0.429 | -0.232 | 0.21 | -0.071 |
| 5 | 19 | 0.143 | -1.159 | 0.19 | -0.357 |
| 6 | 22 | 0.571 | 0.232 | 0.22 | 0.071 |
| 7 | 23 | 0.714 | 0.696 | 0.23 | 0.214 |
| 8 | 24 | 0.857 | 1.159 | 0.24 | 0.357 |
| 9 | 20 | 0.286 | -0.696 | 0.20 | -0.214 |
| 10 | 21 | 0.429 | -0.232 | 0.21 | -0.071 |

---

# Kesimpulan

Empat metode normalisasi yang digunakan pada dataset:

1. **Min-Max Normalization** → mengubah data ke rentang 0–1  
2. **Z-Score Normalization** → menggunakan mean dan standar deviasi  
3. **Decimal Scaling** → menggeser titik desimal berdasarkan digit maksimum  
4. **Mean Normalization** → menggunakan rata-rata dan rentang data