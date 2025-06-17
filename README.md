# Laporan Proyek Machine Learning - Sistem Rekomendasi Musik
Oleh: Yuliana Habibah
## Project Overview

Industri musik digital telah mengalami transformasi signifikan dengan munculnya platform streaming seperti Spotify, Apple Music, dan Deezer. Menurut Laporan Industri Musik Global IFPI (2023), pendapatan streaming musik mencapai $17.5 miliar pada tahun 2022, mencakup 67% total pendapatan industri. Tantangan utama dalam platform ini adalah membantu pengguna menemukan lagu yang relevan dari katalog yang sering melebihi 100 juta track.

Sistem rekomendasi yang efektif dapat meningkatkan engagement pengguna sebesar 30% (Spotify Engineering, 2021) dan mengurangi churn rate hingga 25%. Tanpa rekomendasi yang personal, pengguna menghabiskan 40% lebih banyak waktu untuk mencari konten (McKinsey, 2022).

## Business Understanding

### Problem Statements
Berdasarkan latar belakang di atas, berikut ini merupakan rincian masalah yang dapat diselesaikan pada proyek ini:
- Bagaimana cara memberikan rekomendasi lagu yang sesuai dengan preferensi pengguna berdasarkan data interaksi sebelumnya?


### Goals
Tujuan dari proyek ini adalah:
- Membangun model Collaborative Filtering yang dapat memprediksi popularity lagu berdasarkan preferensi pengguna.

### Solution Statement
Metode:

Collaborative Filtering dengan Neural Network

- Menggunakan embedding layers untuk mempelajari pola preferensi pengguna.

- Memprediksi rating popularity lagu dalam skala 0-1 (dinormalisasi).

**Kelebihan** :  
- Tidak memerlukan fitur tambahan (hanya memanfaatkan data interaksi).
- Dapat menemukan pola tersembunyi antar-lagu.

**Kekurangan** : 
- Tidak bisa memberikan rekomendasi untuk pengguna baru (cold-start problem).
- Membutuhkan data rating yang cukup banyak.

## Data Understanding

Informasi Dataset:

### Deskripsi Kolom Dataset Musik

| No | Nama Kolom          | Deskripsi                                                                                     |
|----|---------------------|-----------------------------------------------------------------------------------------------|
| 1  | Unnamed: 0         | Kolom indeks otomatis (biasanya dapat diabaikan)                                              |
| 2  | track_id           | ID unik untuk setiap lagu dalam platform                                                      |
| 3  | artists            | Nama artis atau grup musik (terdapat 1 missing value)                                         |
| 4  | album_name         | Judul album tempat lagu dirilis (terdapat 1 missing value)                                    |
| 5  | track_name         | Judul lagu (terdapat 1 missing value)                                                         |
| 6  | popularity         | Skor popularitas lagu berdasarkan interaksi pengguna (0-100)                                  |
| 7  | duration_ms        | Durasi lagu dalam milidetik                                                                   |
| 8  | explicit           | Flag apakah lagu mengandung konten eksplisit (True/False)                                     |
| 9  | danceability       | Indeks kesesuaian lagu untuk menari (0.0-1.0)                                                |
| 10 | energy             | Intensitas energi lagu (0.0-1.0)                                                             |
| 11 | key                | Pitch nada dasar lagu (0-11, sesuai Circle of Fifths)                                        |
| 12 | loudness           | Volume rata-rata lagu dalam desibel (dB)                                                     |
| 13 | mode               | Modus musik (0 = minor, 1 = mayor)                                                           |
| 14 | speechiness        | Proporsi konten vokal yang mirip ucapan seperti rap (0.0-1.0)                                 |
| 15 | acousticness       | Probabilitas lagu dihasilkan tanpa efek elektronik (0.0-1.0)                                 |
| 16 | instrumentalness   | Prediksi ketiadaan vokal (0.0 = vokal dominan, 1.0 = instrumental murni)                     |
| 17 | liveness           | Deteksi audiens dalam rekaman (0.0 = studio, 1.0 = live)                                      |
| 18 | valence            | Positivitas emosional lagu (0.0 = negatif/sedih, 1.0 = positif/senang)                       |
| 19 | tempo              | Kecepatan lagu dalam BPM (beats per minute)                                                  |
| 20 | time_signature     | Jumlah ketukan per birama (misal 3 = 3/4, 4 = 4/4)                                           |
| 21 | track_genre        | Genre utama lagu                                                                              |

