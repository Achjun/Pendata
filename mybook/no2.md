# Peramalan Kadar NO₂ di Daerah Bangkalan Madura (Revisi)

## Latar Belakang

Peningkatan aktivitas industri, transportasi, serta pertumbuhan populasi yang pesat telah menyebabkan peningkatan signifikan terhadap tingkat pencemaran udara di berbagai wilayah. Salah satu polutan udara utama yang menjadi perhatian adalah Nitrogen Dioksida (NO₂), yaitu gas beracun yang dihasilkan terutama dari proses pembakaran bahan bakar fosil seperti kendaraan bermotor, pembangkit listrik, dan kegiatan industri.

NO₂ memiliki dampak serius terhadap kesehatan manusia, seperti gangguan pernapasan, iritasi paru-paru, serta memperburuk penyakit asma dan bronkitis. Selain itu, NO₂ juga berkontribusi terhadap pembentukan hujan asam dan penurunan kualitas lingkungan secara keseluruhan.

---

# 1. Pengumpulan Data

Pertama kita akan mengumpulkan data time series harian kadar NO₂ di daerah Bangkalan. Pengumpulan data dilakukan melalui Copernicus Data Space Ecosystem.

## 1.1 Persiapan Akun

Buat akun terlebih dahulu pada:

https://dataspace.copernicus.eu/

Dokumentasi pengambilan data:

https://documentation.dataspace.copernicus.eu/notebook-samples/openeo/NO2Covid.html

Untuk menjalankan kode Python, buka:

https://dataspace.copernicus.eu/analyse/jupyterlab

Kemudian pilih **Python 3 (ipykernel)**.

## 1.2 Instalasi Library

```bash
pip install openeo
```

## 1.3 Koneksi ke OpenEO

```python
import openeo

connection = openeo.connect(
    "openeo.dataspace.copernicus.eu"
).authenticate_oidc()
```

Saat kode dijalankan akan muncul autentikasi:

```text
Visit (link authentikasi) 📋 to authenticate.
✅ Authorized successfully
Authenticated using device code flow.
```

Login menggunakan akun Copernicus yang telah dibuat.

## 1.4 Menentukan Area Pengamatan (AOI)

```python
aoi = {
    "type": "Polygon",
    "coordinates": [
        [
            [113.09, -6.89],
            [112.68, -6.89],
            [112.68, -7.20],
            [113.09, -7.20],
            [113.09, -6.89],
        ]
    ]
}
```

Area dapat dibuat menggunakan:

https://geojson.io/

Salin koordinat yang muncul pada panel kanan lalu sesuaikan dengan variabel `aoi` dan `spatial_extent`.

## 1.5 Pengambilan Data NO₂

```python
s5post = connection.load_collection(
    "SENTINEL_5P_L2",
    temporal_extent=["2023-10-01", "2025-10-01"],
    spatial_extent={
        "west": 112.68,
        "south": -7.20,
        "east": 113.09,
        "north": -6.89
    },
    bands=["NO2"],
)

s5p_no2_daily = s5post.aggregate_temporal_period(
    reducer="mean",
    period="day"
)

s5p_no2_aoi = s5p_no2_daily.aggregate_spatial(
    reducer="mean",
    geometries=aoi
)
```

## 1.6 Menjalankan Batch Job

```python
job = s5post.execute_batch(
    title="NO2 in Bangkalan",
    outputfile="NO2Bangkalan.nc"
)
```

Tunggu hingga status job berubah menjadi **finished (100%)**.

---

# 2. Preprocessing Data

## 2.1 Membaca File NetCDF

```python
import netCDF4

file_path = "data/NO2Bangkalan.nc"
ds = netCDF4.Dataset(file_path)

print(ds.variables.keys())

no2 = ds.variables["NO2"][:]
time = ds.variables["t"][:]
```

## 2.2 Mengatasi Missing Value dengan Interpolasi Linear

