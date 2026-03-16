# Perhitungan Missing Value Menggunakan Metode WKNN

Data:

| No | IPK | PO | JML | IPK_MinMax | PO_MinMax | JML_MinMax |
|----|----|---------|----|-----------|-----------|-----------|
|1|2|2000000|2|0|0|0|
|2|3|3000000|3|0.5|0.5|1|
|3|4|2000000|2|1|0|0|
|4|2|2000000|3|0|0|1|
|5|3|3000000|2|0.5|0.5|0|
|6|4|4000000|3|1|1|1|
|7|2|3000000|?|0|0.5|?|

Missing value terdapat pada **JML data ke-7**.

Data target (data ke-7):

(IPK, PO) = (0 , 0.5)

---

Rumus jarak Euclidean:

$$
d = \sqrt{(x_1-x_2)^2 + (y_1-y_2)^2}
$$

Perhitungan jarak:

| No | Perhitungan | Jarak |
|----|-------------|-------|
|1|√((0−0)² + (0−0.5)²)|0.5|
|2|√((0.5−0)² + (0.5−0.5)²)|0.5|
|3|√((1−0)² + (0−0.5)²)|1.118|
|4|√((0−0)² + (0−0.5)²)|0.5|
|5|√((0.5−0)² + (0.5−0.5)²)|0.5|
|6|√((1−0)² + (1−0.5)²)|1.118|

---

Rumus bobot WKNN:

$$
w = \frac{1}{d}
$$

Perhitungan bobot:

| No | Jarak | Bobot | JML_MinMax |
|----|------|------|-------------|
|1|0.5|2|0|
|2|0.5|2|1|
|3|1.118|0.894|0|
|4|0.5|2|1|
|5|0.5|2|0|
|6|1.118|0.894|1|

---

Rumus prediksi:

$$
y = \frac{\sum (w_i \times y_i)}{\sum w_i}
$$

Perhitungan:

$$
y =
\frac{(2×0)+(2×1)+(0.894×0)+(2×1)+(2×0)+(0.894×1)}
{2+2+0.894+2+2+0.894}
$$

$$
y = \frac{4.894}{9.788}
$$

$$
y \approx 0.5
$$

---

Interpretasi hasil:

Nilai hasil WKNN:

JML_normalisasi ≈ 0.5

Pada data training:

0 → JML = 2  
1 → JML = 3  

Karena nilai berada di tengah, maka dipilih nilai yang paling dekat.

---

Hasil akhir:

| No | IPK | PO | JML |
|----|----|----|----|
|7|2|3000000|2|

Missing value pada **JML data ke-7 diprediksi bernilai 2** menggunakan metode **Weighted K-Nearest Neighbor (WKNN)**.