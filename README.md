# Laporan Proyek Machine Learning
## Movies Recommendation System
Nama     : Andre Saputra Ginting

Username : andresaputra26

Email    : andresaputra260604@gmail.com

## Project Overview
Pertumbuhan industri perfilman, baik di tingkat internasional maupun nasional, menunjukkan perkembangan yang sangat menjanjikan. Hal ini tercermin dari peningkatan jumlah penonton bioskop yang terus bertambah setiap tahunnya. Pada tahun 2018, jumlah penonton bioskop di Indonesia telah melampaui 50 juta orang, dengan hampir 200 judul film dari produksi dalam dan luar negeri yang telah diputar di seluruh wilayah Indonesia (Prasetyo & Nugroho, 2022). Dalam industri perfilman, pengelompokan penonton dilakukan melalui kategori tertentu seperti klasifikasi usia dan pemilihan genre pada setiap film yang diproduksi. Oleh karena itu, diperlukan sistem rekomendasi yang mampu membantu penonton dalam menentukan genre film yang sesuai dengan preferensi serta batasan usia mereka (Nababan & Trisna, 2021).

Untuk mengatasi permasalahan dalam pemberian rekomendasi film, salah satu solusi yang diterapkan adalah penggunaan metode content-based filtering. Teknik ini bekerja dengan memanfaatkan informasi dari atribut-atribut film seperti genre, nama sutradara, aktor utama, serta ringkasan cerita. Dengan menganalisis kemiripan antar atribut tersebut, sistem mampu mengenali hubungan antar film dan memberikan rekomendasi berdasarkan kesamaan karakteristik. Ketika pengguna menyukai atau tertarik pada sebuah film, sistem secara otomatis menyarankan film lain yang memiliki profil serupa. Pendekatan ini bertujuan untuk meningkatkan relevansi hasil rekomendasi serta kepuasan pengguna terhadap sistem (Zakharia et al., 2024).

Selain pendekatan content-based filtering, metode lain yang umum digunakan dalam sistem rekomendasi adalah Collaborative Filtering (CF). Metode ini bekerja dengan memprediksi preferensi atau ketertarikan seorang pengguna terhadap suatu item berdasarkan kesamaan pola perilaku dan penilaian dari pengguna lain. CF mengandalkan data seperti rating yang diberikan oleh pengguna untuk mengidentifikasi hubungan antar pengguna dan merekomendasikan item yang disukai oleh pengguna dengan preferensi serupa. Selain rating, proses ini juga melibatkan evaluasi item melalui opini atau pengalaman pengguna lain, sehingga sistem dapat memberikan rekomendasi yang lebih personal dan relevan (Agustian et al., 2020).

Proyek sistem rekomendasi film menggunakan Content-Based Filtering dan Collaborative Filtering penting diselesaikan karena membantu pengguna menemukan film yang sesuai dengan preferensi mereka secara efisien di tengah banyaknya pilihan yang tersedia. Content-Based Filtering memberikan rekomendasi berdasarkan karakteristik film yang disukai pengguna, sementara Collaborative Filtering memanfaatkan pola preferensi pengguna lain untuk memberikan rekomendasi yang lebih beragam dan relevan. Penggabungan kedua metode ini dapat meningkatkan akurasi dan variasi rekomendasi, sekaligus mengatasi keterbatasan masing-masing pendekatan. Dengan sistem rekomendasi yang efektif, pengalaman pengguna menjadi lebih personal dan menyenangkan, sekaligus mendukung penyedia layanan dalam memahami dan memenuhi kebutuhan pengguna dengan lebih baik.

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

### Visualisasi jumlah rating

![alternative text](images/jumlah_ratings.png)

### 📊 **Hasil Visualisasi**

* **Rating 4.0** menjadi rating yang paling banyak diberikan oleh pengguna, dengan jumlah mencapai **26.818 kali**. Hal ini menunjukkan bahwa sebagian besar pengguna memberikan penilaian positif terhadap film yang mereka tonton.

