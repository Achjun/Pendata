# Rumus dan Langkah Regresi Linier

## Data

| Titik | x | y |
|---|---:|---:|
| A | 2 | 2 |
| B | 4 | 3 |
| C | 5 | 5 |
| D | 3 | 4 |
| E | 3 | 3 |
| F | 4 | 5 |
| G | 5 | 6 |

---

## 1. Model Regresi Linier

Model regresi linier sederhana adalah:

```text
y = b0 + b1x + e
```

Keterangan:

- `y` = nilai yang diprediksi
- `x` = variabel input
- `b0` = intercept atau titik potong garis dengan sumbu y
- `b1` = koefisien regresi atau kemiringan garis
- `e` = error atau residual

Tujuan regresi linier adalah mencari garis terbaik yang dapat mewakili pola data.

---

## 2. Jumlah Data

Jumlah titik data:

```text
n = 7
```

---

## 3. Membuat Tabel Bantuan

Untuk menghitung regresi linier, kita membutuhkan nilai:

- `x`
- `y`
- `x²`
- `xy`

| Titik | x | y | x² | xy |
|---|---:|---:|---:|---:|
| A | 2 | 2 | 4 | 4 |
| B | 4 | 3 | 16 | 12 |
| C | 5 | 5 | 25 | 25 |
| D | 3 | 4 | 9 | 12 |
| E | 3 | 3 | 9 | 9 |
| F | 4 | 5 | 16 | 20 |
| G | 5 | 6 | 25 | 30 |
| **Jumlah** | **26** | **28** | **104** | **112** |

Jadi diperoleh:

```text
Σx = 26
Σy = 28
Σx² = 104
Σxy = 112
```

---

## 4. Menghitung Koefisien b1

Rumus koefisien regresi atau kemiringan garis adalah:

```text
b1 = [nΣxy - (Σx)(Σy)] / [nΣx² - (Σx)²]
```

Masukkan nilai yang sudah diketahui:

```text
b1 = [7(112) - (26)(28)] / [7(104) - (26)²]
```

```text
b1 = [784 - 728] / [728 - 676]
```

```text
b1 = 56 / 52
```

```text
b1 = 14 / 13
```

```text
b1 = 1.0769
```

Jadi:

```text
b1 = 1.0769
```

---

## 5. Menghitung Intercept b0

Rumus intercept adalah:

```text
b0 = [Σy - b1Σx] / n
```

Masukkan nilai yang sudah diketahui:

```text
b0 = [28 - (1.0769)(26)] / 7
```

Karena:

```text
1.0769 × 26 = 28
```

Maka:

```text
b0 = [28 - 28] / 7
```

```text
b0 = 0
```

Jadi:

```text
b0 = 0
```

---

## 6. Membentuk Persamaan Regresi

Rumus awal:

```text
y = b0 + b1x
```

Masukkan nilai `b0` dan `b1`:

```text
y = 0 + 1.0769x
```

Maka persamaan regresinya adalah:

```text
y = 1.0769x
```

Atau dalam bentuk pecahan:

```text
y = 14/13 x
```

---

## 7. Menghitung Prediksi

Rumus prediksi:

```text
ŷ = 1.0769x
```

| Titik | x | y aktual | y prediksi |
|---|---:|---:|---:|
| A | 2 | 2 | 2.1538 |
| B | 4 | 3 | 4.3077 |
| C | 5 | 5 | 5.3846 |
| D | 3 | 4 | 3.2308 |
| E | 3 | 3 | 3.2308 |
| F | 4 | 5 | 4.3077 |
| G | 5 | 6 | 5.3846 |

---

## 8. Menghitung Residual atau Error

Residual adalah selisih antara nilai aktual dengan nilai prediksi.

Rumus residual:

```text
e = y - ŷ
```

| Titik | y aktual | y prediksi | residual |
|---|---:|---:|---:|
| A | 2 | 2.1538 | -0.1538 |
| B | 3 | 4.3077 | -1.3077 |
| C | 5 | 5.3846 | -0.3846 |
| D | 4 | 3.2308 | 0.7692 |
| E | 3 | 3.2308 | -0.2308 |
| F | 5 | 4.3077 | 0.6923 |
| G | 6 | 5.3846 | 0.6154 |

---

## 9. Interpretasi

Persamaan regresi:

```text
y = 1.0769x
```

Artinya, setiap nilai `x` naik 1 satuan, maka nilai `y` diprediksi naik sekitar `1.0769` satuan.

Karena `b0 = 0`, maka garis regresi memotong sumbu y di titik 0.

---

## 10. Kesimpulan

Berdasarkan data:

```text
A = (2, 2)
B = (4, 3)
C = (5, 5)
D = (3, 4)
E = (3, 3)
F = (4, 5)
G = (5, 6)
```

diperoleh persamaan regresi linier:

```text
y = 1.0769x
```


Garis ini adalah garis terbaik berdasarkan metode **least squares**, yaitu metode yang memilih garis dengan jumlah kuadrat residual terkecil.


## 11. Visualisai akhir

![Regresi linear](images/image.png)