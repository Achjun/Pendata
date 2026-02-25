# Visualisasi Distribusi Data

Visualisasi distribusi data adalah teknik grafis untuk menunjukkan bagaimana nilai-nilai dalam kumpulan data tersebar, mengelompok, atau membentuk pola tertentu (seperti Histogram, Boxplot atau Density plot).

## Histogram
Histogram digunakan untuk menampilkan distribusi frekuensi dari data numerik dengan membagi data ke dalam beberapa interval (bins). Visualisasi ini membantu memahami pola penyebaran data, seperti kecenderungan nilai, tingkat variasi, serta kemungkinan adanya nilai ekstrem (outlier).

Pada dataset Iris, histogram digunakan untuk melihat sebaran nilai pada setiap fitur sehingga memudahkan analisis awal sebelum dilakukan pengolahan data lebih lanjut.  

```{figure} images/gambar_1.png
---
width: 80%
align: center
---
Fig. 2 Analisis Statistik Deskriptif Fitur *sepal_length*  
```

## BoxPlot
Boxplot merupakan visualisasi statistik yang digunakan untuk menggambarkan ringkasan distribusi data melalui nilai minimum, kuartil pertama (Q1), median, kuartil ketiga (Q3), dan maksimum. Boxplot juga menampilkan outlier, yaitu data yang berada di luar rentang normal.

Pada dataset Iris, boxplot membantu melihat sebaran data, tingkat variasi, serta perbedaan karakteristik antar fitur secara cepat. Visualisasi ini efektif untuk membandingkan distribusi data dan mendeteksi nilai ekstrem sebelum dilakukan analisis lebih lanjut.

```{figure} images/box.png
---
width: 80%
align: center
---
Fig. 3 Visualisasi distribusi data bentuk BoxPlot *sepal_length*  
```