* Rating **3.0** juga sangat sering diberikan, sebanyak **20.047 kali**, diikuti oleh rating **5.0** (**13.211 kali**) dan **3.5** (**13.136 kali**). Pola ini menunjukkan bahwa mayoritas pengguna cenderung memberikan rating di rentang **tengah ke atas**, yaitu antara **3.0 hingga 5.0**.

* Rating paling rendah, yaitu **0.5**, sangat jarang diberikan, hanya sebanyak **1.370 kali**, diikuti oleh rating **1.5 (1.791 kali)** dan **1.0 (2.811 kali)**. Ini menunjukkan bahwa hanya sedikit pengguna yang benar-benar tidak menyukai film yang mereka tonton.

* **Distribusi ini bersifat skewed ke kanan**, artinya lebih banyak pengguna yang memberikan penilaian positif dibanding negatif. Hal ini bisa mencerminkan dua hal:

  1. Film yang ditonton umumnya berkualitas baik atau sesuai dengan preferensi pengguna.
  2. Pengguna cenderung memberikan penilaian lebih tinggi karena faktor subjektif seperti aktor favorit, alur cerita yang menarik, atau faktor nostalgia.

## Data Preparation
### 1. Merge Data `movies` dan `ratings`
Menggabungkan dua dataset utama (`movies.csv` dan `ratings.csv`) ke dalam satu DataFrame gabungan dilakukan dengan menggunakan relasi berdasarkan kolom `movieId`, yang merupakan kunci primer pada `movies.csv` dan kunci asing pada `ratings.csv`. Proses ini bertujuan untuk menyatukan informasi deskriptif mengenai film (seperti judul dan genre) dengan data interaksi pengguna (seperti `userId` dan `rating`). Dengan penggabungan ini, setiap baris dalam DataFrame akhir akan merepresentasikan satu instance rating yang mencakup siapa pengguna yang memberi rating, berapa nilai rating-nya, serta metadata film yang dinilai. Hal ini sangat penting dalam membangun sistem rekomendasi karena memungkinkan proses analisis preferensi pengguna dan pemodelan machine learning dilakukan secara lebih efisien dan komprehensif dalam satu struktur data yang utuh.

![alternative text](images/merge_data.png)

### Visualisasi Jumlah Title Film (Top 20)

![alternative text](images/Jumlah_title_film.png)

### 📊 **Hasil Visualisasi**

* Film **Forrest Gump (1994)** menjadi film dengan **jumlah kemunculan terbanyak** dalam dataset, yaitu sebanyak **329 kali**, diikuti oleh **The Shawshank Redemption (1994)** (**317 kali**) dan **Pulp Fiction (1994)** (**307 kali**). Hal ini menunjukkan bahwa film-film ini sangat populer dan sering dinilai oleh pengguna.

* Sebagian besar film yang masuk dalam 20 besar berasal dari **dekade 1990-an**, menunjukkan bahwa era ini mendominasi dalam hal jumlah film yang menarik perhatian pengguna. Beberapa film dari tahun 1980-an dan 2000-an juga muncul, seperti *Star Wars: Episode V (1980)* dan *The Lord of the Rings: The Fellowship of the Ring (2001)*.

* Genre yang dominan dalam daftar ini mencakup **Drama, Crime, Adventure, dan Sci-Fi**, menandakan bahwa pengguna cenderung lebih banyak menonton dan memberi penilaian pada film-film dengan narasi yang kuat dan mendalam.

* Menariknya, film **animasi dan keluarga** seperti *Toy Story (1995)* juga masuk ke dalam daftar ini, menunjukkan bahwa genre keluarga tetap memiliki tempat di hati pengguna meskipun lebih sedikit dibanding genre drama atau thriller.

### 2. Menghapus kolom `timestamp`
Menghapus kolom `timestamp` karena tidak digunakan dalam membuat sistem rekomendasi.

![alternative text](images/delete_column.png)

