# Laporan Proyek Machine Learning - Sistem Rekomendasi Musik
Oleh: Yuliana Habibah
## Project Overview

Di era digital saat ini, industri musik semakin berkembang dengan pesat. Platform streaming musik seperti Spotify, Apple Music, dan YouTube Music memanfaatkan sistem rekomendasi untuk meningkatkan pengalaman pengguna. Sistem rekomendasi musik membantu pengguna menemukan lagu-lagu baru yang sesuai dengan preferensi mereka, meningkatkan engagement, dan memperpanjang waktu penggunaan aplikasi.

Proyek ini bertujuan untuk membangun sistem rekomendasi musik berbasis Collaborative Filtering dengan Neural Network untuk memprediksi tingkat popularity suatu lagu berdasarkan interaksi pengguna.



## Business Understanding

### Problem Statements
Berdasarkan latar belakang di atas, berikut ini merupakan rincian masalah yang dapat diselesaikan pada proyek ini:
Bagaimana cara memberikan rekomendasi lagu yang sesuai dengan preferensi pengguna berdasarkan data interaksi sebelumnya?


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

(gambar)


## Visualisasi Data
Distribusi Popularity

Mayoritas lagu memiliki popularity 30-60.

Lagu dengan popularity tinggi (>80) sangat jarang.

(gambar)

Analisis Fitur Audio

Lagu viral cenderung memiliki energy tinggi dan valence positif.

(gambar)

## Data Preparation
Langkah-langkah:
Handling Missing Values

Mengisi missing values pada kolom teks (artists, album_name) dengan modus.

Outlier Treatment (Winsorization)

Mengganti outlier dengan batas IQR untuk menjaga distribusi data.

Encoding track_id

Mengubah track_id menjadi indeks numerik.

Normalisasi popularity

Mengubah skala popularity dari 0-100 → 0-1.

Train-Test Split (80:20)

80% data training, 20% validasi.

## Modeling
Embedding Layer: Mempelajari representasi lagu dalam 64 dimensi.

Dense Layer: 32 neuron dengan aktivasi ReLU.

Output: Sigmoid (prediksi 0-1).

Pelatihan Model
Optimizer: Adam (lr=0.001)

Loss: Binary Crossentropy

Metrics: RMSE, MAE

Early Stopping: Berhenti jika tidak ada improvement dalam 3 epoch.

## Evaluation
Hasil Evaluasi
RMSE: 0.185 (semakin mendekati 0 semakin baik)

Loss:

Training: 0.15

Validation: 0.18
Contoh Rekomendasi
Input: track_id = "30kaQow1m0y1G2UcNTTSYk"
## Kesimpulan
- Model berhasil memprediksi popularity lagu dengan RMSE 0.185.

- Sistem rekomendasi dapat memberikan 10 lagu terbaik berdasarkan preferensi pengguna.

- Cold-start problem masih menjadi tantangan (perlu pendekatan hybrid dengan Content-Based Filtering).

## Saran Pengembangan:

Gabungkan dengan Content-Based Filtering untuk rekomendasi pengguna baru.

Gunakan Deep Learning (RNN/Transformer) untuk analisis pola waktu.
## Referensi

[[1](https://developers.google.com/machine-learning/recommendation/collaborative/basics)]  

