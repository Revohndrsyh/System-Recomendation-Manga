# System Recomandatin Manga - Revo Hendriansyah

## Domain Proyek
Proyek ini membangun sistem rekomendasi manga berbasis Content-Based Filtering dan Collaborative Filtering, yang dapat memberikan rekomendasi manga paling relevan kepada pengguna berdasarkan kemiripan isi maupun pola preferensi pengguna lain.

## Latar Belakang
Manga adalah media hiburan populer dari Jepang yang kini telah mendunia, dengan ribuan judul yang terus bertambah setiap tahunnya. Banyaknya pilihan manga justru membuat pembaca kebingungan dalam menemukan manga yang benar-benar sesuai selera mereka. Oleh karena itu, sistem rekomendasi sangat penting untuk membantu pembaca menemukan manga baru yang relevan dengan minat mereka, baik berdasarkan konten cerita maupun pola perilaku pembaca lain.

## Business Understanding

### Problem Statements
1. Bagaimana membangun sistem rekomendasi manga yang dapat membantu pengguna menemukan judul manga yang sesuai dengan minat dan preferensi mereka di antara ribuan judul yang tersedia?

2. Bagaimana menerapkan dua pendekatan sistem rekomendasi, yaitu Content-Based Filtering dan Collaborative Filtering, untuk meningkatkan kualitas dan personalisasi hasil rekomendasi manga?

3. Bagaimana mengukur dan membandingkan performa kedua pendekatan sistem rekomendasi tersebut secara objektif?

### Goals
1. Mengembangkan sistem rekomendasi manga yang mampu memberikan rekomendasi Top-N manga yang relevan dan personal untuk pengguna, sehingga pengguna tidak lagi kebingungan dalam memilih judul manga yang sesuai dengan minatnya.

2. Menerapkan dan membandingkan dua pendekatan utama:
        - Content-Based Filtering: merekomendasikan manga berdasarkan kemiripan isi (genre, deskripsi, tag).
        - Collaborative Filtering: merekomendasikan manga berdasarkan pola perilaku dan preferensi pengguna lain (matrix factorization).

3. Melakukan evaluasi dan analisis terhadap performa kedua model dengan menggunakan metrik Precision@5, serta menyajikan hasil komparasi yang jelas sehingga dapat diketahui kelebihan dan kekurangan masing-masing pendekatan dalam konteks data manga yang digunakan.

### Solution
1. **Content-Based Filtering**
Sistem rekomendasi dibangun dengan memanfaatkan kemiripan konten antar manga, terutama pada fitur-fitur seperti genre, deskripsi, dan tags.
    - Metode:
        - Setiap manga direpresentasikan sebagai vektor numerik menggunakan TF-IDF dari gabungan fitur konten (combined_features).
        - Kemiripan antar manga dihitung menggunakan Cosine Similarity.
        - Rekomendasi diberikan dengan memilih manga yang paling mirip dengan manga yang disukai atau dicari pengguna.
    - Manfaat:
        - Mampu merekomendasikan manga baru meskipun belum pernah di-rating oleh pengguna lain.
        - Sangat bergantung pada kelengkapan dan kualitas data konten manga.

2. **Collaborative Filtering**
Sistem rekomendasi juga menerapkan collaborative filtering berbasis matrix factorization (SVD) pada matriks user-manga (dalam eksperimen ini menggunakan simulasi data user dummy).
    - Metode:
        - Membuat matriks interaksi user-manga dengan data rating simulasi.
        - Matrix factorization dilakukan menggunakan Truncated SVD untuk menemukan pola laten preferensi pengguna.
        - Rekomendasi diberikan berdasarkan manga yang cenderung disukai oleh pengguna lain dengan pola preferensi serupa.
    - Manfaat:
        - Dapat menemukan pola dan rekomendasi personal yang tidak secara eksplisit tampak pada fitur konten.
        - Efektif jika terdapat cukup banyak data interaksi user asli.