### 3. Mengatasi Missing Values
Menghapus baris data yang memiliki nilai kosong (missing values) pada kolom penting seperti `userId` dan `rating`, yang masing-masing memiliki 18 nilai kosong. Nilai yang hilang pada kolom ini dapat memengaruhi kualitas sistem rekomendasi karena berisi informasi utama tentang pengguna dan preferensinya. Dengan menghapus total 18 baris yang mengandung missing values, data menjadi lebih bersih dan valid untuk dianalisis atau digunakan dalam pelatihan model rekomendasi.

![alternative text](images/missing_values.png)

### 4. Mengatasi data duplikat
Terlihat tidak ada data duplikat.

![alternative text](images/delete_duplicated.png)

### 5. Menghapus Simbol pada kolom `title` dan `genres`
Menghapus simbol tanda kurung pada tahun yang terdapat di kolom `title` dengan mengganti pola teks seperti `(2023)` menjadi hanya `2023`, serta mengubah isi kolom `genres` yang awalnya berupa string dengan genre yang dipisahkan oleh tanda `|` menjadi list atau array genre terpisah, sehingga memudahkan pengolahan data genre secara individual.

![alternative text](images/delete_symbol.png)

### Visualisasi Judul Film Berdasarkan Genre

![alternative text](images/film_by_genre.png)

### 📊 **Hasil Visualisasi**
- Genre Drama merupakan genre yang paling banyak muncul, dengan 41.928 judul film atau sekitar 15,3% dari total keseluruhan.
- Diikuti oleh Comedy (14,2%), Action (11,2%), dan Thriller (9,6%), yang juga memiliki jumlah film yang cukup tinggi.
- Genre seperti Western, Documentary, dan Film-Noir memiliki jumlah film yang jauh lebih sedikit, masing-masing hanya 0,7%, 0,4%, dan 0,3% dari total.
- Selain itu, terdapat pula kategori (no genres listed) yang mencakup 47 judul film atau sekitar 0,0%, menunjukkan bahwa sejumlah kecil film tidak memiliki genre yang terklasifikasi.

Untuk kategori no genres listed akan dihapus.

### Visualisasi Rata-rata Rating per Genre

![alternative text](images/rata-rata_rating_pergenre.png)

### 📊 **Hasil Visualisasi**

- Genre **Film-Noir** memiliki **rata-rata rating tertinggi** dibandingkan genre lainnya, yaitu sebesar **3,92**, diikuti oleh genre **War (3,81)** dan **Documentary (3,80)**. Ketiga genre ini menunjukkan kualitas atau apresiasi yang tinggi dari pengguna meskipun jumlah filmnya relatif lebih sedikit dibanding genre populer lainnya.

- Genre seperti **Drama** dan **Crime** juga menunjukkan rating cukup tinggi (**3,66**), menandakan konsistensi kualitas meskipun jumlah judulnya banyak.

- Sebaliknya, genre **Horror** menempati posisi terendah dengan rata-rata rating sebesar **3,26**, diikuti oleh **Comedy (3,38)** dan **Children (3,41)**. Hal ini mungkin mencerminkan selera pengguna yang lebih kritis terhadap genre-genre tersebut atau kualitas yang lebih bervariasi.

- Menariknya, kategori **(no genres listed)** memiliki rata-rata rating **3,49**, menunjukkan bahwa meskipun tidak diklasifikasikan ke dalam genre tertentu, film-film tersebut tetap mendapatkan apresiasi cukup baik dari pengguna.

### 6. Menghapus data pada kolom `title` yang tidak memiliki genre
Menghapus baris-baris pada DataFrame `df_merge` yang kolom `genres`-nya mengandung nilai `'(no genres listed)'`. Dengan menggunakan fungsi `apply` dan `lambda`, setiap baris dicek apakah genre tersebut tidak mengandung string tersebut, sehingga hanya data dengan genre yang valid yang disimpan. Setelah proses penghapusan, kode mencetak jumlah baris yang tersisa dan menampilkan beberapa baris pertama dari DataFrame hasil pembersihan tersebut.

![alternative text](images/delete_nogenre.png)

## Content Based Filtering

