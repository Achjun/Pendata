# tugas 2

## 1. Struktur Dataset

Dataset yang digunakan merupakan data mahasiswa dengan total:

- Jumlah observasi: **150 baris**
- Jumlah variabel: **11 kolom**
- Tidak terdapat missing value (150 non-null untuk semua variabel)

### Klasifikasi Variabel

**Variabel Numerik:**
- Usia
- Semester
- IPK
- Jumlah_Organisasi
- ID (identifier)

**Variabel Kategorikal (Nominal):**
- Jenis_Kelamin
- Program_Studi
- Status_Beasiswa
- Status_Kerja

**Variabel Ordinal:**
- Tingkat_Kepuasan  
  (Rendah < Sedang < Tinggi < Sangat Tinggi)
- Motivasi_Belajar  
  (Sangat Rendah < Rendah < Sedang < Tinggi < Sangat Tinggi)

---

## 2. Statistik Deskriptif Variabel Numerik

| Variabel            | Mean  | Min | Max |
|---------------------|-------|-----|-----|
| Usia                | 21.43 | 18  | 25  |
| Semester            | 4.33  | 1   | 8   |
| IPK                 | 2.97  | 2.00| 3.99|
| Jumlah_Organisasi   | 2.60  | 0   | 5   |

### Interpretasi:
- Rata-rata mahasiswa berada pada usia **21 tahun**
- Mayoritas berada di sekitar **semester 4**
- Rata-rata IPK sebesar **2.97**
- Mahasiswa rata-rata mengikuti **2–3 organisasi**

---

## 3. Distribusi Variabel Kategorikal

### Jenis_Kelamin
- Perempuan: 80
- Laki-laki: 70

Distribusi relatif seimbang.

### Program_Studi
- Manajemen: 45
- Sistem Informasi: 40
- Teknik Informatika: 33
- Akuntansi: 32

Distribusi program studi cukup merata.

### Status_Beasiswa
- Tidak: 78
- Ya: 72

Distribusi hampir seimbang.

### Status_Kerja
- Part Time: 62
- Tidak Bekerja: 50
- Full Time: 38

Mayoritas mahasiswa bekerja paruh waktu.

---

## 4. Distribusi Variabel Ordinal

### Tingkat_Kepuasan
- Tinggi: 45
- Rendah: 37
- Sangat Tinggi: 37
- Sedang: 31

Mayoritas mahasiswa berada pada kategori **Tinggi dan Sangat Tinggi**.

### Motivasi_Belajar
- Sangat Rendah: 33
- Tinggi: 33
- Sedang: 33
- Sangat Tinggi: 27
- Rendah: 24

Distribusi motivasi belajar relatif merata.

---

## 5. Kesimpulan Tahap Data Understanding

1. Dataset bersih dan tidak memiliki missing value.
2. Distribusi data cukup seimbang untuk analisis statistik.
3. Tidak terdapat nilai ekstrem pada variabel IPK.
4. Dataset cocok digunakan untuk:
   - Analisis regresi
   - Uji korelasi (Pearson/Spearman)
   - Uji beda (t-test / ANOVA)
   - Clustering
   - Analisis hubungan variabel ordinal