3. Evaluasi dan Komparasi Model
        - Setiap pendekatan dievaluasi menggunakan metrik Precision@5 untuk mengukur seberapa banyak manga relevan yang berhasil direkomendasikan di Top-5 hasil.
        - Hasil komparasi precision@5 kedua model disajikan untuk menentukan kelebihan, kekurangan, dan potensi pengembangan sistem rekomendasi di masa depan.

## Data Understanding
Dataset yang digunakan pada proyek ini merupakan kumpulan data manga berjudul [mangadex.orgManga/Manhua/Manhwa Dataset](https://www.kaggle.com/datasets/hanswang06/mangadex-manga-dataset/data), yang berisi ribuan judul manga beserta atribut penting yang dapat dimanfaatkan untuk sistem rekomendasi.

### Sumber Data
- Dataset diambil dari sumber publik [Kaggle](https://www.kaggle.com/datasets/hanswang06/mangadex-manga-dataset/data)

### Informasi Dataset
| Jenis         | Keterangan                                                                                   |  
|---------------|----------------------------------------------------------------------------------------------|
| Title         | mangadex.orgManga/Manhua/Manhwa Dataset                                           | 
| Source        | [Kaggle mangadex](https://www.kaggle.com/datasets/hanswang06/mangadex-manga-dataset/data)                                                                              |
| Maintainer    | Hans Wang                                                                                     |
| License       | the MangaDex Public API License                                                                                   | 
| Visibility    | Publik                                                                                       |
| Tags          | Anime and Manga                              |    
| Usability     | 10.00                                                                                        |

### Jumlah Baris dan Kolom
- Jumlah baris: 5.512
- Jumlah kolom : 6

### Kondisi data
Berdasarkan pemeriksaan awal dari kondisi data, beberapa hal yang perlu diperhatikan:
1. Duplikat Data: 6
2. Missing Value: 448

### Fitur Data
Dataset terdiri dari beberapa fitur yaitu:
1. name: Judul manga.
2. description: Ringkasan singkat mengenai cerita manga.
3. tags: Berisikan genre dan tema yang terkait dengan manga
4. ratings: Ratings pengguna berkisar 0-10
5. followers: Jumllah pengguna yang mengikuti manga.
6. years: Tahun penerbitan

### Explolatory Data Analysis (EDA)
**Top 10 Genre Manga**

Analisis frekuensi genre pada dataset manga menunjukkan bahwa beberapa genre memiliki jumlah manga yang jauh lebih banyak dibandingkan yang lain. Sepuluh genre paling populer di dataset ini adalah:
    1. Romance
    2. Comedy
    3. Drama
    4. Fantasy
    5. Action
    6. Slice of Life
    7. School Life
    8. Web Comic
    9. Full Color
    10. Adaptation

![image.png](https://raw.github.com/Revohndrsyh/System-Recomendation-Manga/main/Top%2010%20Genre.png)

Insight:

Genre Romance, Comedy, dan Drama mendominasi jumlah judul manga, menunjukkan bahwa genre-genre ini sangat diminati dan diproduksi lebih banyak. Hal ini juga bisa menjadi faktor penting dalam sistem rekomendasi, karena manga dengan genre populer memiliki peluang lebih tinggi untuk direkomendasikan kepada pembaca baru.


**Distribusi Rating Manga**

Distribusi rating manga pada dataset ini memperlihatkan sebagian besar manga memiliki rating tinggi di kisaran 7 hingga 9. Hanya sedikit manga yang memiliki rating sangat rendah.

![image.png](https://raw.github.com/Revohndrsyh/System-Recomendation-Manga/main/Distribusi%20Rating.png)

Insight:

Mayoritas manga mendapatkan rating yang baik dari pembaca. Hal ini menunjukkan kurasi atau penilaian komunitas yang cukup ketat, sehingga sistem rekomendasi dapat fokus pada manga dengan rating menengah ke atas untuk meningkatkan kepuasan pengguna. Distribusi ini juga mengindikasikan bahwa sistem perlu memperhatikan threshold rating agar rekomendasi tidak selalu didominasi oleh manga dengan rating sangat tinggi saja.

## Data Preparation
Tahap data preparation dilakukan untuk memastikan data siap digunakan dalam proses pemodelan dan menghasilkan sistem rekomendasi yang optimal. Berikut langkah-langkah yang dilakukan:

1. Pembersihan Teks (Text Cleaning):
    - Setiap data pada kolom name, description, dan tags dibersihkan dari spasi berlebih serta karakter spesial, sehingga hanya tersisa huruf, angka, koma, dan spasi.
    - Hal ini dilakukan agar proses ekstraksi fitur teks (seperti TF-IDF) menjadi lebih efektif dan akurat.

2. Penanganan Missing Value:
    - Kolom description dan tags yang kosong diisi dengan string kosong (''), agar tidak mengganggu proses penggabungan fitur maupun pembuatan model.
    - Kolom rating yang kosong diisi dengan nilai median rating dari seluruh data. Langkah ini bertujuan untuk mengurangi bias akibat data rating yang hilang, serta menjaga jumlah data tetap banyak.
    - Kolom year yang kosong diisi dengan 0 sebagai penanda tahun tidak diketahui.

3. Feature Engineering:
    - Tiga kolom utama (name, description, tags) digabung menjadi satu kolom baru bernama combined_features. Kolom ini digunakan sebagai fitur utama untuk model content-based filtering karena memuat seluruh informasi penting dari manga.

4. Pemeriksaan Akhir:
    - Jumlah data dan jumlah missing value per kolom diperiksa kembali setelah semua tahapan dilakukan, untuk memastikan bahwa data sudah bersih dan siap digunakan untuk analisis lebih lanjut.

## Modeling
Sistem rekomendasi manga pada proyek ini dibangun menggunakan dua pendekatan utama, yaitu Content-Based Filtering dan Collaborative Filtering. Kedua model ini diuji performanya untuk menemukan manga relevan berdasarkan genre, deskripsi, tag, serta pola preferensi pengguna.

**Content-Based Filtering**
Pada pendekatan ini, rekomendasi manga diberikan berdasarkan kemiripan konten antara manga yang dipilih user dengan manga lain di database.
Fitur utama yang digunakan adalah gabungan dari judul (name), deskripsi (description), dan tag/genre (tags) yang diproses menggunakan TF-IDF vectorizer.Kemiripan antar manga dihitung menggunakan Cosine Similarity, sehingga manga dengan genre dan deskripsi paling mirip akan direkomendasikan.

Rumus Cosine Similarity:
Cosine(A, B) = (A ⋅ B) / (||A|| * ||B||)

- Kelebihan: Efisien, bisa merekomendasikan manga baru, tidak perlu data interaksi user
- Kekurangan: Tidak mempertimbangkan pola unik user

**Collaborative Filtering**
Collaborative filtering memanfaatkan pola preferensi pengguna untuk memberikan rekomendasi.
Pada eksperimen ini, model collaborative filtering dibangun dengan simulasi matriks user-manga dan teknik matrix factorization (Truncated SVD).
Rekomendasi untuk user didasarkan pada kemiripan pola rating/feedback antar pengguna.
- Kelebihan: Mampu mempelajari preferensi komunitas, rekomendasi personal
- Kekurangan: Membutuhkan data interaksi user asli

## Evaluation
Tahap evaluasi dilakukan untuk mengukur seberapa baik sistem rekomendasi yang telah dibangun dalam memberikan manga yang relevan kepada pengguna. Evaluasi ini penting untuk memastikan bahwa solusi yang dikembangkan benar-benar menjawab permasalahan bisnis yang telah didefinisikan sebelumnya.

### Metode Evaluasi
Metrik utama yang digunakan adalah Precision@5, yaitu proporsi manga relevan yang berhasil direkomendasikan dalam 5 rekomendasi teratas (Top-5) yang diberikan sistem.
Relevansi diukur dengan dua pendekatan:

- Untuk Content-Based Filtering: manga dianggap relevan jika memiliki genre yang sama dengan manga target.
- Untuk Collaborative Filtering: manga dianggap relevan jika memiliki rating tinggi (misal, rating ≥ 8).

### Hasil Evaluasi
![image.png](https://raw.github.com/Revohndrsyh/System-Recomendation-Manga/main/Hasil%20dan%20Perbandingan%20Model.png)
- Content-Based Filtering:
Precision@5 = 1.00
Seluruh rekomendasi Top-5 manga dari model content-based berhasil tepat genre dengan manga target yang diuji. Artinya, model ini sangat efektif dalam memberikan rekomendasi berbasis konten.
- Collaborative Filtering:
Rata-rata Precision@5 = 0.48 (berdasarkan evaluasi pada 5 user dummy)
Collaborative filtering cukup baik dalam merekomendasikan manga populer (ber-rating tinggi), namun performanya masih di bawah content-based filtering pada dataset ini.

### Analisis dan Keterkaitan dengan Business Understanding
**Problem Statment**
- Problem Statement 1 “Bagaimana membantu pengguna menemukan manga sesuai preferensi?” terjawab dengan dua model rekomendasi yang mampu mengidentifikasi manga yang relevan dari ribuan judul.
- Problem Statement 2 “Bagaimana menerapkan dua pendekatan dan meningkatkan kualitas rekomendasi?” terjawab melalui penerapan content-based filtering (berbasis konten) dan collaborative filtering (berbasis perilaku).
- Problem Statement 3 “Bagaimana mengukur performa dan melakukan komparasi?” terjawab melalui evaluasi objektif dengan metrik Precision@5, sehingga performa kedua pendekatan dapat dibandingkan secara transparan.

**Goals**

- Goals 1 :  Berdasarkan evaluasi Precision@5, sistem content-based filtering mampu memberikan rekomendasi yang seluruhnya relevan (Precision@5 = 1.00), sedangkan collaborative filtering memberikan rekomendasi yang cukup relevan (rata-rata Precision@5 = 0.48 pada 5 user dummy).
- Goals 2 : Kedua pendekatan berhasil diimplementasikan dan diuji. Content-based filtering terbukti sangat efektif pada data manga yang kaya konten, sedangkan collaborative filtering memberikan personalisasi tambahan terutama jika ada data interaksi user asli.
- Goals 3 : Hasil evaluasi memperlihatkan kelebihan content-based filtering dalam menangani data baru dan cold-start, serta potensi collaborative filtering dalam memberikan rekomendasi personal. Komparasi ini menjadi dasar pengembangan sistem rekomendasi ke depannya.

### Hasil evaluasi menunjukkan:

- Content-Based Filtering sangat cocok digunakan pada data manga yang kaya informasi konten, karena mampu memberikan rekomendasi yang sangat relevan tanpa perlu data interaksi pengguna.
- Collaborative Filtering menjadi pelengkap penting untuk personalisasi yang lebih dalam, terutama jika sudah tersedia banyak data interaksi/rating pengguna asli.

Kedua model ini, jika digabungkan, dapat saling melengkapi sehingga sistem rekomendasi manga mampu memberikan pengalaman pencarian manga yang lebih akurat, personal, dan adaptif bagi pengguna—sesuai dengan tujuan utama bisnis (business goals) yang telah dirumuskan pada tahap awal proyek.

### Kesimpulan
Evaluasi dengan Precision@5 membuktikan bahwa solusi yang dibangun telah efektif dalam menyelesaikan permasalahan bisnis, dengan model content-based filtering menunjukkan performa terbaik pada dataset ini. Pengembangan lebih lanjut dapat dilakukan dengan mengintegrasikan lebih banyak data interaksi pengguna asli, sehingga collaborative filtering juga dapat memberikan kontribusi yang lebih besar dalam sistem rekomendasi.

## Refrensi
- Hans Wang. (2025). Kaggle Dataset. https://www.kaggle.com/datasets/hanswang06/mangadex-manga-dataset/data
- Cosine Similarity – GeekCulture. https://medium.com/geekculture/cosine-similarity-and-cosine-distance-48eed889a5c4