**Kelebihan:**

* **Personalized:** Rekomendasi didasarkan pada preferensi dan riwayat pengguna sendiri, sehingga hasilnya sangat personal.
* **Tidak memerlukan data pengguna lain:** Cukup data profil item dan data interaksi pengguna sendiri.
* **Mudah memahami alasan rekomendasi:** Karena didasarkan pada fitur konten, alasan rekomendasi lebih transparan.
* **Dapat merekomendasikan item baru (cold start item):** Selama fitur konten tersedia, item baru bisa direkomendasikan walaupun belum ada interaksi pengguna.

**Kekurangan:**

* **Over-specialization:** Rekomendasi cenderung monoton, hanya menyarankan item yang sangat mirip dengan yang sudah pernah digunakan, sehingga kurang beragam.
* **Butuh fitur konten yang lengkap dan informatif:** Jika fitur item kurang baik, kualitas rekomendasi juga menurun.
* **Cold start pengguna baru:** Untuk pengguna baru yang belum punya riwayat, sulit memberikan rekomendasi yang relevan.

---

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

- Mencari title `Clueless 1995`

![alternative text](images/title_predictinput.png)

**Output mencari title `Clueless 1995`**
| movieId | title         | genres\_string |
| ------- | ------------- | -------------- |
| 1878    | Clueless 1995 | Comedy Romance |

- Hasil rekomendasi

![alternative text](images/output_cbf.png)

| No. | Title                            | Genres String  |
| --- | -------------------------------- | -------------- |
| 0   | Run Fatboy Run 2007              | Comedy Romance |
| 1   | Fever Pitch 2005                 | Comedy Romance |
| 2   | Even Cowgirls Get the Blues 1993 | Comedy Romance |
| 3   | Bride Wars 2009                  | Comedy Romance |
| 4   | Dave 1993                        | Comedy Romance |
| 5   | Look Who's Talking 1989          | Comedy Romance |
| 6   | For Love or Money 1993           | Comedy Romance |
| 7   | MatchMaker, The 1997             | Comedy Romance |
| 8   | Her Alibi 1989                   | Comedy Romance |
| 9   | Dirty 30 2016                    | Comedy Romance |


## Collaborative Filtering

**Kelebihan:**

* **Mampu menemukan pola dan rekomendasi yang lebih bervariasi:** Tidak hanya berdasarkan fitur, tapi juga pola perilaku pengguna lain, sehingga bisa merekomendasikan item yang mungkin tidak mirip secara konten tapi relevan.
* **Tidak bergantung pada fitur konten item:** Bisa digunakan bahkan kalau data konten item terbatas atau tidak tersedia.
* **Meningkatkan keragaman rekomendasi:** Karena didasarkan pada preferensi pengguna lain, lebih mudah keluar dari "zona nyaman" konten yang sudah dikenal.

**Kekurangan:**

* **Cold start problem:** Sulit memberikan rekomendasi pada pengguna baru yang belum punya interaksi atau item baru yang belum ada interaksi.
* **Data sparcity:** Jika interaksi pengguna-item sangat sedikit, kualitas rekomendasi menurun.
* **Scalability:** Butuh komputasi besar saat jumlah pengguna dan item sangat banyak.
* **Risiko popularitas bias:** Rekomendasi cenderung mengutamakan item populer sehingga item niche kurang terekomendasi.

---

### 1. Memilih Fitur yang digunakan untuk melakukan modeling dengan Collaborative Filtering
Menggunakan fitur `userId`, `movieId`, dan `rating` sebagai input utama untuk metode Collaborative Filtering. Fitur `userId` merepresentasikan identitas unik setiap pengguna, `movieId` sebagai identitas unik setiap film, dan `rating` mencerminkan preferensi pengguna terhadap film tertentu. Ketiga fitur ini digunakan untuk mempelajari pola interaksi antara pengguna dan item, sehingga sistem dapat merekomendasikan film berdasarkan kesamaan perilaku pengguna atau kesamaan preferensi antar item.