## Visualisasi Data
Distribusi Popularity
![Cuplikan layar 2025-06-17 172838](https://github.com/user-attachments/assets/cd98102c-4408-466f-a3ab-def61b31c7d0)

- Mayoritas lagu memiliki popularity 30-60.

- Lagu dengan popularity tinggi (>80) sangat jarang.

### Analisis Fitur Audio
![Cuplikan layar 2025-06-17 173020](https://github.com/user-attachments/assets/75079a5b-51d6-43f4-8e02-553d83e34431)

Analisis Fitur Audio

- Lagu viral cenderung memiliki energy tinggi dan valence positif.

![Cuplikan layar 2025-06-17 173453](https://github.com/user-attachments/assets/d285af93-d5bf-495e-9abe-bd1a11440fa9)

## Data Preparation
Langkah-langkah:
1.  Handling Missing Values
![Cuplikan layar 2025-06-17 174422](https://github.com/user-attachments/assets/7887bbbe-29ca-4eb6-92b8-e04dea0fc0a8)

  => Mengisi missing values pada kolom teks (artists, album_name) dengan modus.

2.  Outlier Treatment (Winsorization)

![Cuplikan layar 2025-06-17 174832](https://github.com/user-attachments/assets/96607f78-137f-4568-a16a-bc8a7da61b19)
![Cuplikan layar 2025-06-17 174932](https://github.com/user-attachments/assets/59ab57db-173d-496c-a4db-f351d9aa4ead)
![Cuplikan layar 2025-06-17 175047](https://github.com/user-attachments/assets/93ff2348-daec-4d07-ba13-74063edb5fa1)
![Cuplikan layar 2025-06-17 175144](https://github.com/user-attachments/assets/9966b9b1-948e-49ee-8077-1fe2cdc09da5)
![Cuplikan layar 2025-06-17 175222](https://github.com/user-attachments/assets/15c8a413-b40b-4dd3-ae4f-93e12231a939)
![Cuplikan layar 2025-06-17 175309](https://github.com/user-attachments/assets/6c492ffc-23bb-4367-8f3d-7230964e83df)
![Cuplikan layar 2025-06-17 175353](https://github.com/user-attachments/assets/cc3bc0ad-9ef2-4fda-8349-1655a6f4067f)
![Cuplikan layar 2025-06-17 175452](https://github.com/user-attachments/assets/61566366-a34a-4247-a785-404e2e0e61e7)

🔧 Penanganan Outlier dengan Winsorization
Outlier yang terdeteksi tidak langsung dihapus, melainkan ditangani menggunakan metode Winsorization. Berbeda dari pendekatan trimming yang membuang data ekstrem, Winsorization mempertahankan jumlah data dengan cara membatasi nilai-nilai ekstrem ke batas tertentu.

📊 Dasar Perhitungan: Interquartile Range (IQR)
Winsorization dilakukan berdasarkan rentang antar-kuartil (IQR), dengan langkah berikut:

Q1 (Kuartil 1): Persentil ke-25
Q3 (Kuartil 3): Persentil ke-75
IQR = Q3 - Q1
Nilai batas bawah dan atas ditentukan dengan rumus:

Lower Bound = Q1 - 1.5 × IQR
Upper Bound = Q3 + 1.5 × IQR
Nilai di bawah batas bawah akan digantikan oleh batas bawah, dan sebaliknya untuk nilai di atas batas atas.

🎯 Tujuan Penggunaan Winsorization
- Menekan efek ekstrem dari outlier tanpa mengurangi jumlah data.
- Menjaga distribusi data tetap utuh dan representatif.
- Meningkatkan stabilitas dan akurasi model, terutama dalam regresi.
- Metode ini sangat berguna saat data mengandung outlier, namun tetap ingin mempertahankan keseluruhan observasi dibandingkan harus menghapusnya secara permanen.
- Mengganti outlier dengan batas IQR untuk menjaga distribusi data.
3. Encoding track_id
- **Tujuan**: Mengubah ID string menjadi representasi numerik untuk pemrosesan model
- **Metode**:
  ```python
  track_to_idx = {track_id: idx for idx, track_id in enumerate(df['track_id'].unique())}
  df['track_idx'] = df['track_id'].map(track_to_idx)
Hasil: Setiap track_id unik memiliki indeks integer (0 hingga N-1)

5. Normalisasi popularity

Normalisasi nilai popularity dari skala 0-100 ke 0-1
df['popularity_norm'] = df['popularity'] / 100.0

Alasan:

Mengubah skala [0,100] → [0,1] untuk konsistensi dengan output sigmoid

Mempercepat konvergensi selama training
   Mengubah skala popularity dari 0-100 → 0-1.

7. Train-Test Split (80:20)

Strategi: Stratified sampling berdasarkan popularity

Implementasi:

from sklearn.model_selection import train_test_split
train_df, test_df = train_test_split(df, test_size=0.2, stratify=df['popularity_bin'], random_state=42)

Keuntungan:

- Mempertahankan distribusi popularity di kedua subset

- Mencegah kebocoran data (data shuffling sebelum split)

## Modeling
1. Embedding Layer: Mempelajari representasi lagu dalam 64 dimensi.
Layer ini mengubah ID lagu dan pengguna menjadi representasi vektor padat dalam ruang 64 dimensi. Vektor ini menangkap hubungan tersembunyi antar item, seperti kesamaan genre atau preferensi pengguna, sehingga lagu dengan karakteristik mirip memiliki embedding yang serupa.
2. Dense Layer: 32 neuron dengan aktivasi ReLU.
Layer ini memproses vektor dari embedding untuk mempelajari pola non-linear dalam preferensi musik. Aktivasi ReLU (Rectified Linear Unit) membantu mempercepat pelatihan dan mencegah masalah gradient yang terlalu kecil, dengan mempertahankan hanya nilai positif dari input.
3. Output: Sigmoid (prediksi 0-1).
Layer terakhir menggunakan aktivasi sigmoid untuk mengubah output menjadi nilai antara 0 dan 1, yang dapat diinterpretasikan sebagai probabilitas lagu disukai pengguna. Sigmoid cocok untuk prediksi biner (suka/tidak suka) dan memastikan output berada dalam rentang yang terdefinisi dengan baik.

### Pelatihan Model

Berikut penjelasan singkat dan padat untuk komponen pelatihan model Anda:

**Optimizer: Adam (learning rate=0.001)**
- *Fungsi*: Algoritma adaptif untuk update bobot model selama training
- *Keunggulan*:
  - Menggabungkan momentum (mempercepat konvergensi)
  - Learning rate otomatis menyesuaikan per parameter
  - Stabil untuk berbagai jenis arsitektur neural network
- *Learning rate 0.001*: Nilai default yang baik untuk sebagian besar kasus (tidak terlalu besar/kecil)

**Loss Function: Binary Crossentropy**
- *Kegunaan*: Mengukur kesalahan prediksi probabilitas biner (0-1)
- *Formula*: `−(y_true * log(y_pred) + (1−y_true) * log(1−y_pred))`
- *Alasan Dipilih*: Cocok untuk output sigmoid yang memprediksi popularity score ternormalisasi

**Metrics: RMSE & MAE**
- **RMSE (Root Mean Squared Error)**:
  - Mengukur rata-rata selisih kuadrat prediksi vs aktual
  - Lebih sensitif terhadap outlier dibanding MAE
  - Satuan sama dengan variabel target (popularity 0-1)
  
- **MAE (Mean Absolute Error)**:
  - Mengukur rata-rata selisih absolut
  - Lebih robust terhadap outlier
  - Interpretasi lebih intuitif

*Contoh*:  
Jika RMSE=0.18 dan MAE=0.12, artinya:
- Rata-rata kesalahan prediksi ≈ 0.12 (12% skala popularity)
- Kesalahan terbesar (RMSE) ≈ 18%

Early Stopping: Berhenti jika tidak ada improvement dalam 3 epoch.

## Evaluation
Hasil Evaluasi
RMSE: 0.185 (semakin mendekati 0 semakin baik)
![Cuplikan layar 2025-06-17 185126](https://github.com/user-attachments/assets/8014ff75-4345-4d06-8563-0ceee30c20bf)

Loss:
![Cuplikan layar 2025-06-17 185216](https://github.com/user-attachments/assets/5428b491-1c58-4bd0-9f7c-587cf1bd4a27)

Training: 0.15
**Visualisasi performa model menggunakan RMSE dan loss memberikan gambaran jelas tentang efektivitas pelatihan.** RMSE (Root Mean Squared Error) mengukur akurasi prediksi dalam skala asli popularity (0-1), dihitung dengan merata-ratakan kuadrat selisih prediksi dan nilai sebenarnya. Nilai RMSE yang semakin kecil menunjukkan performa model semakin baik, dengan nilai 0 berarti prediksi sempurna. Misalnya, RMSE 0.18 berarti rata-rata kesalahan prediksi sekitar 18% dari skala popularity. Sementara itu, binary crossentropy loss mengevaluasi seberapa baik model belajar memprediksi probabilitas, dengan rumus yang menghitung ketidaksesuaian antara distribusi prediksi dan nilai aktual. Loss yang menurun selama pelatihan menunjukkan model semakin memahami pola data, sedangkan loss yang stagnan atau naik bisa mengindikasikan masalah seperti overfitting atau learning rate yang tidak optimal. Grafik yang ideal akan menunjukkan tren penurunan bersamaan untuk kedua metrik ini pada data training dan validasi, mengindikasikan model yang konvergen dengan baik.**
Validation: 0.18

### Fungsi rekomendasi:

1. Menerima track_id sebagai input
2. Mengembalikan 10 rekomendasi teratas
3. Proses:
- Encode track_id
- Prediksi popularity untuk semua track
- Urutkan berdasarkan prediksi
- Kembalikan track_id dengan prediksi tertinggi
4. Mengkonversi kembali nilai normalisasi ke skala asli

### Contoh Rekomendasi
Input: track_id = "30kaQow1m0y1G2UcNTTSYk"
![Cuplikan layar 2025-06-17 185752](https://github.com/user-attachments/assets/6b484255-d23f-4897-a675-0a0d45487188)

hasil : Sistem telah memberikan 10 rekomendasi lagu yang dinilai memiliki kemiripan dengan lagu input (30kaQow1m0y1G2UcNTTSYk). Semua lagu yang direkomendasikan memiliki prediksi popularitas yang sama (35.42), yang bisa jadi merupakan hasil dari model regresi prediktif yang dibuat (misalnya menggunakan neural network) berdasarkan fitur-fitur seperti danceability, energy, valence, dsb.
## Kesimpulan
- Model berhasil memprediksi popularity lagu dengan RMSE 0.185.

- Sistem rekomendasi dapat memberikan 10 lagu terbaik berdasarkan preferensi pengguna.

- Cold-start problem masih menjadi tantangan (perlu pendekatan hybrid dengan Content-Based Filtering).

## Saran Pengembangan:

Gabungkan dengan Content-Based Filtering untuk rekomendasi pengguna baru.

Gunakan Deep Learning (RNN/Transformer) untuk analisis pola waktu.
## Referensi

[[1](https://developers.google.com/machine-learning/recommendation/collaborative/basics)]  

