# Laporan Eksplorasi Data dan Analisis Korelasi: Dataset Titanic

Dokumen ini merangkum hasil dari analisis eksplorasi data (Exploratory Data Analysis - EDA) pada dataset Titanic. Tujuannya adalah untuk memahami karakteristik data dan menemukan korelasi antar variabel, khususnya faktor-faktor yang memengaruhi tingkat kelangsungan hidup (`survived`) penumpang.

## Tahapan Analisis Data

Analisis dilakukan melalui beberapa tahapan utama yang terdokumentasi dalam file `marco_explorasi_data_analysis_titanic.ipynb`.

### 1. Pemuatan dan Pemeriksaan Awal
- **Library yang Digunakan**: Analisis ini memanfaatkan library Python populer seperti `pandas` untuk manipulasi data, `numpy` untuk operasi numerik, serta `matplotlib` dan `seaborn` untuk visualisasi data.
- **Pemuatan Dataset**: Dataset "titanic" dimuat langsung dari library `seaborn`.
- **Statistik Deskriptif**:
  - Terdapat total **891 data penumpang** dengan **16 kolom (fitur)**.
  - Ditemukan adanya **data yang hilang (missing values)** pada kolom `age` (177 data), `deck` (688 data), dan `embarked`/`embark_town` (2 data).
  - Rata-rata tingkat kelangsungan hidup penumpang adalah sekitar **38.4%**.
  - Sebagian besar penumpang adalah laki-laki (sekitar 65%).

### 2. Modifikasi Data (Feature Engineering)
Untuk mempermudah analisis kuantitatif, dibuat satu kolom baru:
- `gender_num`: Kolom ini mengubah data kategorikal `sex` menjadi numerik, di mana `male` dipetakan sebagai `1` dan `female` sebagai `0`.

## Analisis Visual dan Korelasi Antar Variabel

Visualisasi data adalah kunci untuk menemukan pola dan hubungan antar variabel. Berikut adalah temuan-temuan utama dari analisis visual:

### a. Korelasi Antara Kelas Penumpang dan Tingkat Kelangsungan Hidup

![Tingkat Kelangsungan Hidup berdasarkan Kelas Penumpang di Titanic](https://i.imgur.com/your-image-url1.png)

Grafik batang di atas menunjukkan korelasi negatif yang sangat kuat antara kelas penumpang (`pclass`) dan tingkat kelangsungan hidup (`survived`).
- **Temuan**:
  - **Kelas 1**: Memiliki tingkat kelangsungan hidup tertinggi (lebih dari 60%).
  - **Kelas 2**: Tingkat kelangsungan hidup sekitar 47%.
  - **Kelas 3**: Tingkat kelangsungan hidup paling rendah (di bawah 25%).
- **Kesimpulan**: Semakin tinggi kelas sosial (diwakili oleh `pclass` yang lebih rendah), semakin besar peluang penumpang untuk selamat. Ini adalah salah satu prediktor keselamatan terkuat.

### b. Korelasi Antara Jenis Kelamin dan Tingkat Kelangsungan Hidup

![Tingkat Kelangsungan Hidup berdasarkan Jenis Kelamin di Titanic](https://i.imgur.com/your-image-url2.png)

Ini adalah faktor dengan korelasi paling signifikan terhadap tingkat kelangsungan hidup.
- **Temuan**:
  - **Perempuan (`female`)**: Memiliki tingkat kelangsungan hidup hampir **75%**.
  - **Laki-laki (`male`)**: Tingkat kelangsungan hidup hanya sekitar **19%**.
- **Kesimpulan**: Terdapat korelasi yang sangat kuat antara jenis kelamin dan keselamatan. Sesuai dengan protokol "wanita dan anak-anak terlebih dahulu," penumpang perempuan memiliki probabilitas selamat yang jauh lebih tinggi.

### c. Korelasi Antara Kelas Penumpang dan Tarif (Fare)

Grafik boxplot menunjukkan hubungan langsung antara kelas penumpang dan tarif yang dibayarkan.
- **Temuan**:
  - Penumpang **Kelas 1** membayar tarif yang jauh lebih tinggi dan memiliki rentang harga yang sangat lebar.
  - Tarif untuk **Kelas 2** dan **Kelas 3** jauh lebih rendah dan lebih terkonsentrasi di nilai yang kecil.
- **Kesimpulan**: Kolom `pclass` adalah proksi yang baik untuk status ekonomi penumpang, yang berkorelasi kuat dengan `fare`.

### d. Korelasi Antara Status Perjalanan dan Kelangsungan Hidup

Analisis membandingkan penumpang yang bepergian sendiri (`alone`) dengan yang bersama keluarga (`sibsp` atau `parch` > 0).
- **Temuan**: Penumpang yang **bersama keluarga** memiliki tingkat kelangsungan hidup yang sedikit lebih tinggi (sekitar 50%) dibandingkan dengan mereka yang **bepergian sendiri** (sekitar 30%).
- **Kesimpulan**: Bepergian dengan anggota keluarga tampaknya memberikan sedikit keuntungan untuk bertahan hidup.

### e. Distribusi Umur dan Hubungannya dengan Faktor Lain

- **Distribusi Umur**: Sebagian besar penumpang berada di rentang usia dewasa muda (20-40 tahun). Terdapat juga jumlah anak-anak yang cukup signifikan.
- **Hubungan Umur, Tarif, dan Keselamatan**: Grafik sebar (scatterplot) menunjukkan bahwa:
  - Penumpang yang membayar **tarif lebih tinggi** (umumnya Kelas 1) memiliki peluang selamat lebih besar, terlepas dari usianya.
  - **Anak-anak** (usia muda) juga menunjukkan tingkat kelangsungan hidup yang relatif lebih tinggi dibandingkan dewasa pada kelas yang sama.

## Kesimpulan Utama

Berdasarkan eksplorasi data, faktor-faktor yang paling kuat berkorelasi dengan tingkat kelangsungan hidup penumpang Titanic adalah:
1.  **Jenis Kelamin**: Menjadi faktor prediktor terkuat. Wanita jauh lebih mungkin selamat.
2.  **Kelas Penumpang (Status Sosial-Ekonomi)**: Penumpang di kelas yang lebih tinggi memiliki peluang selamat yang jauh lebih besar.
3.  **Status Perjalanan**: Bepergian dengan keluarga sedikit meningkatkan peluang selamat.
4.  **Umur**: Menjadi seorang anak memberikan keuntungan dalam bertahan hidup.

Analisis ini memberikan gambaran jelas mengenai hierarki sosial yang berlaku selama evakuasi kapal Titanic, di mana prioritas keselamatan diberikan kepada wanita, anak-anak, dan penumpang kelas atas.