### 2. Encoding Data
Dalam sistem rekomendasi film berbasis Collaborative Filtering, Label Encoding pada kolom `userId` dan `movieId` mengubah data asli menjadi indeks numerik berurutan yang memudahkan pemodelan dan komputasi. Proses ini membantu algoritma memahami pola preferensi pengguna dengan lebih efisien dan memungkinkan interpretasi hasil rekomendasi secara mudah. Dengan encoding, data siap diproses untuk menghasilkan rekomendasi film yang akurat dan relevan.

### 3. Mengacak Data
Acak datanya terlebih dahulu agar distribusinya menjadi random. Proses ini bertujuan untuk mengacak urutan data agar distribusinya menjadi lebih acak dan tidak mengikuti pola tertentu, sehingga model machine learning dapat belajar dari sampel yang lebih representatif dan beragam.

### 4. Membagi Data untuk Training dan Validasi
Membagi dataset menjadi dua bagian: data pelatihan (training set) dan data validasi (validation set) menggunakan metode **train-test split**, dengan proporsi pembagian 80:20. Tujuan dari proses ini adalah agar model dapat belajar dari sebagian data dan kemudian diuji pada data yang belum pernah digunakan sebelumnya, sehingga evaluasi performa model menjadi lebih akurat dan model dapat menghindari overfitting.

### 5. Modeling Collaborative Filtering
Class `RecommenderNet` membuat model rekomendasi yang menggunakan embedding untuk merepresentasikan pengguna dan restoran dalam bentuk vektor berdimensi rendah. Model ini memiliki empat layer embedding: dua untuk fitur utama (`user_embedding` dan `resto_embedding`) dan dua untuk bias (`user_bias` dan `resto_bias`). Dalam proses prediksi, model menghitung dot product antara embedding pengguna dan restoran, lalu menambahkan bias masing-masing, dan mengaplikasikan fungsi sigmoid untuk menghasilkan skor prediksi antara 0 dan 1. Embedding diinisialisasi dengan `he_normal` dan diberi regularisasi L2 untuk mencegah overfitting, berikut adalah parameternya:

| Parameter                | Deskripsi                                                                                         | Tipe Data         | Contoh Nilai                           |
| ------------------------ | ------------------------------------------------------------------------------------------------- | ----------------- | -------------------------------------- |
| `num_users`              | Jumlah total pengguna unik. Digunakan untuk menentukan ukuran layer embedding pengguna.           | Integer           | 610                                    |
| `num_resto`              | Jumlah total restoran (atau film) unik. Menentukan ukuran layer embedding restoran.               | Integer           | 9690                                   |
| `embedding_size`         | Dimensi vektor embedding untuk pengguna dan restoran. Menentukan ukuran representasi fitur laten. | Integer           | 50                                     |
| `user_embedding`         | Layer embedding yang merepresentasikan pengguna sebagai vektor berdimensi `embedding_size`.       | Keras Layer       | `Embedding(num_users, embedding_size)` |
| `user_bias`              | Layer embedding bias untuk pengguna, menghasilkan satu nilai bias per pengguna.                   | Keras Layer       | `Embedding(num_users, 1)`              |
| `resto_embedding`        | Layer embedding yang merepresentasikan restoran sebagai vektor berdimensi `embedding_size`.       | Keras Layer       | `Embedding(num_resto, embedding_size)` |
| `resto_bias`             | Layer embedding bias untuk restoran, menghasilkan satu nilai bias per restoran.                   | Keras Layer       | `Embedding(num_resto, 1)`              |
| `embeddings_initializer` | Metode inisialisasi bobot embedding, digunakan `'he_normal'` dalam kode.                          | String            | `'he_normal'`                          |
| `embeddings_regularizer` | Regularisasi L2 pada embedding untuk mencegah overfitting, dengan nilai `1e-6`.                   | Keras Regularizer | `keras.regularizers.l2(1e-6)`          |

