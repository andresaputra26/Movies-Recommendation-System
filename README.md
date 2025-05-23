# Laporan Proyek Machine Learning
## Movies Recommendation System
Nama     : Andre Saputra Ginting

Username : andresaputra26

Email    : andresaputra260604@gmail.com

## Project Overview
Pertumbuhan industri perfilman, baik di tingkat internasional maupun nasional, menunjukkan perkembangan yang sangat menjanjikan. Hal ini tercermin dari peningkatan jumlah penonton bioskop yang terus bertambah setiap tahunnya. Pada tahun 2018, jumlah penonton bioskop di Indonesia telah melampaui 50 juta orang, dengan hampir 200 judul film dari produksi dalam dan luar negeri yang telah diputar di seluruh wilayah Indonesia (Prasetyo & Nugroho, 2022). Dalam industri perfilman, pengelompokan penonton dilakukan melalui kategori tertentu seperti klasifikasi usia dan pemilihan genre pada setiap film yang diproduksi. Oleh karena itu, diperlukan sistem rekomendasi yang mampu membantu penonton dalam menentukan genre film yang sesuai dengan preferensi serta batasan usia mereka (Nababan & Trisna, 2021).

## Business Understanding
### Problem Statements
- Meningkatnya jumlah film yang tersedia di berbagai platform membuat pengguna kesulitan dalam memilih film yang sesuai dengan preferensi mereka.
- Setiap pengguna memiliki minat dan kebiasaan menonton yang berbeda, namun sistem konvensional belum mampu memberikan rekomendasi yang bersifat personal.
- Kurangnya sistem yang dapat menghubungkan minat pengguna dengan kategori film seperti genre atau penilaian dari pengguna lain menyebabkan rekomendasi yang kurang relevan.
- Pengguna sering membuang waktu untuk menelusuri banyak pilihan film sebelum menemukan yang sesuai, sehingga mengurangi kepuasan terhadap layanan hiburan.

### Goals
- Mengembangkan sistem rekomendasi film yang mampu memberikan saran film berdasarkan preferensi dan riwayat pengguna secara otomatis.
- Menyediakan rekomendasi yang relevan dan personal dengan mempertimbangkan genre film, penilaian pengguna, dan pola perilaku menonton.
- Meningkatkan efisiensi dalam proses pemilihan film, sehingga pengguna dapat dengan mudah menemukan film yang sesuai dengan selera mereka.
- Memberikan pengalaman menonton yang lebih baik dan mendukung penyedia layanan dalam menargetkan konten secara lebih tepat sasaran.

### Solution Statements
* ✅ **Content-Based Filtering**

  * Merekomendasikan film berdasarkan kesamaan konten seperti genre atau kata kunci film.
  * Menggunakan teknik seperti TF-IDF dan cosine similarity untuk mengukur kemiripan antar film.
  * Cocok untuk pengguna baru karena tidak membutuhkan data pengguna lain.

* ✅ **Collaborative Filtering**

  * Memberikan rekomendasi berdasarkan kesamaan perilaku antar pengguna.
  * Menggunakan data rating untuk mengenali pola kesukaan antar pengguna.
  * Efektif untuk menghasilkan rekomendasi personal berdasarkan interaksi pengguna dengan film.
 
## Data Understanding
🎬 Deskripsi Dataset Sistem Rekomendasi Film