```python
import numpy as np
import pandas as pd

no2_filled = np.zeros_like(no2)
no2_filled = no2_filled.filled(0)

for i in range(no2.shape[1]):
    for j in range(no2.shape[2]):
        series = pd.Series(no2[:, i, j])

        no2_filled[:, i, j] = (
            series.interpolate(
                method="linear",
                limit_direction="both"
            ).to_numpy()
        )
```

## 2.3 Menghitung Rata-rata Harian

```python
new_dates = []
new_no2 = []

for i in range(len(dates)):
    new_date = dates[i].strftime("%Y-%m-%d")

    new_dates.append(new_date)
    new_no2.append(np.mean(no2_filled[i]))
```

## 2.4 Menyimpan ke CSV

```python
df = pd.DataFrame({
    "date": new_dates,
    "NO2": new_no2
})

df.to_csv(
    "NO2_Bangkalan_timeseries.csv",
    index=False
)
```

---

# 3. Pengecekan Missing Value Harian

## 3.1 Deteksi Tanggal Hilang

```python
full_range = pd.date_range(
    start="2023-10-01",
    end="2025-09-30",
    freq="D"
)

missing_dates = full_range.difference(df["date"])
```

## 3.2 Interpolasi Missing Date

```python
df = df.set_index("date").reindex(full_range)

df["NO2"] = df["NO2"].interpolate(
    method="time"
)

df["NO2"] = (
    df["NO2"]
    .bfill()
    .ffill()
)
```

---

# 4. Deteksi dan Penanganan Outlier

## 4.1 Deteksi Outlier Menggunakan IQR

```python
Q1 = df["NO2"].quantile(0.25)
Q3 = df["NO2"].quantile(0.75)

IQR = Q3 - Q1

lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR
```

## 4.2 Menghapus Outlier dan Interpolasi

```python
df["NO2_cleaned"] = df["NO2"].mask(
    (df["NO2"] < lower_bound) |
    (df["NO2"] > upper_bound)
)

df["NO2_filled"] = (
    df["NO2_cleaned"]
    .interpolate(method="linear")
    .bfill()
    .ffill()
)
```

---

# 5. Modeling Menggunakan KNN Regression

## 5.1 Normalisasi Data

```python
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()

df["NO2_scaled"] = scaler.fit_transform(
    df[["NO2"]]
)
```

## 5.2 Membentuk Data Supervised

```python
def create_supervised(
    data,
    n_lag=4
):
    ...
```

## 5.3 Uji Korelasi Lag

Menggunakan lag 1–30 hari terhadap target `NO2(t)` untuk memilih fitur terbaik.

## 5.4 Training KNN Regression

```python
from sklearn.neighbors import (
    KNeighborsRegressor
)
```

Model diuji pada:

* Lag 4 hari
* Lag 10 hari
* Lag 30 hari

Menggunakan:

* RMSE
* R² Score
* MAPE

---

# 6. Hasil Evaluasi

| Model        | RMSE     | R²      | MAPE   |
| ------------ | -------- | ------- | ------ |
| KNN (4 Lag)  | 0.065436 | 0.1395  | 61.08% |
| KNN (10 Lag) | 0.067567 | 0.0886  | 64.66% |
| KNN (30 Lag) | 0.074803 | -0.0875 | 72.23% |

---

# 7. Kesimpulan

Hasil evaluasi menunjukkan bahwa peningkatan jumlah fitur historis (lag) tidak selalu meningkatkan performa model. Model terbaik diperoleh pada penggunaan 4 hari sebelumnya dengan RMSE paling kecil dan nilai R² tertinggi dibandingkan model lainnya.

Penambahan lag hingga 10 dan 30 hari justru menurunkan performa model yang ditunjukkan oleh peningkatan RMSE dan MAPE serta penurunan nilai R². Hal ini menunjukkan bahwa model KNN Regression kurang mampu menangkap pola data NO₂ harian secara optimal dan rentan mengalami penurunan kemampuan generalisasi ketika jumlah fitur historis ditambah.

Untuk penelitian selanjutnya, model lain seperti Random Forest Regression, SVR, XGBoost, LSTM, atau GRU dapat dipertimbangkan untuk memperoleh performa prediksi yang lebih baik.