Menginisialisasi model RecommenderNet dengan jumlah pengguna sebanyak 610 dan jumlah film sebanyak 9690, serta ukuran embedding 40. Model kemudian dikompilasi menggunakan fungsi loss BinaryCrossentropy, optimizer Adam dengan learning rate 0.001, dan metrik evaluasi Root Mean Squared Error (RMSE) untuk mengukur akurasi prediksi rating yang berada pada rentang 0.5 sampai 5.0.

| Parameter        | Deskripsi                                   | Tipe Data        | Nilai pada Data Anda        |
| ---------------- | ------------------------------------------- | ---------------- | --------------------------- |
| `num_users`      | Jumlah total pengguna unik                  | Integer          | 610                         |
| `num_movies`     | Jumlah total film unik                      | Integer          | 9690                        |
| `embedding_size` | Dimensi vektor embedding                    | Integer          | 50                          |
| `loss`           | Fungsi kerugian saat training               | Loss Function    | `BinaryCrossentropy`        |
| `optimizer`      | Algoritma optimisasi model                  | Optimizer Object | `Adam(learning_rate=0.001)` |
| `metrics`        | Metode evaluasi performa model              | List             | `[RootMeanSquaredError()]`  |
| `rating_range`   | Rentang nilai rating pengguna terhadap film | Float Range      | 0.5 – 5.0                   |

### 6. Evaluasi
Menjalankan proses pelatihan (training) model rekomendasi menggunakan data training X_train dan target y_train. Proses pelatihan dilakukan selama 20 epoch dengan ukuran batch sebanyak 8 data per iterasi. Selain itu, model juga divalidasi pada setiap epoch menggunakan data validasi (X_val, y_val) untuk memantau performa model pada data yang tidak dilatih secara langsung. Hasil pelatihan dan validasi disimpan dalam variabel history yang bisa digunakan untuk analisis lebih lanjut, seperti melihat grafik loss dan akurasi selama training.

Untuk mengevaluasi kinerja sistem rekomendasi, digunakan metrik **Root Mean Squared Error (RMSE)**, yang mengukur tingkat kesalahan prediksi rating film dibandingkan dengan rating asli dari pengguna.

RMSE adalah metrik evaluasi yang digunakan untuk mengukur seberapa besar perbedaan (galat) antara nilai yang diprediksi oleh model dengan nilai aktual (yang sebenarnya). RMSE sering digunakan dalam regresi dan sistem rekomendasi untuk menilai akurasi prediksi.

Rumus: 

![alternative text](images/RMSE.png)

Hasil Akhir: 

| Metric          | Hasil (Akhir) |
| --------------- | ------------- |
| Training Loss   | 0.5890        |
| Training RMSE   | 0.1786        |
| Validation Loss | 0.6080        |
| Validation RMSE | 0.1979        |

Hasil pelatihan menunjukkan model memiliki error rendah dengan training RMSE 0.1786 dan validation RMSE 0.1979. Perbedaan kecil antara training dan validation menandakan model tidak overfitting dan mampu memprediksi rating film dengan cukup baik.

#### Perbandingan Training dan Validation Loss

![alternative text](images/evaluasi_model_loss.png)

Grafik *Training and Validation Loss* memperlihatkan bahwa *training loss* terus menurun selama proses pelatihan, yang berarti model semakin baik dalam mempelajari data pelatihan. Sementara itu, *validation loss* juga menurun dan tetap stabil setelah beberapa epoch, menandakan model tidak mengalami overfitting dan mampu bekerja dengan baik pada data baru.

#### Perbandingan Training dan Validation RMSE

![alternative text](images/evaluasi_model_rmse.png)

Pada grafik *Training and Validation RMSE*, *training RMSE* menurun secara konsisten, sedangkan *validation RMSE* menurun pada awal pelatihan dan kemudian stabil pada nilai yang rendah. Selisih antara RMSE pada data training dan validation cukup kecil, menunjukkan model memiliki performa yang seimbang dan dapat dipercaya untuk prediksi di sistem rekomendasi film.

### Output Rekomendasi Film dengan Collaborative Filtering

![alternative text](images/output_cf.png)