Pada project ini digunakan dataset mengenai film yang berasal dari platform kaggle dengan judul ***Movies & Ratings for Recommendation System*** dengan Link dataset sebagai berikut [Movies & Ratings for Recommendation System](https://www.kaggle.com/datasets/nicoletacilibiu/movies-and-ratings-for-recommendation-system). Dataset ini terdiri dari dua file utama dalam format CSV, yaitu movies.csv dan ratings.csv.

Proyek ini menggunakan dua file utama dalam bentuk CSV: movies.csv dan ratings.csv. Berikut adalah penjelasan struktur kolom pada masing-masing file:
### 1. `movies.csv`
File `movies.csv` dalam sistem rekomendasi film umumnya menyimpan **informasi metadata tentang film**.

### 📄 **Isi Data `movies.csv`:**

| No. | Nama Kolom | Deskripsi                                                             | Tipe Data |
| --- | ---------- | --------------------------------------------------------------------- | --------- |
| 1   | `movieId`  | ID unik untuk setiap film. Digunakan sebagai identifikasi utama film. | `int64`   |
| 2   | `title`    | Judul lengkap dari film, termasuk tahun rilis dalam tanda kurung.     | `object`  | 
| 3   | `genres`   | Kategori atau jenis film                                              | `object`  | 

### 2. `ratings.csv`
File `ratings.csv` menyimpan **data penilaian (rating)** yang diberikan oleh **pengguna** terhadap film dalam sistem rekomendasi.

### 📄 **Isi Data `ratings.csv`:**

| No. | Nama Kolom  | Deskripsi                                                                                                 | Tipe Data |
| --- | ----------- | --------------------------------------------------------------------------------------------------------- | --------- |
| 1   | `userId`    | ID unik untuk setiap pengguna. Digunakan untuk mengidentifikasi pemberi rating.                           | `int64`   |
| 2   | `movieId`   | ID unik untuk setiap film. Berelasi dengan kolom `movieId` pada `movies.csv`.                             | `int64`   |
| 3   | `rating`    | Nilai penilaian yang diberikan oleh pengguna terhadap film, dalam skala (biasanya 0.5 hingga 5.0).        | `float64` |
| 4   | `timestamp` | Waktu saat rating diberikan, dalam format UNIX timestamp. Dapat diubah ke format tanggal jika diperlukan. | `int64`   |

File `movies.csv` dan `ratings.csv` saling terhubung melalui kolom `movieId`, yang memungkinkan sistem rekomendasi untuk menggabungkan data metadata film dengan interaksi pengguna. Melalui hubungan ini, sistem dapat menganalisis preferensi pengguna berdasarkan rating yang diberikan terhadap film tertentu dan menggunakan informasi genre dari `movies.csv` untuk memberikan rekomendasi yang relevan dan personal. Keterkaitan ini menjadi dasar dalam penerapan metode seperti content-based filtering maupun collaborative filtering dalam sistem rekomendasi film.

## Data Preparation
### 1. Merge Data `movies` dan `ratings`
Menggabungkan dua dataset utama (`movies.csv` dan `ratings.csv`) ke dalam satu DataFrame gabungan dilakukan dengan menggunakan relasi berdasarkan kolom `movieId`, yang merupakan kunci primer pada `movies.csv` dan kunci asing pada `ratings.csv`. Proses ini bertujuan untuk menyatukan informasi deskriptif mengenai film (seperti judul dan genre) dengan data interaksi pengguna (seperti `userId` dan `rating`). Dengan penggabungan ini, setiap baris dalam DataFrame akhir akan merepresentasikan satu instance rating yang mencakup siapa pengguna yang memberi rating, berapa nilai rating-nya, serta metadata film yang dinilai. Hal ini sangat penting dalam membangun sistem rekomendasi karena memungkinkan proses analisis preferensi pengguna dan pemodelan machine learning dilakukan secara lebih efisien dan komprehensif dalam satu struktur data yang utuh.

<br>
<image src='images/barchart_cat.png' width= 500/>
<br>

### 2. Menghapus kolom `timestamp`
Menghapus kolom `timestamp` karena tidak digunakan dalam membuat sistem rekomendasi.

<br>
<image src='images/barchart_cat.png' width= 500/>
<br>

### 3. Mengatasi Missing Values
Menghapus baris data yang memiliki nilai kosong (missing values) pada kolom penting seperti `userId` dan `rating`, yang masing-masing memiliki 18 nilai kosong. Nilai yang hilang pada kolom ini dapat memengaruhi kualitas sistem rekomendasi karena berisi informasi utama tentang pengguna dan preferensinya. Dengan menghapus total 18 baris yang mengandung missing values, data menjadi lebih bersih dan valid untuk dianalisis atau digunakan dalam pelatihan model rekomendasi.

<br>
<image src='images/barchart_cat.png' width= 500/>
<br>

### 4. Mengatasi data duplikat
Terlihat tidak ada data duplikat.

<br>
<image src='images/barchart_cat.png' width= 500/>
<br>

### 5. Menghapus Simbol pada kolom `title` dan `genres`
Menghapus simbol tanda kurung pada tahun yang terdapat di kolom `title` dengan mengganti pola teks seperti `(2023)` menjadi hanya `2023`, serta mengubah isi kolom `genres` yang awalnya berupa string dengan genre yang dipisahkan oleh tanda `|` menjadi list atau array genre terpisah, sehingga memudahkan pengolahan data genre secara individual.

<br>
<image src='images/barchart_cat.png' width= 500/>
<br>

### 6. Menghapus data pada kolom `title` yang tidak memiliki genre
Menghapus baris-baris pada DataFrame `df_merge` yang kolom `genres`-nya mengandung nilai `'(no genres listed)'`. Dengan menggunakan fungsi `apply` dan `lambda`, setiap baris dicek apakah genre tersebut tidak mengandung string tersebut, sehingga hanya data dengan genre yang valid yang disimpan. Setelah proses penghapusan, kode mencetak jumlah baris yang tersisa dan menampilkan beberapa baris pertama dari DataFrame hasil pembersihan tersebut.

<br>
<image src='images/barchart_cat.png' width= 500/>
<br>

## Content Based Filtering

### 1. Memilih Fitur yang digunakan untuk melakukan modeling dengan Content Based Filtering
Menggunakan fitur `movieId`, `title`, dan `genres` sebagai input utama untuk metode Content Based Filtering. Fitur `title` dan `genres` digunakan untuk merepresentasikan konten film, sehingga sistem dapat memberikan rekomendasi berdasarkan kesamaan isi atau kategori film, sedangkan `movieId` berfungsi sebagai identitas unik setiap film dalam proses pemodelan dan evaluasi.

### 2. Penghapusan Data Duplikat Berdasarkan Judul dan Genre
Mengubah kembali daftar genre pada kolom `genres` menjadi string yang dipisahkan dengan tanda `|` untuk memudahkan proses pengecekan duplikat. Selanjutnya, data diduplikasi dihapus berdasarkan kombinasi kolom `title` dan string genre tersebut agar setiap judul dengan genre unik hanya muncul sekali. Setelah itu, kolom sementara `genres_str` yang digunakan untuk pengecekan duplikat dihapus agar data kembali bersih. Terakhir, kode mencetak jumlah baris yang tersisa setelah penghapusan duplikat dan menampilkan beberapa baris pertama dari dataset hasil pembersihan.

### 3. TF-IDF Vectorizer
Pada tahap ini, daftar genre diubah menjadi string agar bisa diproses oleh `TfidfVectorizer`, yang kemudian mengubah genre menjadi representasi numerik berbobot TF-IDF dan membuat kolom baru yaitu `genres_string`. Representasi ini digunakan untuk mengukur kemiripan film berdasarkan genre dalam Content Based Filtering.

### 4. Menghapus kolom `genres`
Karena sudah mempunyai kolom `genres_string` yang sudak dilakukan proses pengubahan menjadi string, jadi kolom `genres` sudah tidak diperlukan lagi.

### 5. Cosine Similarity
Pada tahap ini, dilakukan perhitungan *cosine similarity* terhadap matriks TF-IDF untuk mengukur tingkat kemiripan antar film berdasarkan genre. Nilai cosine similarity menunjukkan seberapa mirip dua film, dengan rentang nilai antara 0 (tidak mirip) hingga 1 (sangat mirip), dan hasilnya digunakan sebagai dasar dalam memberikan rekomendasi film yang kontennya paling serupa.

### 6. Tahap Rekomendasi Film
Memberikan rekomendasi film berdasarkan kemiripan konten (genre) menggunakan nilai *cosine similarity*. Fungsi menerima judul film (`movie_title`) sebagai input dan mencari film lain yang paling mirip berdasarkan matriks kesamaan (`similarity_data`). Dengan memanfaatkan `argpartition`, fungsi mengekstrak indeks film dengan nilai kemiripan tertinggi (k film teratas) secara efisien. Film yang sama dengan input akan dihapus dari hasil rekomendasi agar tidak direkomendasikan ulang. Hasil akhirnya adalah DataFrame berisi daftar film yang paling mirip, berdasarkan genre, sebanyak `k` rekomendasi teratas.

### 7. Pengujian sistem Content Based Filtering
Tahap ini merupakan proses pengujian sistem Content Based Filtering, di mana pengguna memasukkan judul film `'Clueless 1995'` untuk mencari rekomendasi. Sistem terlebih dahulu memastikan bahwa film tersebut ada di dalam dataset dan memiliki genre `Comedy Romance`. Selanjutnya, fungsi `movie_recommendations` digunakan untuk menghitung kemiripan antara film tersebut dan film lainnya berdasarkan genre menggunakan representasi TF-IDF dan cosine similarity. Hasilnya adalah daftar 10 film dengan genre paling mirip yang direkomendasikan kepada pengguna, menunjukkan bahwa sistem mampu memberikan rekomendasi yang relevan berdasarkan konten film.

## Collaborative Filtering

### 1. Memilih Fitur yang digunakan untuk melakukan modeling dengan Collaborative Filtering
Menggunakan fitur `userId`, `movieId`, dan `rating` sebagai input utama untuk metode Collaborative Filtering. Fitur `userId` merepresentasikan identitas unik setiap pengguna, `movieId` sebagai identitas unik setiap film, dan `rating` mencerminkan preferensi pengguna terhadap film tertentu. Ketiga fitur ini digunakan untuk mempelajari pola interaksi antara pengguna dan item, sehingga sistem dapat merekomendasikan film berdasarkan kesamaan perilaku pengguna atau kesamaan preferensi antar item.

### 2. Encoding Data

### 3. Mengacak Data

## 📚 Referensi
- Prasetyo, H., & Nugroho, I. (2022). Analisis Perkembangan Industri Perfilman dan Peran Teknologi Informasi di Indonesia. Jurnal Pengembangan Teknologi Informasi dan Ilmu Komputer, 6(2), 235-242. https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/download/9163/4159
- Nababan, R. B., & Trisna, R. (2021). Rekomendasi Film Berdasarkan Preferensi Genre dan Usia Menggunakan Algoritma K-Nearest Neighbor. Proceeding of Engineering, 7(2), 326–331. https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/16511/16220