### 🎥 **Showing Recommendations for User: 418**

#### ✅ Movie with High Ratings from User

| **Title**                              | **Genres**                 |
| -------------------------------------- | -------------------------- |
| Shawshank Redemption, The (1994)       | Crime, Drama               |
| Trainspotting (1996)                   | Comedy, Crime, Drama       |
| Monty Python's Life of Brian (1979)    | Comedy                     |
| Monty Python and the Holy Grail (1975) | Adventure, Comedy, Fantasy |
| To Kill a Mockingbird (1962)           | Drama                      |

#### ⭐ Top 10 Movie Recommendation

| **Title**                                              | **Genres**                   |
| ------------------------------------------------------ | ---------------------------- |
| Wallace & Gromit: The Best of Aardman Animation (1996) | Adventure, Animation, Comedy |
| Philadelphia Story, The (1940)                         | Comedy, Drama, Romance       |
| Rear Window (1954)                                     | Mystery, Thriller            |
| It Happened One Night (1934)                           | Comedy, Romance              |
| Casablanca (1942)                                      | Drama, Romance               |
| Lifeboat (1944)                                        | Drama, War                   |
| Hours, The (2002)                                      | Drama, Romance               |
| Dune (2000)                                            | Drama, Fantasy, Sci-Fi       |
| Louis C.K.: Shameless (2007)                           | Comedy                       |
| Three Billboards Outside Ebbing, Missouri (2017)       | Crime, Drama                 |

### ✅ Evaluasi Berdasarkan Permasalahan & Tujuan

* ✔ **Kesulitan dalam menentukan film yang tepat** berhasil diatasi dengan adanya sistem rekomendasi otomatis.
* ✔ **Personalisasi konten berhasil dicapai**, karena sistem menyesuaikan rekomendasi dengan preferensi dan aktivitas pengguna.
* ✔ **Proses pemilihan film menjadi lebih efisien**, sehingga pengguna tidak perlu menghabiskan waktu lama untuk memilih tontonan.

### 📈 Dampak terhadap Pemahaman Bisnis

* 💡 Mendorong loyalitas pengguna dengan menyediakan rekomendasi yang sesuai dengan selera masing-masing.
* 💡 Mempermudah pengguna dalam menemukan film, sehingga meningkatkan kenyamanan dan kepuasan saat menggunakan layanan.
* 💡 Mendukung strategi platform hiburan dalam menyajikan konten yang lebih relevan dan meningkatkan interaksi pengguna.

## 📚 Referensi
- Prasetyo, H., & Nugroho, I. (2022). Analisis Perkembangan Industri Perfilman dan Peran Teknologi Informasi di Indonesia. Jurnal Pengembangan Teknologi Informasi dan Ilmu Komputer, 6(2), 235-242. https://j-ptiik.ub.ac.id/index.php/j-ptiik/article/download/9163/4159
- Nababan, R. B., & Trisna, R. (2021). Rekomendasi Film Berdasarkan Preferensi Genre dan Usia Menggunakan Algoritma K-Nearest Neighbor. Proceeding of Engineering, 7(2), 326–331. https://openlibrarypublications.telkomuniversity.ac.id/index.php/engineering/article/view/16511/16220
- Zakharia, A., Ulhaq, A. D., Suryono, A. B., Nugroho, N. C., Hafith, D. F., & Gusmao, N. D. A. (2024). Sistem Rekomendasi Film Indonesia Menggunakan Metode Content-Based Filtering. LOGIC: Jurnal Ilmu Komputer dan Pendidikan, 2(4), 671–678. https://journal.mediapublikasi.id/index.php/logic/article/download/4299/2851/10661
- Agustian, A., & Suryanegara, M. (2020). Sistem Rekomendasi Film Menggunakan Metode Collaborative Filtering dan K-Nearest Neighbors. Jurnal Aplikasi dan Teori Ilmu Komputer (JATIKOM), 3(1), 1–8. https://ejournal.upi.edu/index.php/JATIKOM/article/download/33208/14281
